---
title: Azure VMware Solution (AVS) に移行する VMware サーバーを Azure Migrate で評価する
description: AVS に移行する VMware 環境のサーバーを Azure Migrate で評価する方法について説明します。
author: rashi-ms
ms.author: rajosh
ms.manager: abhemraj
ms.topic: tutorial
ms.date: 09/14/2020
ms.custom: MVC
ms.openlocfilehash: a2637fbfcaf1e30b1df9f0739630ea2883eba3fa
ms.sourcegitcommit: 611b35ce0f667913105ab82b23aab05a67e89fb7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/14/2021
ms.locfileid: "129994208"
---
# <a name="tutorial-assess-vmware-servers-for-migration-to-avs"></a>チュートリアル: AVS への移行のために VMware サーバーを評価する

Azure への移行に取り組む過程では、オンプレミスのワークロードを評価し、クラウドへの対応性を測り、リスクを明らかにして、コストと複雑さを見積もります。

この記事では、Azure VMware Solution (AVS) への移行に備えて、検出した VMware 仮想マシンとサーバーを Azure Migrate を使用して評価する方法について説明します。 AVS は、VMware プラットフォームを Azure で実行することができるマネージド サービスです。

このチュートリアルでは、以下の内容を学習します。
> [!div class="checklist"]
- サーバーのメタデータと構成情報に基づいて評価を実行する。
- パフォーマンス データに基づいて評価を実行する。

> [!NOTE]
> チュートリアルでは、シナリオを試すための最も簡単な方法を説明し、可能な限り既定のオプションを使用します。 

Azure サブスクリプションをお持ちでない場合は、開始する前に [無料アカウント](https://azure.microsoft.com/pricing/free-trial/) を作成してください。



## <a name="prerequisites"></a>前提条件

このチュートリアルに従って AVS への移行についてサーバーを評価する前に、必ず評価対象のサーバーを検出しておきます。

- Azure Migrate アプライアンスを使用してサーバーを検出する場合は、[こちらのチュートリアルに従います](tutorial-discover-vmware.md)。 
- インポートした CSV ファイルを使用してサーバーを検出する場合は、[こちら](tutorial-discover-import.md)のチュートリアルに従ってください。


## <a name="decide-which-assessment-to-run"></a>実行する評価を決定する


評価を実行する際に使用するサイズ設定基準のベースを、現状のオンプレミスで収集されたサーバー構成データおよびメタデータにするか、動的パフォーマンス データにするかを決定します。

**評価** | **詳細** | **推奨**
--- | --- | ---
**現状のオンプレミス** | サーバー構成データおよびメタデータに基づいて評価します。  | AVS の推奨ノード サイズは、オンプレミスの VM およびサーバーのサイズに加え、ノード タイプ、ストレージの種類、許容するエラーの設定に関して評価に指定した設定に基づきます。
**パフォーマンスベース** | 収集された動的パフォーマンス データに基づいて評価します。 | AVS の推奨ノード サイズは、CPU とメモリの使用率データに加え、ノード タイプ、ストレージの種類、許容するエラーの設定に関して評価に指定した設定に基づきます。

> [!NOTE]
> Azure VMware Solution (AVS) 評価は、VMware VM とサーバーに対してのみ作成できます。

## <a name="run-an-assessment"></a>評価を実行する

評価を実行するには次のようにします。

1.  **[概要]** ページの **[Windows, Linux and SQL Server]\(Windows、Linux、SQL Server\)** で、 **[サーバーの評価と移行]** をクリックします。
    :::image type="content" source="./media/tutorial-assess-sql/assess-migrate.png" alt-text="Azure Migrate の [概要] ページ":::

1. **[Azure Migrate: Discovery and assessment]\(Azure Migrate: 検出および評価\)** で、 **[評価]** をクリックします。

   ![[評価] ボタンの場所](./media/tutorial-assess-vmware-azure-vmware-solution/assess.png)

1. **[サーバーの評価]**  >  **[評価の種類]** で、 **[Azure VMware Solution (AVS)]** を選択します。

1. **[検出ソース]** で次の操作を行います。

    - アプライアンスを使用してサーバーを検出した場合、 **[Azure Migrate アプライアンスから検出されたサーバー]** を選択します。
    - インポートした CSV ファイルを使用してサーバーを検出した場合、 **[Imported servers]\(インポートされたサーバー\)** を選択します。 
    
1. **[編集]** をクリックして、評価のプロパティを確認します。

    :::image type="content" source="./media/tutorial-assess-vmware-azure-vmware-solution/assess-servers.png" alt-text="評価の設定を選択するためのページ":::
 

1. **[評価のプロパティ]**  >  **[ターゲット プロパティ]** で:

    - 移行先となる Azure リージョンを **[ターゲットの場所]** で指定します。
       - サイズとコストは、指定した場所に基づいて推奨されます。
   - **[ストレージの種類]** は、既定で **[vSAN]** に設定されています。 AVS プライベート クラウドでは、これが既定のストレージの種類となります。
   - AVS ノードでは現在、**予約インスタンス** はサポートされません。
1. **[VM サイズ]** では:
    - **[ノードの種類]** は、既定で **[AV36]** に設定されています。 サーバーを AVS に移行する必要のあるノードが Azure Migrate によって推奨されます。
    - **[FTT 設定、RAID レベル]** で、許容するエラーと RAID の組み合わせを選択します。  選択した FTT オプションとオンプレミスのサーバー ディスク要件を組み合わせて、AVS で必要とされる vSAN ストレージの合計が決定されます。
    - **[CPU Oversubscription]\(CPU オーバーサブスクリプション\)** で、AVS ノードの 1 つの物理コアに関連付けられる仮想コアの比率を指定します。 オーバーサブスクリプションが 4 対 1 を上回る場合、パフォーマンスが低下する可能性がありますが、Web サーバー タイプのワークロードには使用できます。
    - **[Memory overcommit factor]\(メモリのオーバーコミット率\)** に、クラスター上のメモリのオーバーコミットの比率を指定します。 値 1 は 100% のメモリ使用量、0.5 は 50%、2 は使用可能なメモリの 200% を使用していることを表します。 0\.5 から 10 までの、最大で小数点以下 1 桁の値のみ追加できます。
    - **[Dedupe and compression factor]\(重複排除と圧縮率\)** で、ワークロードで予想される重複排除と圧縮率を指定します。 実際の値は、オンプレミスの vSAN またはストレージ構成から取得できます。これは、ワークロードによって異なる場合があります。 値 3 は 3 倍を意味し、300 GB のディスクでは 100 GB のストレージのみが使用されます。 値 1 は、重複排除も圧縮もないことを意味します。 1 から 10 までの、最大で小数点以下 1 桁の値のみを追加できます。
1. **[ノード サイズ]** で、次の操作を行います。 
    - **[サイズ変更の設定基準]** で、静的メタデータを評価の基準にするか、パフォーマンスベースのデータを評価の基準にするかを選択します。 パフォーマンス データを使用する場合:
        - 評価の基準とするデータ期間を **[パフォーマンス履歴]** で指定します。
        - パフォーマンス サンプルに使用するパーセンタイル値を **[百分位の使用率]** で指定します。 
    - 評価中に使用したいバッファーを **[快適性係数]** で指定します。 ここでは、季節ごとの使用量、短期間のパフォーマンス履歴、将来に使用量が増える可能性などの問題が考慮されます。 たとえば、快適性係数を 2 とした場合、
    
        **コンポーネント** | **有効使用率** | **快適性係数の追加 (2.0)**
        --- | --- | ---
        コア | 2  | 4
        メモリ | 8 GB | 16 GB  

1. **[価格]** では:
    - **[プラン]** には、登録されている [Azure プラン](https://azure.microsoft.com/support/legal/offer-details/)が表示されます。 評価によって、そのプランのコストが見積もられます。
    - 自分のアカウントの請求通貨を **[通貨]** で選択します。
    - Azure プランとは別に適用されるサブスクリプション固有の割引を **[割引 (%)]** に追加します。 既定の設定は 0% です。

1. 変更内容を確定する場合は **[保存]** をクリックします。

    :::image type="content" source="./media/tutorial-assess-vmware-azure-vmware-solution/avs-view-all.png" alt-text="評価のプロパティ":::

1. **[サーバーの評価]** で **[次へ]** をクリックします。

1. **[評価するサーバーの選択]**  >  **[評価名]** で、評価の名前を指定します。 
 
1. **[グループの選択または作成]** で **[新規作成]** を選択し、グループ名を指定します。 
    
    :::image type="content" source="./media/tutorial-assess-vmware-azure-vmware-solution/assess-group.png" alt-text="グループにサーバーを追加する":::
 
1. アプライアンスを選択し、グループに追加するサーバーを選択します。 続けて、 **[次へ]** をクリックします。

1. **[評価の確認と作成]** で評価の詳細を確認したら、 **[評価の作成]** をクリックしてグループを作成し、評価を実行します。

    > [!NOTE]
    > パフォーマンスベースの評価の場合は、検出の開始後、少なくとも 1 日経ってから評価を作成することをお勧めします。 これにより、パフォーマンス データを収集する時間が確保され、信頼度が上がります。 高い信頼度レーティングを得るためには、検出の開始後、指定したパフォーマンス期間 (日、週、月) を置くのが理想です。

## <a name="review-an-assessment"></a>評価を確認する

AVS の評価には以下が記述されています。

- **Azure VMware Solution (AVS) 対応性**: オンプレミスのサーバーが Azure VMware Solution (AVS) への移行に適しているかどうか。
- **Azure VMware Solution ノードの数**: サーバーを実行するために必要な Azure VMware Solution ノードの推定数。
- **すべての AVS ノードの使用率**: すべてのノードにおける CPU、メモリ、および記憶域の使用率の予測。
    - 使用率では、vCenter Server、NSX Manager (大規模)、NSX Edge など、クラスター管理オーバーヘッドが事前に考慮されます。HCX がデプロイされている場合は、HCX Manager と IX アプライアンスによる消費 (圧縮と重複除去の前の最大 44vCPU (11 CPU)、75 GB の RAM、722 GB のストレージ) も考慮されます。
    - 制限要因により、リソースに対応するために必要なホストとノードの数が決まります。
- **月間コスト見積もり**: オンプレミスの VM を実行しているすべての Azure VMware Solution (AVS) ノードの月間推定コスト。

## <a name="view-an-assessment"></a>評価を表示する

評価を表示するには:

1. **[Windows, Linux and SQL Server]\(Windows、Linux、SQL Server\)**  >  **[Azure Migrate: Discovery and assessment]\(Azure Migrate: 検出および評価\)** で、**[Azure VMware Solution]** の横にある数字をクリックします。

1. **[評価]** で、評価を選択して開きます。 以下はその例です (見積もりとコストはあくまで例です)。 

    :::image type="content" source="./media/tutorial-assess-vmware-azure-vmware-solution/avs-assessment-summary.png" alt-text="AVS 評価の概要":::

1. 評価の概要を確認します。 **[Sizing assumptions]\(サイズ決定の前提\)** をクリックすると、ノードのサイズ設定とリソース使用率の計算で使用された前提を確認できます。 評価のプロパティを編集して、評価を再計算することもできます。
 

### <a name="review-readiness"></a>対応性を確認する

1. **[Azure 対応性]** をクリックします。
2. **[Azure 対応性]** で、対応性の状態を確認します。

    - **[AVS 対応]** : サーバーを変更せずにそのまま Azure AVS に移行できます。 サーバーを AVS で起動し、AVS のフル サポートを受けます。
    - **[条件付きで対応]** : サーバーは、最新の vSphere バージョンとの互換性に問題がある可能性があります。 AVS で完全に動作するためには、VMware ツールのインストールなどの設定が必要となる可能性があります。
    - **[AVS に未対応]** :VM は、AVS では起動しません。 たとえば、オンプレミスの VMware サーバーに外部デバイス (CD-ROM など) を装着している場合に、VMware VMotion を使用すると VMotion の操作に失敗します。
 - **[対応性が不明]** : オンプレミス環境から収集したメタデータが不十分なために、Azure Migrate がサーバーの対応性を判断できませんでした。

3. 推奨されるツールを確認します。

    - VMware HCX または Enterprise: VMware サーバーの場合、オンプレミスのワークロードを Azure VMware Solution (AVS) プライベート クラウドに移行するために推奨される移行ツールは、VMware Hybrid Cloud Extension (HCX) ソリューションです。 詳細については、ここをクリックしてください。
    - 不明: CSV ファイルを介してインポートされたサーバーの場合、既定の移行ツールは不明です。 VMware サーバーの場合は、VMware Hybrid Cloud Extension (HCX) ソリューションを使用することをお勧めします。
4. [AVS 対応性] の状態をクリックします。 サーバー対応性の詳細を表示し、ドリルダウンしてサーバーの詳細 (コンピューティング、ストレージ、ネットワークの設定など) を表示できます。

### <a name="review-cost-estimates"></a>コスト見積もりを確認する

評価の概要には、Azure でサーバーを実行する場合のコンピューティングとストレージのコストの見積もりが表示されます。 

1. 月間合計コストを確認します。 評価対象のグループ内のすべてのサーバーのコストが集計されます。

    - コストの見積もりは、すべてのサーバーのリソース要件全体を考慮した場合に必要な AVS ノードの数に基づいて算出されます。
    - AVS の価格はノードごとであるため、総コストではコンピューティング コストとストレージ コストは配分されません。
    - コストの見積もりは、オンプレミスのサーバーを AVS で実行した場合の見積もりです。 AVS 評価では、PaaS や SaaS のコストは考慮されません。

2. 月間ストレージの見積もりを確認します。 このビューには、評価されたグループの集計されたストレージ コストが、ストレージ ディスクの種類ごとに分けて表示されます。 
3. ドリルダウンすることで、特定のサーバーについてコストの詳細を確認できます。

### <a name="review-confidence-rating"></a>信頼度レーティングを確認する

パフォーマンスベースの評価には、Server Assessment によって信頼度レーティングが割り当てられます。 レーティングの範囲は、星 1 つ (最も低い) から星 5 つ (最も高い) までです。

信頼度レーティングを使うと、評価の推奨サイズの信頼性を見積もることができます。 このレーティングは、評価の計算に必要なデータ ポイントの有効性に基づいています。

> [!NOTE]
> CSV ファイルに基づいて評価を作成した場合、信頼度レーティングは割り当てられません。

信頼度レーティングは次のとおりです。

**データ ポイントの可用性** | **信頼度レーティング**
--- | ---
0% - 20% | 1 つ星
21% - 40% | 2 つ星
41% - 60% | 3 つ星
61% - 80% | 4 つ星
81% - 100% | 5 つ星

信頼度レーティングについての[詳しい情報](concepts-assessment-calculation.md#confidence-ratings-performance-based)をご覧ください。

## <a name="next-steps"></a>次の手順

- [依存関係マッピング](concepts-dependency-visualization.md)を使用してサーバーの依存関係を明らかにします。
- [エージェントレス](how-to-create-group-machine-dependencies-agentless.md)または[エージェントベース](how-to-create-group-machine-dependencies.md)の依存関係マップを設定します。
