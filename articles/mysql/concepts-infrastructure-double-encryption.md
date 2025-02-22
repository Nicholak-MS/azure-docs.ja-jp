---
title: インフラストラクチャの二重暗号化 - Azure Database for MySQL
description: インフラストラクチャの二重暗号化を使用して、サービス マネージド キーで 2 番目の暗号化レイヤーを追加する方法について説明します。
author: mksuni
ms.author: sumuth
ms.service: mysql
ms.topic: conceptual
ms.date: 6/30/2020
ms.openlocfilehash: 9b6d87c3bfabf3884d9a90966994eea002a45dd8
ms.sourcegitcommit: 98e126b0948e6971bd1d0ace1b31c3a4d6e71703
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2021
ms.locfileid: "114674437"
---
# <a name="azure-database-for-mysql-infrastructure-double-encryption"></a>Azure Database for MySQL のインフラストラクチャの二重暗号化

[!INCLUDE[applies-to-mysql-single-server](includes/applies-to-mysql-single-server.md)]

Azure Database for MySQL は、Microsoft のマネージド キーを使用してデータに対して[保存データのストレージ暗号化](concepts-security.md#at-rest)を使用します。 バックアップを含むデータはディスク上で暗号化され、この暗号化は常に有効であり、無効にすることはできません。 暗号化について、Azure のストレージ暗号化に FIPS 140-2 検証済み暗号化モジュールと AES 256 ビット暗号化が使用されます。

インフラストラクチャの二重暗号化は、サービス マネージド キーで 2 番目の暗号化レイヤーを追加します。 FIPS 140-2 の検証された暗号化モジュールを使用しますが、暗号化アルゴリズムは異なります。 これにより、保存データの保護レイヤーが追加されます。 インフラストラクチャの二重暗号化に使用されるキーは、Azure Database for MySQL サービスによっても管理されます。 インフラストラクチャの二重暗号化は、追加の暗号化レイヤーがパフォーマンスに影響を与える可能性があるため、既定では有効になっていません。

> [!NOTE]
> 保存データの暗号化と同様に、この機能は、General Purpose および Memory Optimized 価格レベルで使用できる "汎用ストレージ v2 (最大 16 TB をサポート)" ストレージでのみサポートされます。 詳細については、[ストレージの概念](concepts-pricing-tiers.md#storage)に関するページを参照してください。 その他の制限事項については、「[制限事項](concepts-infrastructure-double-encryption.md#limitations)」セクションを参照してください。

インフラストラクチャ レイヤーの暗号化には、ストレージ デバイスまたはネットワーク ワイヤに最も近いレイヤーに実装する利点があります。 Azure Database for MySQL は、サービス マネージド キーを使用して、2 つの暗号化レイヤーを実装します。 厳密にはサービス レイヤーにあっても、保存データが格納されているハードウェアに非常に近いものです。 必要に応じて、プロビジョニングされた MySQL サーバーの[ユーザーのマネージド キー](concepts-data-encryption-mysql.md)を使用して、保存データの暗号化を有効にすることもできます。 

インフラストラクチャ レイヤーでの実装では、キーの多様性もサポートされます。 インフラストラクチャは、コンピューターとネットワークのさまざまなクラスターを認識している必要があります。 それにより、さまざまなキーを使用すると、インフラストラクチャ攻撃の影響範囲とさまざまなハードウェアおよびネットワーク障害を最小限に抑えることができます。 

> [!NOTE]
> インフラストラクチャの二重暗号化を使用すると、追加の暗号化プロセスによって Azure Database for MySQL サーバーのスループットに 5-10% の影響があります。

## <a name="benefits"></a>メリット

Azure Database for MySQL のインフラストラクチャの二重暗号化には、次の利点があります。

1. **さらに多様性が増した暗号化実装** - ハードウェア ベースの暗号化への計画的な移行により、ソフトウェア ベースの実装に加えて、ハードウェア ベースの実装が提供されるため、実装がさらに多様化します。
2. **実装エラー** - インフラストラクチャ レイヤーでの 2 つの暗号化レイヤーにより、プレーンテキスト データを公開する上位層でのキャッシュまたはメモリ管理のエラーから保護されます。 また、この 2 つのレイヤーは、一般に暗号化の実装のエラーに対しても保証します。

これらの組み合わせにより、暗号に対する攻撃に使用される一般的な脅威や弱点に対する強力な保護が提供されます。

## <a name="supported-scenarios-with-infrastructure-double-encryption"></a>インフラストラクチャの二重暗号化でサポートされるシナリオ

Azure Database for MySQL によって提供される暗号化機能を一緒に使用することもできます。 使用できるさまざまなシナリオの概要を次に示します。

|  ##   | 既定の暗号化 | インフラストラクチャの二重暗号化 | カスタマー マネージド キーを使用したデータ暗号化  |
|:------|:------------------:|:--------------------------------:|:--------------------------------------------:|
| 1     | *はい*              | *いいえ*                             | *いいえ*                                         |
| 2     | *はい*              | *はい*                            | *いいえ*                                         |
| 3     | *はい*              | *いいえ*                             | *はい*                                        |
| 4     | *はい*              | *はい*                            | *はい*                                        |
|       |                    |                                  |                                              |

> [!Important]
> - シナリオ 2 と 4 では、インフラストラクチャの暗号化のレイヤーが追加されるため、Azure Database for MySQL サーバーのワークロードの種類に基づき、5～10% のスループットの低下を招く可能性があります。
> - Azure Database for MySQL のインフラストラクチャの二重暗号化の構成は、サーバーの作成時にのみ許可されます。 一度サーバーがプロビジョニングされると、ストレージ暗号化を変更することはできません。 ただし、インフラストラクチャの二重暗号化を使用して作成されたサーバーもそうでないサーバーも、カスタマー マネージド キーを使用してデータの暗号化を有効にすることもできます。

## <a name="limitations"></a>制限事項

Azure Database for MySQL の場合、インフラストラクチャの二重暗号化のサポートには、次のようないくつかの制限があります。

* この機能のサポートは、**General Purpose** および **Memory Optimized** 価格レベルに限定されています。
* この機能は、汎用ストレージ v2 (最大 16 TB) をサポートしているリージョンとサーバーでのみサポートされています。 最大 16 TB のストレージをサポートする Azure リージョンの一覧については、[こちら](concepts-pricing-tiers.md#storage)のドキュメントにあるストレージのセクションを参照してください

    > [!NOTE]
    > - 汎用ストレージ v2 をサポートしている [Azure リージョン](concepts-pricing-tiers.md#storage)で作成されたすべての新しい MySQL サーバーで、カスタマー マネージド キーによる暗号化のサポートを **利用できます**。 ポイント イン タイム リストア (PITR) サーバーまたは読み取りレプリカは、理論上 ' 新規 ' には該当しません。
    > - プロビジョニングされたサーバーによって汎用ストレージ v2 がサポートされているかどうかを検証するには、ポータルの [価格レベル] ブレードにアクセスして、プロビジョニング済みのサーバーでサポートされる最大ストレージ サイズを確認します。 スライダーを最大 4 TB まで動かすことができる場合、お使いのサーバーは汎用ストレージ v1 上にあり、カスタマー マネージド キーを使用した暗号化はサポートされません。 ただし、データは常にサービス マネージド キーを使用して暗号化されます。 質問がある場合は、AskAzureDBforMySQL@service.microsoft.com までご連絡ください。



## <a name="next-steps"></a>次のステップ

[Azure Database for MySQL のインフラストラクチャの二重暗号化を設定する](howto-double-encryption.md)方法について説明します。
