---
title: Azure Key Vault のコンテナーを別のリソース グループに移動する | Microsoft Docs
description: キー コンテナーを別のリソース グループに移動するためのガイダンス。
services: key-vault
author: msmbaldwin
tags: azure-resource-manager
ms.service: key-vault
ms.subservice: general
ms.topic: how-to
ms.date: 03/31/2021
ms.author: mbaldwin
ms.openlocfilehash: 508a6aebe581df1c4fcaa634bdcb1d870f319f84
ms.sourcegitcommit: 0ede6bcb140fe805daa75d4b5bdd2c0ee040ef4d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2021
ms.locfileid: "122606208"
---
# <a name="moving-an-azure-key-vault-across-resource-groups"></a>リソース グループ間での Azure Key Vault の移動

## <a name="overview"></a>概要

リソース グループ間でのキー コンテナーの移動は、サポートされているキー コンテナー機能です。 リソース グループ間でキー コンテナーを移動しても、キー コンテナーのファイアウォールまたはアクセス ポリシーの構成には影響しません。 接続されているアプリケーションとサービス プリンシパルは、意図したとおりに動作し続けるはずです。

> [!IMPORTANT]
> **ディスクの暗号化に使用されているキー コンテナーは移動できません。**
> VM のディスク暗号化でキー コンテナーを使用している場合、ディスク暗号化が有効になっている間、キー コンテナーを別のリソース グループまたはサブスクリプションに移動することはできません。 キー コンテナーを新しいリソース グループまたはサブスクリプションに移動する前に、ディスクの暗号化を無効にする必要があります。 

## <a name="design-considerations"></a>デザインに関する考慮事項

組織は、リソース グループ レベルでの適用または除外を使用して Azure Policy を実装している可能性があります。 キー コンテナーが現在存在しているリソース グループと、キー コンテナーの移動先のリソース グループには、異なるポリシー割り当てのセットが存在する場合があります。 ポリシー要件の競合により、アプリケーションが中断される可能性があります。

### <a name="example"></a>例

2 年間有効な証明書を作成するキー コンテナーに接続されているアプリケーションがあるとします。 キー コンテナーの移動先のリソース グループには、1 年より長い期間有効な証明書の作成をブロックするポリシー割り当てがあります。 キー コンテナーを新しいリソース グループに移動すると、2 年間有効な証明書を作成する操作は、Azure Policy の割り当てによってブロックされます。

### <a name="solution"></a>解決策

Azure portal の Azure Policy ページにアクセスし、現在のリソース グループと移動先のリソース グループのポリシー割り当てを調べて、不一致がないことを確認します。

## <a name="procedure"></a>手順

1. Azure Portal にログインする
2. お使いのキー コンテナーに移動する
3. [概要] タブをクリックする
4. [移動] ボタンを選択する
5. ドロップダウン リストのオプションから [別のリソース グループに移動する] を選択する
6. キー コンテナーの移動先のリソース グループを選択する
7. リソースの移動に関する警告を確認する
8. [OK] を選択する

Key Vault によって、リソースの移動の有効性が評価され、エラーがあればアラートが通知されます。 エラーが見つからない場合は、リソースの移動が完了します。 
