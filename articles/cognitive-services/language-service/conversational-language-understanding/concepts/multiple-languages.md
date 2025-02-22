---
title: 多言語プロジェクト
titleSuffix: Azure Cognitive Services
description: 多言語プロジェクトを使用する方法については、「会話言語の理解」を参照してください。
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: text-analytics
ms.topic: conceptual
ms.date: 11/02/2021
ms.author: aahi
ms.custom: ignite-fall-2021
ms.openlocfilehash: 4bbad9e51e26d643ff121e9b80b5da3fbafd89b9
ms.sourcegitcommit: 106f5c9fa5c6d3498dd1cfe63181a7ed4125ae6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2021
ms.locfileid: "131091330"
---
# <a name="multilingual-projects"></a>多言語プロジェクト

会話言語を理解すると、一度に複数の言語にプロジェクトを簡単に拡張できます。 プロジェクトで複数の言語を有効にすると、言語固有の発話とシノニムをプロジェクトに追加し、インテントとエンティティの多言語予測を取得できるようになります。 

## <a name="multilingual-intent-and-learned-entity-components"></a>多言語の目的と学習済みのエンティティ コンポーネント

プロジェクトで複数の言語を有効にすると、プロジェクトを主に 1つの言語でトレーニングし、その後すぐに他の言語で予測を取得できます。 

たとえば、英語の発話を使用してプロジェクト全体をトレーニングし、フランス語、ドイツ語、標準中国語、日本語、韓国語などでクエリを実行できます。 会話言語の理解により、多言語テクノロジを使用してモデルをトレーニングすることで、プロジェクトを複数の言語に簡単に拡張できます。

特定の言語が他の言語と同じように実行されていないことを確認するたびに、その言語の発話をプロジェクトに追加できます。 Language Studio の [[タグ発話]](../how-to/tag-utterances.md) ページで、追加する発話の言語を選択できます。 その言語の例をモデルに導入すると、その言語のより多くの構文を学び、より良い予測をするようになります。

すべての言語で同じ量の発話を追加することは求められていません。 プロジェクトの大部分は 1 つの言語でビルドする必要があります。また、あまりうまく実行されていないと考える言語では、いくつかの発話のみを追加するようにします。 主に英語であるプロジェクトを作成し、フランス語、ドイツ語、およびスペイン語でのテストを開始した場合、ドイツ語が他の 2 つの言語と同様に実行されないことがわかります。 その場合は、元の英語の例の 5% をドイツ語で追加し、新しいモデルをトレーニングし、ドイツ語でもう一度テストを行うことを検討してください。 ドイツ語のクエリで、より良い結果が得られます。 追加する発話が多いほど、結果が改善される可能性が高くなります。 

別の言語でデータを追加することで他の言語に悪影響を及ぼすことはないはずです。 

## <a name="list-and-prebuilt-components-in-multiple-languages"></a>複数の言語でのコンポーネントの一覧と事前構築

複数の言語が有効になっているプロジェクトでは、すべてのリスト キーに対して **言語ごと** にシノニムを指定できます。 プロジェクトに対してクエリを実行する言語によっては、その言語のシノニムを持つリスト コンポーネントの一致のみが取得されます。 プロジェクトに対してクエリを実行するときに、要求本文に言語を指定できます。

```json
"query": "{query}"
"language": "{language code}"
```

言語を指定しない場合は、プロジェクトの既定の言語にフォールバックします。 さまざまな言語コードの一覧については、 [言語サポート](../language-support.md)の記事を参照してください。

あらかじめ構築されたコンポーネントは似ており、特定の言語で使用できる事前構築済みのコンポーネントの予測を取得することが想定されます。 要求の言語によって、どのコンポーネントの予測が試行されるかも決まります。 事前に構築された各コンポーネントの言語サポートについては、「[構築済みのコンポーネント](../prebuilt-component-reference.md)」の関連記事を参照してください。

## <a name="next-steps"></a>次のステップ

* [発話にタグ付けする](../how-to/tag-utterances.md) 
* [モデルをトレーニングする](../how-to/train-model.md)
