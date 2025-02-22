---
title: インクルード ファイル
description: インクルード ファイル
services: cosmos-db
author: SnehaGunda
ms.service: cosmos-db
ms.topic: include
ms.date: 07/02/2021
ms.author: sngun
ms.custom: include file
ms.openlocfilehash: 2f055d8fe6608d328421e1916c5855d300c49dcc
ms.sourcegitcommit: 0046757af1da267fc2f0e88617c633524883795f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2021
ms.locfileid: "121725487"
---
1. 新しいブラウザー ウィンドウで、[Azure Portal](https://portal.azure.com/) にサインインします。

2. 左側のメニューで、 **[リソースの作成]** を選択します。
   
   :::image type="content" source="./media/cosmos-db-create-dbaccount-graph/create-nosql-db-databases-json-tutorial-0.png" alt-text="Azure portal でリソースを作成する":::   

3. **[新規]** ページで、 **[データベース]**  >  **[Azure Cosmos DB]** の順に選択します。

   :::image type="content" source="./media/cosmos-db-create-dbaccount-graph/create-nosql-db-databases-json-tutorial-1.png" alt-text="Azure portal の [データベース] ウィンドウ":::      

3. **[Azure Cosmos DB アカウントの作成]** ページで、新しい Azure Cosmos DB アカウントの設定を入力します。 
 
   |設定|値|説明 |
   |---|---|---|
   |サブスクリプション|サブスクリプション名|この Azure Cosmos アカウントに使用する Azure サブスクリプションを選択します。 |
   |リソース グループ|リソース グループ名|リソース グループを選択するか、 **[新規作成]** を選択し、新しいリソース グループの一意の名前を入力します。 |
   |アカウント名|一意の名前を入力します|自分の Azure Cosmos DB アカウントを識別するための一意の名前を入力します。 アカウント URI は、一意のアカウント名に *gremlin.azure.com* が追加されたものになります。<br><br>アカウント名に使用できるのは、小文字、数字、ハイフン (-) のみで、長さは 3 文字から 44 文字の範囲にする必要があります。|
   API|Gremlin (グラフ)|API によって、作成するアカウントの種類が決まります。 Azure Cosmos DB には、5 種類の API が用意されています。ドキュメント データベース用の Core (SQL)、グラフ データベース用の Gremlin、ドキュメント データベース用の MongoDB、Azure Table、Cassandra です。 API ごとに別のアカウントを作成する必要があります。 <br><br>このクイックスタートでは Gremlin API に対応するテーブルを作成するので、**Gremlin (グラフ)** を選択します。 <br><br>[Gremlin API に関する詳細を参照してください](../graph-introduction.md)。|
   |場所|ユーザーに最も近いリージョン|Azure Cosmos DB アカウントをホストする地理的な場所を選択します。 データに最も高速にアクセスできるよう、お客様のユーザーに最も近い場所を使用します。|
   |容量モード|プロビジョニング スループットまたはサーバーレス|[プロビジョニング スループット](../set-throughput.md) モードでアカウントを作成するには、 **[Provisioned throughput]\(プロビジョニング スループット\)** を選択します。 [サーバーレス](../serverless.md) モードでアカウントを作成するには、 **[サーバーレス]** を選択します。|
   |Apply Azure Cosmos DB free tier discount (Azure Cosmos DB Free レベル割引を適用する)|**[適用]** または **[適用しない]**|Azure Cosmos DB Free レベルのアカウントでは、最初の 1000 RU/s と 25 GB のストレージを無料でご利用いただけます。 [Free レベル](https://azure.microsoft.com/pricing/details/cosmos-db/)の詳細を確認してください。|

   > [!NOTE]
   > Azure サブスクリプションにつき所有できる Free レベルの Azure Cosmos DB アカウントは 1 つまでです。また、アカウントの作成時にオプトインする必要があります。 Free レベルの割引を適用するオプションが表示されない場合は、サブスクリプション内の別のアカウントが Free レベルで既に有効になっていることを意味します。

   :::image type="content" source="./media/cosmos-db-create-dbaccount-graph/azure-cosmos-db-create-new-account.png" alt-text="Azure Cosmos DB の新しいアカウント ページ":::   

1. **[グローバル分散]** タブで、次の詳細を構成します。 このクイックスタートでは、既定値のままでかまいません。

   |設定|値|説明 |
   |---|---|---|
   |geo 冗長性|無効化|リージョンをペア リージョンとペアリングすることによる、アカウントでのグローバル配信を有効または無効にします。 アカウントには、後でさらにリージョンを追加できます。|
   |マルチリージョン書き込み|無効化|マルチリージョン書き込み機能を使用すると、世界中のデータベースとコンテナーで、プロビジョニングされたスループットを利用できます。|

   > [!NOTE]
   > **[Capacity mode]\(容量モード\)** として **[サーバーレス]** を選択した場合、以下のオプションは利用できません。
   > - Apply Free Tier Discount (Free レベルの割引の適用)
   > - geo 冗長
   > - マルチリージョン ライター

1. 必要に応じて、次のタブで追加の詳細を構成できます。

   * **[ネットワーク]** - [仮想ネットワークからのアクセス](../how-to-configure-vnet-service-endpoint.md)を構成します。
   * **[バックアップ ポリシー]** - [定期的](../configure-periodic-backup-restore.md)または [継続的](../provision-account-continuous-backup.md)のいずれかのバックアップ ポリシーを構成します。
   * **[暗号化]** - サービス マネージド キーまたは [カスタマー マネージド キー](../how-to-setup-cmk.md#create-a-new-azure-cosmos-account)のいずれかを使用します。
   * **[タグ]** - タグは名前と値のペアで、同じタグを複数のリソースやリソース グループに適用することでリソースを分類したり、統合した請求を表示したりできるようにします。

1. **[Review + create]\(レビュー + 作成\)** を選択します。

1. アカウントの作成には数分かかります。 ポータルに "**Azure Cosmos DB アカウントが作成されました** ページが表示されます。

   :::image type="content" source="./media/cosmos-db-create-dbaccount-graph/azure-cosmos-db-graph-created.png" alt-text="[Azure Cosmos DB アカウントが作成されました] ページ":::   