---
title: ファームウェアのメジャー ブートとホストの構成証明 - Azure のセキュリティ
description: Azure ファームウェアのメジャー ブートとホストの構成証明の技術的概要。
author: yosharm
ms.service: security
ms.subservice: security-fundamentals
ms.topic: article
ms.author: terrylan
manager: rkarlin
ms.date: 06/24/2021
ms.openlocfilehash: af2927e4aa9dc9044546537adbde3af97cba4be1
ms.sourcegitcommit: 692382974e1ac868a2672b67af2d33e593c91d60
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2021
ms.locfileid: "130249383"
---
# <a name="measured-boot-and-host-attestation"></a>メジャー ブートとホストの構成証明
この記事では、メジャー ブートとホストの構成証明を通じて、Microsoft がホストの整合性とセキュリティを確保する方法について説明します。

## <a name="measured-boot"></a>メジャー ブート

[トラステッド プラットフォーム モジュール](/windows/security/information-protection/tpm/trusted-platform-module-top-node) (TPM) は、信頼できるサードパーティによって提供されるファームウェアを使用する、暗号化によってセキュリティで保護された改ざん防止監査コンポーネントです。 ブート構成ログには、ホストでブートストラップ シーケンスが前回行われたときに、そのプラットフォーム構成レジスタ (PCR) に記録されたハッシュチェーン測定値が含まれています。 次の図に、この記録プロセスを示します。 前にハッシュされた測定値を次の測定値のハッシュに増分的に追加し、そのハッシュ アルゴリズムを共用体で実行すると、ハッシュチェーンが実現します。

![ホストの構成証明サービスのハッシュチェーンを示す図。](./media/measured-boot-host-attestation/hash-chaining.png)

構成証明は、ホストでそのブート構成ログ (TCGLog) を使用して構成状態が提供されたときに実行されます。 TPM では読み取りおよび拡張操作以外の PCR 値が公開されないため、ブート ログの偽造は困難です。 さらに、ホストの構成証明サービスによって提供される資格情報は、特定の PCR 値にシールされます。 ハッシュチェーンを使用すると、資格情報を帯域外でスプーフィングまたはシール解除することが不可能になります。

## <a name="host-attestation-service"></a>ホストの構成証明サービス

ホストの構成証明サービスは、顧客データまたはワークロードとのやりとりを許可する前に、ホスト マシンが信頼できるかどうかを確認する予防措置です。 ホストの構成証明サービスでは、各ホストから送信されたコンプライアンス ステートメント (ホストのコンプライアンスの検証可能な証明) を構成証明ポリシー (セキュリティで保護された状態の定義) に照らして検証することで、確認が行われます。 このシステムの整合性は、TPM によって提供される [root-of-trust](https://www.uefi.org/sites/default/files/resources/UEFI%20RoT%20white%20paper_Final%208%208%2016%20%28003%29.pdf) によって保証されます。

ホストの構成証明サービスは、特定のロックダウン環境内の各 Azure クラスターに存在します。 ロックダウンされた環境には、ホスト マシン ブートストラップ プロトコルに参加するその他のゲートキー パーサービスが含まれています。 公開キー基盤 (PKI) は、構成証明要求を検証するための仲介役として、また、ID 発行元として (ホストの構成証明が成功した場合) 機能します。 証明ホストに発行された構成証明後の資格情報は、その ID にシールされます。 要求元のホストでのみ、資格情報をシールし、それらを利用して増分アクセス許可を取得することができます。 これにより、中間者攻撃やスプーフィング攻撃を防ぐことができます。

Azure ホストが、工場出荷時に、セキュリティが誤った構成で到着した場合、またはデータセンターで改ざんされている場合、その TCGLog には、ホストの構成証明サービスによって次回の構成証明に対してフラグが設定された侵害のインジケーターが含まれています。これにより、構成証明が失敗します。 構成証明が失敗すると、Azure フリートは問題のあるホストを信頼できなくなります。 この妨害により、ホストとの間のすべての通信が実質的にブロックされ、インシデント ワークフローがトリガーされます。 根本的な原因と潜在的な侵害の兆候を特定するために、調査と詳細な事後分析が実施されます。 分析が完了した後にのみ、ホストが修復され、Azure フリートに参加して顧客のワークロードを実行することができます。

ホストの構成証明サービスのアーキテクチャの概要を次に示します。

![ホストの構成証明サービスのアーキテクチャを示す図。](./media/measured-boot-host-attestation/host-attestation-arch.png)

## <a name="attestation-measurements"></a>構成証明の測定値

現在キャプチャされているさまざまな測定値の例を次に示します。

### <a name="secure-boot-and-secure-boot-keys"></a>セキュア ブートとセキュア ブート キー
署名データベースと失効署名データベースのダイジェストが正しいことを検証することで、クライアント エージェントで適切なソフトウェアを信頼できると判断されていることが、ホストの構成証明サービスによって保証されます。 公開キー登録キー データベースと公開プラットフォーム キーの署名を検証することで、信頼できる関係者のみが、信頼できると見なされるソフトウェアの定義を変更するアクセス許可を保持していることが、ホストの構成証明サービスで確認されます。 最後に、セキュア ブートがアクティブになっていることを確保することで、これらの定義が適用されていることがホストの構成証明サービスにより検証されます。

### <a name="debug-controls"></a>デバッグ コントロール
デバッガーは、開発者向けの強力なツールです。 ただし、メモリやその他のデバッグ コマンドへの自由なアクセスが、信頼できない関係者に与えられた場合、データの保護とシステムの整合性が損なわれるおそれがあります。 ホストの構成証明サービスを使用すると、運用環境でのブート時にすべての種類のデバッグが確実に無効になります。

### <a name="code-integrity"></a>コードの整合性
UEFI [セキュア ブート](secure-boot.md)により、ブート シーケンス中に、確実に信頼できる低レベルのソフトウェアのみを実行することができます。 しかし、カーネル モード アクセスを使用するドライバーやその他の実行可能ファイルには、ブート後の環境でも同じチェックを適用する必要があります。 そのため、コードの整合性 (CI) ポリシーを使用して、有効および無効な署名を指定することにより、信頼できると見なされるドライバー、バイナリ、およびその他の実行可能ファイルが定義されます。 これらのポリシーは強制的に適用されます。 ポリシーの違反があると、調査のためにセキュリティ インシデント対応チームに対してアラートが生成されます。

## <a name="next-steps"></a>次のステップ
プラットフォームの整合性とセキュリティを強化する方法の詳細については、次を参照してください。

- [ファームウェアのセキュリティ](firmware.md)
- [プラットフォーム コードの整合性](code-integrity.md)
- [セキュア ブート](secure-boot.md)
- [プロジェクト Cerberus](project-cerberus.md)
- [保存時の暗号化](encryption-atrest.md)
- [ハイパーバイザー セキュリティ](hypervisor.md)
