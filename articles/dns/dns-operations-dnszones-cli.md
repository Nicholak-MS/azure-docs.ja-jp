---
title: Azure DNS での DNS ゾーンの管理 - Azure CLI | Microsoft Docs
description: Azure CLI を使用して DNS ゾーンを管理できます。 この記事では、Azure DNS で DNS ゾーンを更新、削除、および作成する方法について説明します。
services: dns
documentationcenter: na
author: rohinkoul
ms.service: dns
ms.devlang: azurecli
ms.topic: how-to
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/28/2021
ms.author: rohink
ms.custom: devx-track-azurecli
ms.openlocfilehash: 871fa6456847655f4e75ddf8e145a2423715dd08
ms.sourcegitcommit: a5dd9799fa93c175b4644c9fe1509e9f97506cc6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2021
ms.locfileid: "108203345"
---
# <a name="how-to-manage-dns-zones-in-azure-dns-using-the-azure-cli"></a>Azure CLI を使用して Azure DNS で DNS ゾーンを管理する方法

> [!div class="op_single_selector"]
> * [ポータル](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI](dns-operations-dnszones-cli.md)


この記事では、クロス プラットフォームの Azure CLI を使用して、DNS ゾーンを管理する方法について説明します。 Azure CLI は、Windows、Mac、Linux に対応しています。 DNS ゾーンは、[Azure PowerShell](dns-operations-dnszones.md) または Azure Portal を使用して管理することもできます。

このガイドでは、特にパブリック DNS ゾーンについて説明します。 Azure CLI を使用した Azure DNS での Private Zones の管理については、[Azure CLI を使用した Azure DNS Private Zones での作業の開始](private-dns-getstarted-cli.md)に関するページを参照してください。

## <a name="introduction"></a>はじめに

[!INCLUDE [dns-create-zone-about](../../includes/dns-create-zone-about-include.md)]

## <a name="set-up-azure-cli-for-azure-dns"></a>Azure DNS 向け Azure CLI の設定

### <a name="before-you-begin"></a>始める前に

構成を開始する前に、以下がそろっていることを確認します。

* Azure サブスクリプション。 Azure サブスクリプションをまだお持ちでない場合は、[MSDN サブスクライバーの特典](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)を有効にするか、[無料アカウント](https://azure.microsoft.com/pricing/free-trial/)にサインアップしてください。

* Windows、Linux、または MAC 用の最新バージョンの Azure CLI をインストールしてください。 詳しくは、「 [Azure CLI のインストール](/cli/azure/install-az-cli2)」をご覧ください。

### <a name="sign-in-to-your-azure-account"></a>Azure アカウントへのサインイン

コンソール ウィンドウを開き、資格情報を使用して認証を行います。 詳細については、「[Azure CLI を使用して Azure にサインインする](/cli/azure/authenticate-azure-cli)」を参照してください

```
az login
```

### <a name="select-the-subscription"></a>サブスクリプションの選択

アカウントのサブスクリプションを確認します。

```
az account list
```

使用する Azure サブスクリプションを選択します。

```azurecli-interactive
az account set --subscription "subscription name"
```

### <a name="optional-to-installuse-azure-dns-private-zones-feature"></a>省略可能: Azure DNS Private Zones の機能のインストール/使用
Azure DNS Private Zone の機能は、Azure CLI の拡張機能を介して利用できます。 "dns" Azure CLI 拡張機能をインストールしてください。 

```
az extension add --name dns
``` 

### <a name="create-a-resource-group"></a>リソース グループを作成する

Azure Resource Manager では、リソース グループの場所を指定する必要があります。 この場所は、そのリソース グループ内のすべてのリソースの既定の保存先として使用されます。 すべての DNS リソースはグローバルであるため、リソース グループの場所の選択は Azure DNS には影響しません。

既存のリソース グループを使用する場合は、この手順をスキップしてかまいません。

```azurecli-interactive
az group create --name myresourcegroup --location "West US"
```

## <a name="getting-help"></a>ヘルプの表示

Azure DNS に関連するすべての Azure CLI コマンドは `az network dns` で始まります。 `--help` オプション (短縮形 `-h`) を使用すると、各コマンドのヘルプを利用できます。  次に例を示します。

```azurecli-interactive
az network dns --help
az network dns zone --help
az network dns zone create --help
```

## <a name="create-a-dns-zone"></a>DNS ゾーンの作成

DNS ゾーンは、`az network dns zone create` コマンドを使用して作成します。 `az network dns zone create -h` を使用すると、ヘルプが表示されます。

次の例では、*MyResourceGroup* というリソース グループに *contoso.com* という DNS ゾーンを作成します。

```azurecli-interactive
az network dns zone create --resource-group MyResourceGroup --name contoso.com
```

### <a name="to-create-a-dns-zone-with-tags"></a>タグのある DNS ゾーンを作成するには

次の例では、`--tags` パラメーター (短縮形 `-t`) を使用して、*project = demo* と *env = test* の 2 つ [Azure Resource Manager タグ](dns-zones-records.md#tags)を含む DNS ゾーンを作成する方法を示します。

```azurecli-interactive
az network dns zone create --resource-group MyResourceGroup --name contoso.com --tags "project=demo" "env=test"
```

## <a name="get-a-dns-zone"></a>DNS ゾーンの取得

DNS ゾーンを取得するには、 `az network dns zone show`を使用します。 `az network dns zone show --help` を使用すると、ヘルプが表示されます。

次の例では、リソース グループ *MyResourceGroup* から DNS ゾーン *contoso.com* とその関連データを返します。 

```azurecli-interactive
az network dns zone show --resource-group myresourcegroup --name contoso.com
```

次の例は応答です。

```json
{
  "etag": "00000002-0000-0000-3d4d-64aa3689d201",
  "id": "/subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com",
  "location": "global",
  "maxNumberOfRecordSets": 5000,
  "name": "contoso.com",
  "nameServers": [
    "ns1-04.azure-dns.com.",
    "ns2-04.azure-dns.net.",
    "ns3-04.azure-dns.org.",
    "ns4-04.azure-dns.info."
  ],
  "numberOfRecordSets": 4,
  "resourceGroup": "myresourcegroup",
  "tags": {},
  "type": "Microsoft.Network/dnszones"
}
```

DNS レコードを一覧表示するには、`az network dns record-set list` を使用します。

## <a name="list-dns-zones"></a>DNS ゾーンの一覧表示

DNS ゾーンを列挙するには、`az network dns zone list` を使用します。 `az network dns zone list --help` を使用すると、ヘルプが表示されます。

リソース グループを指定すると、リソース グループ内のゾーンのみが一覧表示されます。

```azurecli-interactive
az network dns zone list --resource-group MyResourceGroup
```

リソース グループを省略すると、サブスクリプション内のすべてのゾーンが一覧表示されます。

```azurecli-interactive
az network dns zone list 
```

## <a name="update-a-dns-zone"></a>DNS ゾーンの更新

DNS ゾーンのリソースへの変更は、 `az network dns zone update`を使用して行うことができます。 `az network dns zone update --help` を使用すると、ヘルプが表示されます。

このコマンドによって、ゾーン内の DNS レコード セットが更新されることはありません (「 [DNS レコードの管理方法](dns-operations-recordsets-cli.md)」を参照)。 この操作は、ゾーンのリソース自体のプロパティを更新するためだけに使用します。 現時点では、これらのプロパティは、ゾーンのリソースの [Azure Resource Manager の"タグ"](dns-zones-records.md#tags) に限定されています。

次の例では、DNS ゾーンのタグを更新する方法を示します。 既存のタグは、指定された値に置き換えられます。

```azurecli-interactive
az network dns zone update --resource-group myresourcegroup --name contoso.com --set tags.team=support
```

## <a name="delete-a-dns-zone"></a>DNS ゾーンの削除

DNS ゾーンは、`az network dns zone delete` を使用して削除できます。 `az network dns zone delete --help` を使用すると、ヘルプが表示されます。

> [!NOTE]
> DNS ゾーンを削除すると、ゾーン内の DNS レコードもすべて削除されます。 この操作を元に戻すことはできません。 DNS ゾーンを使用している場合、ゾーンを削除すると、ゾーンを使用するサービスは機能しなくなります。
>
>ゾーンを誤って削除しないようにするには、「[DNS ゾーンとレコードを保護する](dns-protect-zones-recordsets.md)」をご覧ください。

このコマンドは、確認を求めるプロンプトを表示します。 オプションの `--yes` スイッチはこのプロンプトを表示しません。

次の例は、リソース グループ *MyResourceGroup* から *contoso.com* ゾーンを削除する方法を示します。

```azurecli-interactive
az network dns zone delete --resource-group myresourcegroup --name contoso.com
```

## <a name="next-steps"></a>次のステップ

DNS ゾーンでレコード セットとレコードを管理する方法については[こちら](./dns-getstarted-cli.md)をご覧ください。

Azure DNS にドメインを委任する方法については[こちら](dns-domain-delegation.md)をご覧ください。
