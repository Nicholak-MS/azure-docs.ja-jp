---
title: インクルード ファイル
description: インクルード ファイル
services: storage
author: roygara
ms.service: storage
ms.topic: include
ms.date: 08/28/2020
ms.author: rogarana
ms.custom: include file
ms.openlocfilehash: a5fd0394feb8b58688bd163d62af30b031125b46
ms.sourcegitcommit: 3de22db010c5efa9e11cffd44a3715723c36696a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2021
ms.locfileid: "109663902"
---
Azure Files では、Premium、トランザクション最適化、ホット、クールの 4 つの異なるストレージのサービス レベルが提供されており、お客様のシナリオのパフォーマンスと価格の要件に合わせて共有を調整できます。

- **Premium**:Premium ファイル共有は、ソリッド ステート ドライブ (SSD) によってサポートされており、IO 集中型ワークロードで一貫した優れたパフォーマンスと待機時間 (ほとんどの IO 操作で 1 桁のミリ秒以内の低待機時間) を提供します。 Premium ファイル共有は、データベース、Web サイトのホスティング、開発環境など、幅広い種類のワークロードに適しています。 Premium ファイル共有は、サーバー メッセージ ブロック (SMB) プロトコルとネットワーク ファイル システム (NFS) プロトコルの両方で使用できます。
- **トランザクション最適化**:トランザクション最適化ファイル共有は、Premium ファイル共有が提供する待機時間を必要としない、トランザクション負荷の高いワークロードを可能にします。 トランザクション最適化ファイル共有は、ハード ディスク ドライブ (HDD) によってサポートされている標準ストレージ ハードウェアで提供されます。 トランザクション最適化は、従来は "Standard" と呼ばれていましたが、これはサービス レベル自体ではなく、ストレージ メディアの種類を指しています (ホットおよびクールも、標準ストレージ ハードウェア上にあるため、"Standard" サービス レベルです)。
- **Hot**:ホット ファイル共有は、チーム共有などの汎用ファイル共有シナリオに最適化されたストレージを提供します。 ホット ファイル共有は、HDD によってサポートされている標準ストレージ ハードウェアで提供されます。
- **Cool**:クール ファイル共有は、オンライン アーカイブ ストレージのシナリオ向けに最適化された、コスト効率に優れたストレージを提供します。 クール ファイル共有は、HDD によってサポートされている標準ストレージ ハードウェアで提供されます。

Premium ファイル共有は、**FileStorage ストレージ アカウント** の種類でデプロイされ、プロビジョニング済み課金モデルでのみ利用できます。 Premium ファイル共有のプロビジョニング済み課金モデルについて詳しくは、「[Premium ファイル共有のプロビジョニングについて](../articles/storage/files/understanding-billing.md#provisioned-model)」をご覧ください。 トランザクション最適化、ホット、クール ファイル共有などの Standard ファイル共有は、**汎用バージョン 2 (GPv2) ストレージ アカウント** の種類でデプロイされ、従量課金制で利用できます。 

ワークロードのストレージ層を選択する場合は、パフォーマンスと使用量の要件を考慮してください。 ワークロードに 1 桁の待機時間が必要な場合、またはオンプレミスの SSD ストレージ メディアを使用している場合は、おそらく Premium 層が最適です。 チーム共有が Azure からオンプレミスにマウントされている場合または Azure File Sync を使用してオンプレミスにキャッシュされている場合など、低待機時間が特に問題ではない場合は、コストの観点から、標準ストレージの方が適している可能性があります。

ファイル共有をストレージ アカウントで作成すると、異なるストレージ アカウントの種類に固有の層に移動させることはできません。 たとえば、トランザクション最適化ファイル共有を Premium 層に移動する場合、FileStorage ストレージ アカウントで新しいファイル共有を作成し、データを元の共有から FileStorage アカウント内の新しいファイル共有にコピーする必要があります。 AzCopy を使用して Azure ファイル共有間でデータをコピーすることをお勧めしますが、Windows の `robocopy` または macOS と Linux 用の `rsync` などのツールを使用することもできます。 

GPv2 ストレージ アカウント内にデプロイされたファイル共有は、新しいストレージ アカウントを作成してデータを移行することなく、Standard 層 (トランザクション最適化、ホット、クール) 間で移動できますが、層を変更するとトランザクション コストが発生します。 共有をホットな層からクールな層に移動すると、共有内の各ファイルについてクールな層の書き込みトランザクション料金が発生します。 ファイル共有をクールな層からホットな層に移動すると、共有内の各ファイルについてクールな層の読み込みトランザクション料金が発生します。

詳細については、「[Azure Files の課金について](../articles/storage/files/understanding-billing.md)」をご覧ください。