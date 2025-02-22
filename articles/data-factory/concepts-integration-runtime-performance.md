---
title: Integration Runtime のパフォーマンス
titleSuffix: Azure Data Factory & Azure Synapse
description: Azure Data Factory および Azure Synapse Analytics で、Azure Integration Runtime のパフォーマンスを最適化および改善する方法について説明します。
author: kromerm
ms.topic: conceptual
ms.author: makromer
ms.service: data-factory
ms.subservice: data-flows
ms.custom: synapse
ms.date: 09/09/2021
ms.openlocfilehash: 13f632da70944d7c1aec00df112782429dc9620e
ms.sourcegitcommit: 0770a7d91278043a83ccc597af25934854605e8b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/13/2021
ms.locfileid: "124787909"
---
# <a name="optimizing-performance-of-the-azure-integration-runtime"></a>Azure Integration Runtime のパフォーマンスの最適化

データ フローは、実行時にスピンアップされる Spark クラスター上で実行されます。 使用されるクラスターの構成は、アクティビティの統合ランタイム (IR) 内に定義されます。 統合ランタイムを定義する際は、クラスターの種類、クラスターのサイズ、Time to Live という 3 つのパフォーマンスに関する考慮事項があります。

Integration Runtime の作成方法の詳細については、[Integration Runtime](concepts-integration-runtime.md) に関する記事を参照してください。

## <a name="cluster-type"></a>クラスターの種類

選択できる Spark クラスターのスピンアップの種類には、汎用、メモリ最適化、コンピューティング最適化の 3 つのオプションがあります。

**汎用** クラスターは既定で選択されており、ほとんどのデータ フロー ワークロードに適しています。 パフォーマンスとコストのバランスが最適になる傾向があります。

データ フローに多数の結合と参照が含まれている場合は、**メモリ最適化** クラスターを使用することをお勧めします。 メモリ最適化クラスターでは、より多くのデータをメモリに格納できるため、メモリ不足のエラーを最小限に抑えることができます。 メモリ最適化は、コアあたりの価格ポイントが最も高いだけでなく、より満足のいくパイプラインになる傾向もあります。 データ フローの実行時にメモリ不足エラーが発生する場合は、メモリ最適化 Azure IR 構成に切り替えます。 

**コンピューティング最適化** は、ETL ワークフローには適しておらず、ほとんどの運用ワークロードには推奨されません。 データをフィルター処理したり、派生列を追加したりするなど、メモリを多用しない簡単なデータ変換の場合は、コアあたりの価格が低めのコンピューティング最適化クラスターを使用できます。

## <a name="cluster-size"></a>クラスター サイズ

データ フローでは、データ処理を Spark クラスター内の異なる複数のノードに分散して、操作を並列で実行します。 コア数が多い Spark クラスターでは、コンピューティング環境のノード数が増加します。 ノードが増えると、データ フローの処理能力が向上します。 多くの場合、クラスターのサイズを増やすことは、処理時間を短縮するための簡単な方法です。

既定のクラスター サイズは、4 つのドライバー ノードと 4 つのワーカー ノードです。  より多くのデータを処理する場合は、より大きなクラスターを使用することをお勧めします。 可能なサイズ変更オプションは次のとおりです。

| ワーカー コア | ドライバー コア | コア総数 | Notes |
| ------------ | ------------ | ----------- | ----- |
| 4 | 4 | 8 | コンピューティング最適化には使用できません |
| 8 | 8 | 16 | |
| 16 | 16 | 32 | |
| 32 | 16 | 48 | |
| 64 | 16 | 80 | |
| 128 | 16 | 144 | |
| 256 | 16 | 272 | |

データ フローは仮想コア時間で課金されます。つまり、クラスターのサイズと実行時間の両方が考慮されます。 スケールアップすると、1 分あたりのクラスター コストが増加しますが、全体的な時間は減少します。

> [!TIP]
> クラスターのサイズがデータ フローのパフォーマンスに与える影響には上限があります。 データのサイズによっては、クラスターのサイズを大きくしてもパフォーマンスが向上しなくなるポイントがあります。 たとえば、データのパーティション数よりも多くのノードがある場合、ノードを追加しても役に立ちません。 ベスト プラクティスとして、小規模に開始し、パフォーマンスのニーズに合わせてスケールアップすることをお勧めします。 

## <a name="time-to-live"></a>Time to Live

既定では、すべてのデータ フロー アクティビティにより、Azure IR 構成に基づいて新しい Spark クラスターがスピンアップされます。 コールド クラスターの起動にかかる時間は数分で、それが完了するまではデータ処理を開始できません。 パイプラインに複数の **シーケンシャル** データ フローが含まれている場合は、Time to Live (TTL) 値を有効にすることができます。 Time to Live 値を指定すると、クラスターは実行が完了してから一定の期間、有効な状態に維持されます。 TTL 時間内に IR を使用する新しいジョブを開始すると、既存のクラスターが再利用され、開始時間は大幅に減少します。 2 番目のジョブが完了すると、クラスターは TTL 時間の間、再び有効な状態で維持されます。

[Data Flow Properties]\(データ フロー プロパティ\) で Azure Integration Runtime の [クイック再利用] オプションを設定することで、ウォーム クラスターの起動時間をさらに最小限に抑えることができます。 これを true に設定すると、サービスは各ジョブの後に既存のクラスターを破棄せず、既存のクラスターを再利用するように指示されます。これにより、Azure IR に設定したコンピューティング環境が、TTL で指定した時間まで基本的に存続することになります。 このオプションを使用すると、パイプラインから実行される場合に、データ フロー アクティビティの起動時間が最短になります。

ただし、データ フローの大部分が並列で実行される場合は、それらのアクティビティに使用する IR の TTL を有効にしないことをお勧めします。 1 つのクラスターで一度に実行できるジョブは 1 つだけです。 使用可能なクラスターがあり、2 つのデータ フローが開始されている場合は、その 1 つだけにライブ クラスターが使用されます。 2 番目のジョブで、それ専用の分離クラスターがスピンアップされます。

> [!NOTE]
> 自動解決統合ランタイムを使用する場合、Time to Live は使用できません

## <a name="next-steps"></a>次のステップ

パフォーマンスに関する Data Flow のその他の記事を参照してください。

- [Data Flow のパフォーマンス](concepts-data-flow-performance.md)
- [Data Flow のアクティビティ](control-flow-execute-data-flow-activity.md)
- [データ フローのパフォーマンスの監視](concepts-data-flow-monitoring.md)
