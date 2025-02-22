---
title: 業界の AI ソリューション
description: Azure Synapse Analytics の業界の AI ソリューション
services: synapse-analytics
ms.service: synapse-analytics
ms.subservice: machine-learning
ms.topic: overview
ms.reviewer: garye
ms.date: 11/02/2021
author: nelgson
ms.author: negust
ms.custom: ignite-fall-2021
ms.openlocfilehash: 0a4476b1324938acd2c753368f26bc7aafbed62b
ms.sourcegitcommit: 106f5c9fa5c6d3498dd1cfe63181a7ed4125ae6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2021
ms.locfileid: "131091215"
---
# <a name="industry-ai-solutions"></a>業界の AI ソリューション

どの業界にも、業界に固有の解決すべき一般的な問題があります。 この記事では、業界の一般的な問題の解決に迅速に取り組めるようにするために、Azure Synapse ワークスペースで利用可能な業界のソリューションについて説明します。 現時点では、提供される AI ソリューションは、製品レコメンデーションのための小売ソリューションです。 はじめに、このソリューションを小売業者として使用する方法の詳細を以下で確認できます。

## <a name="target-user"></a>ターゲット ユーザー

レコメンデーション ソリューションは、従来のデータ サイエンティストと、コードに慣れ、機械学習の概念に精通している新しいデータ サイエンティストを対象にしています。 このソリューションは、小売りドメインの特定の問題を解決するために、これらのユーザーの生産性を向上することを意図しています。

## <a name="retail-product-recommendation-solution"></a>小売製品のレコメンデーション ソリューション

**小売 - 製品のレコメンデーション** ソリューションは、堅牢でスケーラブルなレコメンデーション エンジンを提供し、追加設定なしで Synapse で開発することができます。 このソリューションを使用すると、製品のレコメンデーション向けの機械学習モデルをトレーニングする Notebook が提供されます。

独自のビジネス要件を確実に満たすようにするために、事前構成済みの Notebook をカスタマイズする必要がある場合があります。

この小売レコメンデーション ソリューションは、2 つの異なるモードでデプロイできます。 サンプル データで試してみるか、Synapse の小売用データベース テンプレートを使用してモデル化されたデータベースを使用できます。

**小売 - 製品のレコメンデーション** ソリューションでは、コンテンツベースのフィルター処理に関するレコメンデーションのパイプラインが提供されます。 コンテンツベースのフィルター処理パイプラインでは、LightGBM アルゴリズムを使用して、ユーザーと項目の特徴に基づいてユーザーの好みを予測するためのモデルをトレーニングします。 機能には、ユーザー プロファイルや項目プロファイルなどの静的な機能と、集計されたユーザー動作パターンなどの動的な機能があります。 コンテンツベースのフィルター処理の型指定されたレコメンデーション システムは、多くの場合、"パーソナライズされたおすすめ候補" や "おすすめの新製品" などのレコメンデーションに使用されます。

## <a name="get-started"></a>はじめに

1. Synapse ワークスペースを開きます
1. [ホーム] 画面の **[Discover more]\(その他を参照\)** セクションで、 **[Knowledge center]\(ナレッジ センター\)** を選択します。
1. [Knowledge center]\(ナレッジ センター\) で、 **[ギャラリーの参照]** を選択します。
1. ギャラリーで、 **[Database Templates]\(データベース テンプレート\)** タブを選択し、 **[AI solutions]\(AI ソリューション\)** セクションまで下にスクロールして、[Retail - Product recommendations]\(小売 - 製品のレコメンデーション\) ソリューションを選択します。 **[Continue]** をクリックします。
1. 次の 2 つのオプションから選択できます。
   * "サンプル データを使用する" 
   * "ワークスペース データベースから自分のデータを使用する" このオプションの例には、小売データベース テンプレートを使用してモデル化されたデータベースがあります。
   
    **[デプロイ]** をクリックすると、Synapse ワークスペースに Notebook が開きます。

1. これで、ワークスペースに Notebook が表示されます。 この Notebook を Spark プールにアタッチして、実際に使ってみることができます。 この Notebook は、特定のニーズに合わせてカスタマイズすることを意図している点に注意してください。

> [!NOTE]
> 独自のデータベースを選択する場合は、独自のテーブル名と列名を使用するために Notebook をカスタマイズする必要があります。

## <a name="next-steps"></a>次のステップ

* [Azure Synapse Analytics の使用を開始する](../get-started.md)
* [ワークスペースを作成する](../get-started-create-workspace.md)
