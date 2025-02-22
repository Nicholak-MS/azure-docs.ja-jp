---
title: Azure アプリケーション オファーのテストと発行
description: プレビューする Azure アプリケーション オファーを送信し、オファーをプレビューしてテストしてから、Azure Marketplace に公開します。
author: aarathin
ms.author: aarathin
ms.reviewer: dannyevers
ms.service: marketplace
ms.subservice: partnercenter-marketplace-publisher
ms.topic: how-to
ms.date: 09/27/2021
ms.openlocfilehash: d7606595adb5c0d20b348bbe323d27af64e8d9cb
ms.sourcegitcommit: 10029520c69258ad4be29146ffc139ae62ccddc7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2021
ms.locfileid: "129082101"
---
# <a name="test-and-publish-an-azure-application-offer"></a>Azure アプリケーション オファーのテストと発行

この記事では、パートナー センターを使用して公開する Azure アプリケーション オファーを送信し、オファーをプレビューしてテストしてから、コマーシャル マーケットプレースにライブで公開する方法について説明します。 公開するプランを既に作成しておく必要があります。

## <a name="submit-the-offer-for-publishing"></a>公開するオファーを送信する

#### <a name="workspaces-view"></a>[ワークスペース ビュー](#tab/workspaces-view)

1. [パートナー センター](https://partner.microsoft.com/dashboard/home)にサインインします。

1. ホーム ページで、 **[Marketplace offers]\(Marketplace のオファー\)** タイルを選択します。

    [ ![パートナー センターのホーム ページにある [Marketplace offers]\(Marketplace のオファー\) タイルを示しています。](./media/workspaces/partner-center-home.png) ](./media/workspaces/partner-center-home.png#lightbox)

1. [Marketplace offers]\(Marketplace のオファー\) ページで、公開するオファーを選択します。
1. ポータルの右上隅で、 **[レビューと公開]** を選択します。
1. 各ページの **[状態]** 列に **[完了]** と表示されていることを確認します。 次の 3 つの状態のいずれかが表示されます。
    - **[未開始]** – ページが不完全です。
    - **[不完全]** – ページに必要な情報がないか、修正が必要なエラーがあります。 ページに戻って更新する必要があります。
    - **[完了]** – ページが完了しました。 必須のデータはすべて入力済みであり、エラーはありません。
1. いずれかのページの状態が **[完了]** 以外である場合は、ページ名を選択し、問題を修正してページを保存してから、 **[レビューと公開]** をもう一度選択して、このページに戻ります。
1. すべてのページが完了したら、アプリが確実に正しくテストされるよう、 **[認定の注意書き]** ボックスに認定チームに向けたテストの指示を入力します。 アプリの理解に役立つ補足事項を提供します。
1. オファーを公開するプロセスを開始するには、 **[公開]** を選択します。 **[オファーの概要]** ページが表示され、オファーの **公開ステータス** が示されます。

#### <a name="current-view"></a>[現在のビュー](#tab/current-view)

1. [パートナー センター](https://partner.microsoft.com/dashboard/commercial-marketplace/overview)のコマーシャル マーケットプレースにサインインします。
1. **[概要]** ページで、発行するオファーを選択します。
1. ポータルの右上隅で、 **[レビューと公開]** を選択します。
1. 各ページの **[状態]** 列に **[完了]** と表示されていることを確認します。 次の 3 つの状態のいずれかが表示されます。
    - **[未開始]** – ページが不完全です。
    - **[不完全]** – ページに必要な情報がないか、修正が必要なエラーがあります。 ページに戻って更新する必要があります。
    - **[完了]** – ページが完了しました。 必須のデータはすべて入力済みであり、エラーはありません。
1. いずれかのページの状態が **[完了]** 以外である場合は、ページ名を選択し、問題を修正してページを保存してから、 **[レビューと公開]** をもう一度選択して、このページに戻ります。
1. すべてのページが完了したら、アプリが確実に正しくテストされるよう、 **[認定の注意書き]** ボックスに認定チームに向けたテストの指示を入力します。 アプリの理解に役立つ補足事項を提供します。
1. オファーを公開するプロセスを開始するには、 **[公開]** を選択します。 **[オファーの概要]** ページが表示され、オファーの **公開ステータス** が示されます。

---

オファーの公開ステータスは、公開プロセスを移動すると変更されます。 このプロセスの詳細については、「[検証と公開の手順](review-publish-offer.md#validation-and-publishing-steps)」を参照してください。

## <a name="preview-and-test-the-offer"></a>オファーをプレビューしてテストする

オファーをサインオフする準備ができたら、オファーのプレビューを確認して承認するように求めるメールが送信されます。 お使いのブラウザーの **[オファーの概要]** ページを更新し、自分のオファーが発行元のサインオフ フェーズに達したかどうかを確認することもできます。 そうなっている場合は、 **[公開]** ボタンとプレビュー リンクが使用可能になります。 Microsoft からプランを販売することを選択した場合、プレビュー対象ユーザーに追加されたユーザーは、この段階で確実に要件を満たすために、プランの取得とデプロイをテストすることができます。

次のスクリーンショットは、 **[公開]** ボタンの下に 2 つのプレビュー リンクがあるオファーの **[オファーの概要]** ページを示しています。 このページに表示される検証手順は、オファーの作成時に選択した内容によって異なります。

[![パートナー センターに表示されるオファーの [オファーの概要] ページを示しています。[公開] ボタンとプレビュー リンクが表示されています。](media/create-new-azure-app-offer/azure-app-publish-status.png)](media/create-new-azure-app-offer/azure-app-publish-status.png#lightbox)

オファーをプレビューする手順は次のとおりです。

1. **[オファーの概要]** ページで、 **[公開]** ボタンの下にあるプレビュー リンクを選択します。 
1. 購入と設定のフローを徹底的に検証するには、自分のオファーがプレビュー段階にある間にそれを購入してください。 まず、課金を処理しないよう、[サポート チケット](https://aka.ms/marketplacesupport)で Microsoft に通知します。
1. Azure アプリケーションが[コマーシャル マーケットプレースの測定サービスを使用した従量制課金](marketplace-metering-service-apis.md)をサポートしている場合は、「[マーケットプレースの従量制課金 API](marketplace-metering-service-apis.md#development-and-testing-best-practices)」で詳しく説明されているテストのベスト プラクティスを確認し、それに従ってください。
1. オファーをプレビューしてテストした後に変更を加える必要がある場合は、オファーを編集して再送信すれば、新しいプレビューを公開できます。 詳細については、「[Commercial Marketplace で既存のオファーを更新する](./update-existing-offer.md)」を参照してください。

## <a name="publish-your-offer-live"></a>オファーを発行する

プレビューですべてのテストが完了したら、 **[公開]** を選択して、オファーをコマーシャル マーケットプレースに公開します。

   > [!TIP]
   > オファーが既にマーケットプレースで公開されている場合は、更新しても、 **[公開]** を選択するまで公開されません。

コマーシャル マーケットプレースでオファーを使用できるように選択したら、一連の最終的な検証チェックが行われ、そのライブのオファーの構成がプレビュー バージョンのオファーと同等に構成されていることが確認されます。 これらの検証チェックの詳細については、「[公開フェーズ](review-publish-offer.md#publish-phase)」を参照してください。

これらの検証チェックが完了すると、自分のオファーはマーケットプレースに公開されます。

### <a name="errors-and-review-feedback"></a>エラーとフィードバックの確認

発行プロセスの **手動検証** の手順には、オファーの広範なレビューとそれに関連する技術資産 (特に Azure Resource Manager テンプレート) が含まれるため、通常、問題は pull request (PR) のリンクとして示されます。 これらの PR を表示してそれに対応する方法については、「[レビュー フィードバックの処理](azure-app-review-feedback.md)」をご覧ください。

1 つまたは複数の公開手順でエラーが発生した場合は、それらを修正してからオファーを再公開してください。

## <a name="next-step"></a>次のステップ

- [コマーシャル マーケットプレース向け分析レポートにアクセスする](analytics.md)
- **Microsoft との共同販売**、および **CSP プログラムを通じた再販** によって、[Azure アプリケーション オファーを販売](azure-app-marketing.md)します。
