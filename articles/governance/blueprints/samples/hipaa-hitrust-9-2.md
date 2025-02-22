---
title: HIPAA HITRUST 9.2 ブループリント サンプルの概要
description: HIPAA HITRUST 9.2 ブループリント サンプルの概要。 このブループリント サンプルは、お客様が特定の HIPAA HITRUST 9.2 コントロールを評価するのに役立ちます。
ms.date: 09/08/2021
ms.topic: sample
ms.openlocfilehash: f566ea3fdc1d9922a99e375fab517203da59d526
ms.sourcegitcommit: f6e2ea5571e35b9ed3a79a22485eba4d20ae36cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/24/2021
ms.locfileid: "128658270"
---
# <a name="hipaa-hitrust-92-blueprint-sample"></a>HIPAA HITRUST 9.2 ブループリント サンプル

HIPAA HITRUST 9.2 ブループリント サンプルでは、特定の HIPAA HITRUST 9.2 コントロールの評価に役立つ、[Azure Policy](../../policy/overview.md) を使用したガバナンス ガードレールが提供されます。
このブループリントは、HIPAA HITRUST 9.2 コントロールを実装する必要がある Azure でデプロイされたアーキテクチャのために、お客様が一連の主要なポリシーをデプロイするのに役立ちます。

## <a name="control-mapping"></a>コントロール マッピング

[Azure Policy のコントロール マッピング](../../policy/samples/hipaa-hitrust-9-2.md)では、このブループリント内に含まれるポリシー定義についてと、それらのポリシー定義が HIPAA HITRUST 9.2 の **コンプライアンス ドメイン** および **コントロール** にどのようにマッピングされるかについて詳しく説明します。 リソースはアーキテクチャに割り当てられると、割り当て済みのポリシー定義に違反していないかどうかを Azure Policy によって評価されます。 詳細については、[Azure Policy](../../policy/overview.md) に関するページをご覧ください。

## <a name="deploy"></a>配置

Azure Blueprints HIPAA HITRUST 9.2 ブループリント サンプルをデプロイするには、以下の手順を行う必要があります。

> [!div class="checklist"]
> - サンプルから新しいブループリントを作成する
> - サンプルのコピーを **発行済み** としてマークする
> - ブループリントのコピーを既存のサブスクリプションに割り当てる

Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/free) を作成してください。

### <a name="create-blueprint-from-sample"></a>サンプルからブループリントを作成する

最初に、サンプルをスターターとして使用して環境内に新しいブループリントを作成することにより、ブループリント サンプルを実装します。

1. 左側のウィンドウにある **[すべてのサービス]** を選択します。 **[ブループリント]** を探して選択します。

1. 左側の **[はじめに]** ページで、 _[ブループリントの作成]_ の下にある **[作成]** ボタンを選択します。

1. _[その他のサンプル]_ で **[HIPAA HITRUST]** ブループリント サンプルを見つけて、 **[このサンプルを使用する]** を選択します。

1. ブループリント サンプルの _[基本]_ を入力します。

   - **[ブループリントの名前]** : HIPAA HITRUST 9.2 ブループリント サンプルのコピーの名前を指定します。
   - **[定義の場所]** :省略記号を使用して、サンプルのコピーを保存する管理グループを選択します。

1. ページの上部にある _[アーティファクト]_ タブまたはページの下部にある **[次へ: アーティファクト]** を選択します。

1. ブループリント サンプルを構成するアーティファクトの一覧を確認します。 多くのアーティファクトには、後で定義するパラメーターがあります。 ブループリント サンプルの確認が完了したら、 **[下書きの保存]** を選択します。

### <a name="publish-the-sample-copy"></a>サンプルのコピーを発行する

環境でのブループリント サンプルのコピーの作成が完了しました。 これは **下書き** モードで作成されており、割り当ておよびデプロイの前に **発行** する必要があります。 ブループリント サンプルのコピーは、お使いの環境や必要性に応じてカスタマイズできますが、それが原因で HIPAA HITRUST 9.2 コントロールに準拠しなくなる可能性もあります。

1. 左側のウィンドウにある **[すべてのサービス]** を選択します。 **[ブループリント]** を探して選択します。

1. 左側の **[ブループリントの定義]** ページを選択します。 ブループリント サンプルのコピーを、フィルターを使用して検索し、選択します。

1. ページの上部にある **[ブループリントを発行する]** を選択します。 右側の新しいページで、ブループリント サンプルのコピーの **[バージョン]** を指定します。 このプロパティは、後で変更を加える場合に役立ちます。 **[変更に関するメモ]** に入力します (例: 「HIPAA HITRUST 9.2 ブループリント サンプルから発行する最初のバージョン」)。 次に、ページの下部にある **[発行]** を選択します。

### <a name="assign-the-sample-copy"></a>サンプルのコピーを割り当てる

正常に **発行** されたブループリント サンプルのコピーは、保存先の管理グループ内のサブスクリプションに割り当てることができます。 この手順では、ブループリント サンプルのコピーの各デプロイを一意にするためのパラメーターを指定します。

1. 左側のウィンドウにある **[すべてのサービス]** を選択します。 **[ブループリント]** を探して選択します。

1. 左側の **[ブループリントの定義]** ページを選択します。 ブループリント サンプルのコピーを、フィルターを使用して検索し、選択します。

1. ブループリント定義ページの上部にある **[ブループリントの割り当て]** を選択します。

1. ブループリント割り当て用のパラメーター値を指定します。

   - 基本

     - **サブスクリプション**:ブループリント サンプルのコピーを保存した管理グループ内の 1 つ以上のサブスクリプションを選択します。 複数のサブスクリプションを選択すると、入力したパラメーターを使用して、それぞれに対して割り当てが作成されます。
     - **割り当て名**:名前は、ブループリントの名前に基づいてあらかじめ設定されています。
       必要に応じて変更することも、そのままにしておくこともできます。
     - **[場所]** :マネージド ID を作成するリージョンを選択します。 Azure Blueprint は、この管理対象 ID を使用して、割り当てられたブループリント内にすべての成果物をデプロイします。 詳細については、[Azure リソースの管理対象 ID の概要](../../../active-directory/managed-identities-azure-resources/overview.md)に関するページをご覧ください。
     - **ブループリント定義ラベル**:ブループリント サンプルのコピーの **発行済み** バージョンを選択します。

   - ロックの割り当て

     お使いの環境のブループリントのロック設定を選択します。 詳細については、[ブループリント リソースのロック](../concepts/resource-locking.md)に関するページを参照してください。

   - マネージド ID

     既定の _システム割り当て_ マネージド ID オプションはそのままにします。

   - アーティファクトのパラメーター

     このセクションで定義するパラメーターは、定義対象のアーティファクトに適用されます。 これらのパラメーターはブループリントの割り当て時に定義されるので、[動的パラメーター](../concepts/parameters.md#dynamic-parameters)です。 アーティファクトのパラメーターとその説明を含む詳しい一覧については、「[アーティファクトのパラメーター表](#artifact-parameters-table)」を参照してください。

1. すべてのパラメーターの入力が完了したら、ページの下部にある **[割り当て]** を選択します。 ブループリントの割り当てが作成され、アーティファクトのデプロイが開始されます。 デプロイに要する時間は、約 1 時間です。 デプロイの状態を確認するには、ブループリントの割り当てを開きます。

> [!WARNING]
> Azure Blueprints サービスと、組み込まれているブループリント サンプルは、**無料** でご利用になれます。 Azure リソースは、[製品ごとに課金](https://azure.microsoft.com/pricing/)されます。 このブループリント サンプルでデプロイされるリソースの実行コストを見積もるには、[料金計算ツール](https://azure.microsoft.com/pricing/calculator/)を使用します。

### <a name="artifact-parameters-table"></a>アーティファクトのパラメーター表

以下の表は、ブループリント アーティファクトのパラメーターの一覧を示しています。

|アーティファクト名 |パラメーター名 |説明 |
|---|---|---|
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |インターネットに接続するエンドポイント経由のアクセスを制限する必要がある |制限が少なすぎる NSG 受信規則の監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |アカウント: Guest アカウントの状態 |ローカルの Guest アカウントを無効にするかどうかを指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |適応型アプリケーション制御を仮想マシンで有効にする必要がある |アプリケーション ホワイトリスト登録の監視を Azure Security Center で有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |インターネットまたは Windows ドメインへの同時接続を許可する |コンピューターがドメイン ベースのネットワークと非ドメイン ベースのネットワークの両方に、同時に接続されるのを防止するかどうかを指定します。 値が 0 の場合は同時接続が許可され、値が 1 の場合はブロックされます。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |API アプリには HTTPS V2 を介してのみアクセスできるようにする |API アプリ V2 における HTTPS の使用に関する監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |アプリケーション名 (ワイルドカード対応) |インストールする必要があるアプリケーションの名前をセミコロンで区切った一覧。 例: 'Microsoft SQL Server 2014 (64 ビット); Microsoft Visual Studio Code' または 'Microsoft SQL Server 2014*' ('Microsoft SQL Server 2014' で始まるアプリケーションに一致) |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |プロセス終了の監査 |プロセスが終了したときに監査イベントを生成するかどうかを指定します。 重要なプロセスの終了を監視するために推奨されます。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |ストレージ アカウントに対する制限のないネットワーク アクセスの監査 |ストレージ アカウントに対するネットワーク アクセスの監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |監査: セキュリティ監査のログを記録できない場合は直ちにシステムをシャットダウンする |セキュリティ イベントのログを記録できない場合に、システムがシャットダウンするかどうかを監査します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |証明書の拇印 |信頼されたルート証明書ストア (Cert:\LocalMachine\Root) に存在する必要がある証明書の拇印をセミコロンで区切った一覧。 例: THUMBPRINT1;THUMBPRINT2;THUMBPRINT3 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Batch アカウントで診断ログを有効にする必要がある |Batch アカウントで診断ログの監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |イベント ハブの診断ログを有効にする必要がある |イベント ハブ アカウントで診断ログの監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Search サービスにおける診断ログを有効にする必要がある |Azure Search サービスで診断ログの監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |仮想マシン スケール セットの診断ログを有効にする必要がある |Service Fabric で診断ログの監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |仮想マシンでディスク暗号化を適用する必要がある |VM のディスク暗号化の監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |安全でないゲスト ログオンを有効にする |SMB クライアントで SMB サーバーへの安全でないゲスト ログオンが許可されるかどうかを指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |仮想マシンに Just-In-Time ネットワーク アクセス制御を適用する必要がある |ネットワークのジャスト イン タイム アクセスの監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |仮想マシンの管理ポートを閉じておく必要がある |Virtual Machines の開いている管理ポートの監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |サブスクリプションに対する書き込みアクセス許可を持つアカウントに対して MFA を有効にする必要がある |サブスクリプションで書き込みアクセス許可を持つアカウントに対する MFA の監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |サブスクリプションで所有者アクセス許可を持つアカウントに対して MFA を有効にする必要がある |サブスクリプションで所有者アクセス許可を持つアカウントに対する MFA の監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |ネットワーク アクセス: リモートからアクセスできるレジストリのパス |`winreg` レジストリ キーのアクセス制御リスト (ACL) に一覧表示されているユーザーまたはグループに関係なく、どのレジストリ パスに対してネットワーク経由でアクセスできるかを指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |ネットワーク アクセス: リモートからアクセスできるレジストリのパスおよびサブパス |`winreg` レジストリ キーのアクセス制御リスト (ACL) に一覧表示されているユーザーまたはグループに関係なく、どのレジストリ パスとサブパスに対してネットワーク経由でアクセスできるかを指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |ネットワーク アクセス: 匿名でアクセスできる共有 |匿名ユーザーがアクセスできるネットワーク共有を指定します。 どのユーザーもサーバー上の共有リソースにアクセスする前に認証されている必要があるため、このポリシー設定の既定の構成はほとんど効果がありません。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |回復コンソール: すべてのドライブとフォルダーに、フロッピーのコピーとアクセスを許可する |回復コンソールの SET コマンドを使用できるようにするかどうかを指定します。これにより、回復コンソールの環境変数を設定できるようになります。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |API アプリでリモート デバッグを無効にする |API アプリのリモート デバッグの監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Web アプリケーションのリモート デバッグを無効にする |Web アプリのリモート デバッグの監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Batch アカウントにおけるログの必須の保持期間 (日) |診断ログの必須の保持期間 (日) |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Azure Search サービスにおけるログの必須の保持期間 (日) |診断ログの必須の保持期間 (日) |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |イベント ハブ アカウントにおけるログの必須の保持期間 (日) |診断ログの必須の保持期間 (日) |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |ネットワーク セキュリティ グループの診断設定をデプロイするためのストレージ アカウントのリソース グループ名 (存在する必要があります) |ストレージ アカウントが作成されるリソース グループ。 このリソース グループは、既に存在している必要があります。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Kubernetes サービスでロールベースのアクセス制御 (RBAC) を使用する必要がある |RBAC が有効にされていない Kubernetes サービスの監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |SQL マネージド インスタンスの TDE 保護機能を自分のキーを使用して暗号化する必要がある |独自のキー サポートを使用した Transparent Data Encryption (TDE) の監視を有効または無効にします。 独自キーのサポートを使用した TDE によって、TDE 保護機能での透明性と制御性が強化され、HSM で保護された外部サービスによるセキュリティが向上し、職務の分離が促進されます。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |SQL Server の TDE 保護機能を自分のキーを使用して暗号化する必要がある |独自のキー サポートを使用した Transparent Data Encryption (TDE) の監視を有効または無効にします。 独自キーのサポートを使用した TDE によって、TDE 保護機能での透明性と制御性が強化され、HSM で保護された外部サービスによるセキュリティが向上し、職務の分離が促進されます。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |ネットワーク セキュリティ グループの診断設定をデプロイするためのリージョン ストレージ アカウントのストレージ アカウント プレフィックス |このプレフィックスがネットワーク セキュリティ グループの場所と組み合わされて、作成されるストレージ アカウント名となります。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |仮想マシン スケール セットにシステムの更新プログラムをインストールする必要がある |システム更新プログラムの仮想マシン スケール セット レポートを有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |仮想マシン スケール セットにシステムの更新プログラムをインストールする必要がある |システム更新プログラムの仮想マシン スケール セット レポートを有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |マルチキャスト名前解決をオフにする |単一のサブネット上でローカル サブネット リンク経由のマルチキャストを使用して送信するセカンダリ名解決プロトコル (LLMNR) を、有効にするかどうかを指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |仮想マシンを新しい Azure Resource Manager リソースに移行する必要がある |従来のコンピューティング VM の監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |仮想マシン スケール セットのセキュリティ構成の脆弱性を修復する必要がある |仮想マシン スケール セットの OS 脆弱性の監視を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |脆弱性評価ソリューションによって脆弱性を修復する必要がある |脆弱性評価ソリューションによる VM 脆弱性の検出を有効または無効にします |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |脆弱性評価を SQL マネージド インスタンス上で有効にする必要がある |定期的な脆弱性評価スキャンが有効になっていない SQL マネージド インスタンスを監査します。 脆弱性評価は、潜在的なデータベースの脆弱性を検出、追跡、および修正するのに役立ちます。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (ドメイン): ローカル ファイアウォールの規則を適用する |ドメイン プロファイルのグループ ポリシーによって構成されるファイアウォール規則と一緒に適用されるローカル ファイアウォール規則の作成を、ローカル管理者に許可するかどうかを指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (ドメイン): 送信接続の動作 |送信ファイアウォール規則と一致しないドメイン プロファイルの送信接続の動作を指定します。 既定値の 0 は接続を許可することを意味し、値 1 は接続をブロックすることを意味します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (ドメイン): 送信接続の動作 |送信ファイアウォール規則と一致しないドメイン プロファイルの送信接続の動作を指定します。 既定値の 0 は接続を許可することを意味し、値 1 は接続をブロックすることを意味します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (ドメイン): 通知を表示する |プログラムが受信接続の受信をブロックされたときに、セキュリティが強化された Windows ファイアウォールからユーザーに通知を表示するかどうかを、ドメイン プロファイルに対して指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (ドメイン): プロファイル設定を使用する |セキュリティが強化された Windows ファイアウォールでドメイン プロファイルの設定を使用して、ネットワーク トラフィックをフィルター処理するかどうかを指定します。 [オフ] を選択すると、セキュリティが強化された Windows ファイアウォールによって、このプロファイルのファイアウォール規則も接続セキュリティ規則も使用されません。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (プライベート): ローカル接続のセキュリティ規則を適用する |プライベート プロファイルのグループ ポリシーによって構成される接続セキュリティ規則と一緒に適用される接続セキュリティ規則の作成を、ローカル管理者に許可するかどうかを指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (プライベート): ローカル ファイアウォールの規則を適用する |プライベート プロファイルのグループ ポリシーによって構成されるファイアウォール規則と一緒に適用されるローカル ファイアウォール規則の作成を、ローカル管理者に許可するかどうかを指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (プライベート): 送信接続の動作 |送信ファイアウォール規則と一致しないプライベート プロファイルの送信接続の動作を指定します。 既定値の 0 は接続を許可することを意味し、値 1 は接続をブロックすることを意味します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (プライベート): 通知を表示する |プログラムが受信接続の受信をブロックされたときに、セキュリティが強化された Windows ファイアウォールからユーザーに通知を表示するかどうかを、プライベート プロファイルに対して指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (プライベート): プロファイル設定を使用する |セキュリティが強化された Windows ファイアウォールでプライベート プロファイルの設定を使用して、ネットワーク トラフィックをフィルター処理するかどうかを指定します。 [オフ] を選択すると、セキュリティが強化された Windows ファイアウォールによって、このプロファイルのファイアウォール規則も接続セキュリティ規則も使用されません。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (パブリック): ローカル接続のセキュリティ規則を適用する |パブリック プロファイルのグループ ポリシーによって構成される接続セキュリティ規則と一緒に適用される接続セキュリティ規則の作成を、ローカル管理者に許可するかどうかを指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (パブリック): ローカル ファイアウォールの規則を適用する |パブリック プロファイルのグループ ポリシーによって構成されるファイアウォール規則と一緒に適用されるローカル ファイアウォール規則の作成を、ローカル管理者に許可するかどうかを指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (パブリック): 送信接続の動作 |送信ファイアウォール規則と一致しないパブリック プロファイルの送信接続の動作を指定します。 既定値の 0 は接続を許可することを意味し、値 1 は接続をブロックすることを意味します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (パブリック): 通知を表示する |プログラムが受信接続の受信をブロックされたときに、セキュリティが強化された Windows ファイアウォールからユーザーに通知を表示するかどうかを、パブリック プロファイルに対して指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール (パブリック): プロファイル設定を使用する |セキュリティが強化された Windows ファイアウォールでパブリック プロファイルの設定を使用して、ネットワーク トラフィックをフィルター処理するかどうかを指定します。 [オフ] を選択すると、セキュリティが強化された Windows ファイアウォールによって、このプロファイルのファイアウォール規則も接続セキュリティ規則も使用されません。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール: ドメイン: ユニキャスト応答の許可 |セキュリティが強化された Windows ファイアウォールで、ローカル コンピューターが発信マルチキャストまたはブロードキャスト メッセージに対してユニキャスト応答を受信できるようにするかどうかを、ドメイン プロファイルに対して指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール: プライベート: ユニキャスト応答の許可 |セキュリティが強化された Windows ファイアウォールで、ローカル コンピューターが発信マルチキャストまたはブロードキャスト メッセージに対してユニキャスト応答を受信できるようにするかどうかを、プライベート プロファイルに対して指定します。 |
|HITRUST/HIPAA コントロールを監査し、特定の VM 拡張機能をデプロイして監査要件をサポートする |Windows ファイアウォール: パブリック: ユニキャスト応答の許可 |セキュリティが強化された Windows ファイアウォールで、ローカル コンピューターが発信マルチキャストまたはブロードキャスト メッセージに対してユニキャスト応答を受信できるようにするかどうかを、パブリック プロファイルに対して指定します。 |

## <a name="next-steps"></a>次のステップ

ブループリントとその使用方法に関するその他の記事:

- [ブループリントのライフサイクル](../concepts/lifecycle.md)を参照する。
- [静的および動的パラメーター](../concepts/parameters.md)の使用方法を理解する。
- [ブループリントの優先順位](../concepts/sequencing-order.md)のカスタマイズを参照する。
- [ブループリントのリソース ロック](../concepts/resource-locking.md)の使用方法を調べる。
- [既存の割り当ての更新](../how-to/update-existing-assignments.md)方法を参照する。
