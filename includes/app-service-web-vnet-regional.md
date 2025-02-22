---
author: ccompy
ms.service: app-service-web
ms.topic: include
ms.date: 10/21/2020
ms.author: ccompy
ms.openlocfilehash: 399ce5e8714eb6935e3c2eac06ed44b712a14e35
ms.sourcegitcommit: 0046757af1da267fc2f0e88617c633524883795f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2021
ms.locfileid: "121741418"
---
リージョン VNet 統合を使用すると、アプリは次のものにアクセスできるようになります。

* アプリと同じリージョンにある VNet 内のリソース。
* VNet 内のリソースは、アプリが統合されている VNet とピアリングされます。
* サービス エンドポイントでセキュリティ保護されたサービス。
* Azure ExpressRoute 接続にまたがるリソース。
* 統合されている VNet 内のリソース。
* Azure ExpressRoute 接続を含む、ピアリングされた接続にまたがるリソース。
* プライベート エンドポイント 

同じリージョンの VNet との VNet 統合を使用する場合は、次の Azure ネットワーク機能を使用できます。

* **ネットワーク セキュリティ グループ (NSG)** :統合サブネットに配置された NSG を使って送信トラフィックをブロックできます。 VNet 統合を使ってアプリへの受信アクセスを提供できないため、受信規則は適用されません。
* **ルート テーブル (UDR)** :統合サブネット上にルート テーブルを配置して、必要な場所に送信トラフィックを送信できます。

既定では、アプリでは RFC1918 トラフィックのみが VNet にルーティングされます。 すべての送信トラフィックを VNet にルーティングする場合は、次の手順を使用して `WEBSITE_VNET_ROUTE_ALL` 設定をアプリに適用します。 

1. アプリ ポータルの **[構成]** UI にアクセスします。 **[新しいアプリケーション設定]** を選択します。
1. **[名前]** ボックスに「`WEBSITE_VNET_ROUTE_ALL`」、 **[値]** ボックスに「`1`」と入力します。

   ![アプリケーション設定を指定する][4]

1. **[OK]** を選択します。
1. **[保存]** を選択します。

> [!NOTE]
> すべての送信トラフィックを VNet にルーティングする場合は、統合サブネットに適用されている NSG と UDR に従います。 `WEBSITE_VNET_ROUTE_ALL`を `1` に設定した場合、トラフィックを他の場所に送信するルートを指定しない限り、パブリック IP アドレスへの送信トラフィックは、引き続きアプリのプロパティに一覧表示されているアドレスから送信されます。
> 
> リージョン VNet 統合では、ポート 25 を使用できません。

同じリージョンの VNet との VNet 統合を使用する場合、いくつかの制限があります。

* グローバル ピアリング接続にまたがるリソースには到達できません。
* この機能は、Premium V2 と Premium V3 のすべての App Service スケール ユニットから使用できます。 また、Standard でも使用できますが、新しい App Service のスケール ユニットからのみ利用できます。 以前のスケール ユニットを使用している場合は、Premium V2 App Service プランの機能のみを使用できます。 Standard App Service プランでこの機能を使用できるようにするには、Premium V3 App Service プランでアプリを作成します。 それらのプランは、最新のスケール ユニットでのみサポートされます。 その後、必要に応じてスケールダウンできます。  
* 統合サブネットは、1 つの App Service プランでしか使用できません。
* この機能は、App Service Environment にある Isolated プランのアプリでは使用できません。
* この機能には、Azure Resource Manager VNet 内に /28 以上の未使用のサブネットが必要です。
* アプリと VNet は同じリージョンに存在する必要があります。
* 統合アプリで VNet を削除することはできません。 VNet を削除する前に、統合を削除してください。
* App Service プランごとに 1 リージョンの VNet 統合のみを持つことができます。 同じ App Service プラン内の複数のアプリが同じ VNet を使用できます。
* リージョン VNet 統合を使用しているアプリがあるときに、アプリまたはプランのサブスクリプションを変更することはできません。
* アプリでは、構成を変更せずに Azure DNS Private Zones のアドレスを解決することはできません。

VNet 統合は、専用サブネットに依存します。 サブネットをプロビジョニングすると、Azure サブネットは先頭から 5 つの IP を失います。 プラン インスタンスごとに、統合サブネットから 1 つのアドレスが使用されます。 アプリを 4 つのインスタンスにスケールする場合は、4 つのアドレスが使用されます。 

サイズをスケールアップまたはスケールダウンすると、必要なアドレス空間が短期間に 2 倍になります。 これは、特定のサブネット サイズでサポートされる実際の使用可能なインスタンスに影響します。 次の表に、CIDR ブロックあたりの使用可能アドレスの最大数と、これが水平スケールに与える影響を示します。

| CIDR ブロック サイズ | 使用可能なアドレスの最大数 | 水平スケールの最大値 (インスタンス)<sup>*</sup> |
|-----------------|-------------------------|---------------------------------|
| /28             | 11                      | 5                               |
| /27             | 27                      | 13                              |
| /26             | 59                      | 29                              |

<sup>*</sup>ある時点でサイズまたは SKU のいずれかでスケールアップまたはスケールダウンする必要があることを前提としています。 

割り当てた後はサブネット サイズを変更できないため、アプリが到達する可能性のあるスケールに対応できるだけの十分な大きさを持つサブネットを使用してください。 サブネット容量に関する問題を回避するには、64 個のアドレスを持つ /26 を使用する必要があります。  

別のプラン内のご自身のアプリが、別のプラン内のアプリから既に接続されている VNet にアクセスできるようにしたい場合は、既存の VNet 統合によって使用されているものとは異なるサブネットを選択します。

この機能は、[カスタム コンテナー](../articles/app-service/quickstart-custom-container.md)を含め、Windows と Linux の両方のアプリで完全にサポートされています。 すべての動作は、Windows アプリと Linux アプリ間で同じです。

### <a name="service-endpoints"></a>サービス エンドポイント

リージョン VNet 統合を使用すると、サービス エンドポイントで保護されている Azure サービスに接続できます。 サービス エンドポイントで保護されたサービスにアクセスするには、次の操作を行う必要があります。

1. 統合のための特定のサブネットに接続するために、Web アプリとのリージョン VNet 統合を構成します。
1. 対象のサービスに移動し、統合サブネットに対してサービス エンドポイントを構成します。

### <a name="network-security-groups"></a>ネットワーク セキュリティ グループ

ネットワーク セキュリティ グループを使用して、VNet 内のリソースへの受信および送信トラフィックをブロックできます。 リージョン VNet 統合を使用するアプリでは、[ネットワーク セキュリティ グループ][VNETnsg]を使用して、VNet またはインターネット内のリソースへの送信トラフィックをブロックできます。 パブリック アドレスへのトラフィックをブロックするには、アプリケーション設定 `WEBSITE_VNET_ROUTE_ALL` を `1` に設定する必要があります。 VNet 統合はアプリからの送信トラフィックのみに影響を与えるため、NSG での受信規則はアプリに適用されません。

アプリへの受信トラフィックを制御するには、アクセス制限機能を使用します。 統合サブネットに適用される NSG は、統合サブネットに適用されているルートに関係なく有効になります。 `WEBSITE_VNET_ROUTE_ALL` が `1` に設定されていて、統合サブネット上でパブリック アドレス トラフィックに影響を与えるルートがない場合、すべての送信トラフィックは引き続き、統合サブネットに割り当てられた NSG に従います。 `WEBSITE_VNET_ROUTE_ALL` が設定されていない場合、NSG は RFC1918 トラフィックにのみ適用されます。

### <a name="routes"></a>ルート

ルート テーブルを使用して、アプリからの送信トラフィックを任意の場所にルーティングすることができます。 既定では、ルート テーブルは、RFC1918 の送信先トラフィックのみに影響を与えます。 `WEBSITE_VNET_ROUTE_ALL` を `1` に設定すると、すべての送信呼び出しが影響を受けます。 統合サブネット上に設定されているルートは、受信アプリ要求への応答には影響を与えません。 一般的な宛先には、ファイアウォール デバイスまたはゲートウェイを含めることができます。

オンプレミスのすべての送信トラフィックをルーティングする場合は、ルート テーブルを使用して、すべての送信トラフィックを ExpressRoute ゲートウェイに送信できます。 ゲートウェイにトラフィックをルーティングする場合は、外部ネットワークのルートを設定して、応答を返信するようにしてください。

また、Border Gateway Protocol (BGP) ルートも、アプリのトラフィックに影響を与えます。 ExpressRoute ゲートウェイのようなものから BGP ルートを使用している場合は、アプリの送信トラフィックが影響を受けます。 既定では、BGP ルートは、RFC1918 の送信先トラフィックにのみ影響を与えます。 `WEBSITE_VNET_ROUTE_ALL` が `1` に設定されている場合、すべての送信トラフィックは、BGP ルートの影響を受ける可能性があります。

### <a name="azure-dns-private-zones"></a>Azure DNS プライベート ゾーン 

アプリでは、VNet に統合された後、VNet が構成されているのと同じ DNS サーバーが使用されます。 既定では、アプリは Azure DNS プライベート ゾーンで動作しません。 Azure DNS プライベート ゾーンで動作させるには、次のアプリ設定を追加する必要があります。

1. `WEBSITE_DNS_SERVER` (値 `168.63.129.16`)
1. `WEBSITE_VNET_ROUTE_ALL` (値 `1`)

これらの設定により、アプリからのすべての送信呼び出しが VNet に送信され、アプリから Azure DNS プライベート ゾーンにアクセスできるようになります。 これらの設定を使用すると、アプリは、ワーカー レベルで DNS プライベート ゾーンを照会することによって、Azure DNS を使用できます。  

### <a name="private-endpoints"></a>プライベート エンドポイント

[プライベート エンドポイント][privateendpoints]を呼び出す場合は、DNS 参照がプライベート エンドポイントに解決されるようにする必要があります。 この動作は、次のいずれかの方法で実現できます。 

* Azure DNS プライベート ゾーンと統合する。 VNet にカスタム DNS サーバーがない場合、これは自動的に行われます。
* アプリで使用される DNS サーバーでプライベート エンドポイントを管理する。 これを行うには、プライベート エンドポイント アドレスを把握し、到達しようとしているエンドポイントが A レコードを使用してそのアドレスにポイントされるようにします。
* Azure DNS プライベート ゾーンに転送する独自の DNS サーバーを構成する。

<!--Image references-->
[4]: ../includes/media/web-sites-integrate-with-vnet/vnetint-appsetting.png

<!--Links-->
[VNETnsg]: /azure/virtual-network/security-overview/
[privateendpoints]: ../articles/app-service/networking/private-endpoint.md
