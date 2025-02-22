---
title: Azure エンタープライズ転送
description: Azure EA 転送について説明します
author: bandersmsft
ms.reviewer: baolcsva
ms.service: cost-management-billing
ms.subservice: enterprise
ms.topic: conceptual
ms.date: 08/02/2021
ms.author: banders
ms.custom: contperf-fy21q1
ms.openlocfilehash: cc8d65ec4b714bbb98036c5ed3deabd4b75d3c98
ms.sourcegitcommit: 0046757af1da267fc2f0e88617c633524883795f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/13/2021
ms.locfileid: "121751985"
---
# <a name="azure-enterprise-transfers"></a>Azure エンタープライズ転送

この記事では、エンタープライズ転送の概要について説明します。

## <a name="transfer-an-enterprise-account-to-a-new-enrollment"></a>エンタープライズ アカウントを新しい登録に転送する

アカウントの転送によって、アカウント オーナーが現在の加入契約から別の加入契約に移動されます。 アカウント オーナーの関連サブスクリプションはすべて、転送先の加入契約に移動されます。 アカウントの転送は、複数のアクティブな加入契約があり、選択したアカウント オーナーのみを移動する場合に使用します。

このセクションは情報提供のみを目的としています。エンタープライズ管理者がアクションを実行することはできません。 エンタープライズ アカウントを新しい加入契約に転送するためにはサポート リクエストが必要となります。

エンタープライズ アカウントを新しい登録に転送する場合は、次の点に注意してください。

- 要求で指定されたアカウントのみが転送されます。 すべてのアカウントが選択されている場合、すべてが転送されます。
- 元の加入契約の状態は、アクティブまたは延長として保持されます。 有効期限が切れるまでは、この登録を使用し続けることができます。

### <a name="prerequisites"></a>前提条件

アカウントの転送を要求する場合は、次の情報を指定します。

- 転送するアカウントの転送先加入契約の数、アカウント名、アカウント オーナーの電子メール
- 元の登録については、転送元の登録番号とアカウント

アカウントの転送前に注意するべきその他の点は、次のとおりです。

- 元の登録と対象の登録の両方で、EA 管理者からの承認が必要です
- アカウントの転送要件が満たさない場合は、登録の転送を検討してください。
- アカウントの移行では、特定のアカウントに関連したすべてのサービスとサブスクリプションが移行されます。
- 転送が完了すると、転送済みアカウントは、転送元の加入契約では非アクティブとして表示され、転送先の加入契約ではアクティブとして表示されます。
- アカウントが示す終了日は、移行元の登録における移行の実施日に対応し、移行先の登録では開始日として表示されます。
- 転送の実施日前にアカウントに関して生じた使用量については、すべてが元の加入契約下に残されます。

## <a name="transfer-enterprise-enrollment-to-a-new-one"></a>エンタープライズ登録を新しいエンタープライズ登録に転送する

次の場合に、加入契約の転送を検討します。

- 現在の加入契約の前払い期間が終了した。
- 加入契約の期限が切れているか、延長されており、新しい契約の交渉が行われている。
- 複数の加入契約があり、すべてのアカウントと課金を 1 つの加入契約にまとめたい。

このセクションは情報提供のみを目的としています。エンタープライズ管理者がアクションを実行することはできません。 エンタープライズ加入契約を新しい加入契約に転送するためにはサポート リクエストが必要となります ([加入契約の自動転送](#auto-enrollment-transfer)の資格を満たしている場合を除く)。

エンタープライズ登録全体を別の登録に転送するよう要求すると、次の操作が行われます。

- 使用量の転送は、新しい加入契約に反映されるまでに最大 72 時間かかることがあります。
- 転送された加入契約で DA または AO ビュー料金が有効になっている場合は、新しい加入契約で有効にする必要があります。
- API レポートまたは Power BI を使用している場合は、新しい加入契約で新しい API キーを生成してください。
- すべての EA 部署管理者を含め、すべての Azure サービス、サブスクリプション、アカウント、部署、加入契約の構造全体が、転送先の新しい加入契約に転送されます。
- 登録の状態は "_転送済み_" に設定されます。 転送済み登録は、過去の使用状況レポートを作成する目的にのみ使用できます。
- 転送済みの登録には、ロールやサブスクリプションを追加することができません。 転送済みの状態では、加入契約に対して使用量を追加することができません。
- 契約に残っている Azure 前払い残高は、将来の期間を含めて失われます。
-    転送元の加入契約で RI が購入されている場合、RI の購入料金は元の加入契約に残りますが、すべての RI の特典は、新しい加入契約で使用できるように転送されます。
-    Marketplace での 1 回限りの購入料金と、以前の加入契約で既に発生した月額固定料金は、新しい加入契約には転送されません。 Marketplace の従量課金制の料金は転送されます。

### <a name="effective-transfer-date"></a>有効な転送日

有効な転送日には、転送先の加入契約の開始日以降の日付を指定できます。

元の登録の使用量は、Azure 前払いまたは超過分に対して課金されます。 有効な転送日以降に発生した使用量は、新しい加入契約に転送され、課金されます。

### <a name="prerequisites"></a>前提条件

登録の転送を要求する場合は、次の情報を指定します。

- 転送元の加入契約については、加入契約番号。
- 対象の登録については、転送先の登録番号。
- 登録の転送の有効日には、対象の登録の開始日以降の日付を指定できます。 選択した日付は、既に発行されている超過分の請求書の使用量に影響を与えません。

登録の転送前に注意するべきその他の点は、次のとおりです。

- 転送元の加入契約と転送先の加入契約の両方について、EA 管理者からの承認が必要です。
- 登録の転送要件が満たさない場合は、アカウントの転送を検討してください。
- 転送元の加入契約の状態は転送済みに更新され、過去の使用状況レポートを作成する目的にのみ使用できます。
- 加入契約の転送中にダウンタイムは発生しません。
- 使用状況がターゲットの加入契約で反映されるまでに、最大 24 から 48 時間かかる場合があります。
- 部署管理者またはアカウント所有者のコスト ビュー設定は引き継がれません。
  - 以前に有効だった場合には、転送先の加入契約で設定を有効にする必要があります。
- 転送元の加入契約で使用されているすべての API キーは、転送先の加入契約のために再生成する必要があります。
- 転送元と転送先の加入契約が異なるクラウド インスタンスにある場合、転送は失敗します。 Azure サポートは、同じクラウド インスタンス内でのみ転送できます。
- 予約 (予約インスタンス):
  - 異なる通貨間の加入契約またはアカウントの転送は、毎月の予約購入に影響します。
  - 加入契約の転送中または転送後に通貨が変化すると、月単位の予約購入は、転送元の加入契約でキャンセルされます。 これは意図的なもので、月単位の予約購入にのみ影響します。
  - 場合によっては、ローカルまたは新しい通貨で、新しい加入契約を使用し、キャンセルされた月単位の予約を転送元の加入契約から再購入する必要があります。


### <a name="auto-enrollment-transfer"></a>加入契約の自動転送

加入契約の転送をリクエストするサポート チケットを提出したことがない場合でも、加入契約の状態が **[転送済み]** と表示されることがあります。 **[転送済み]** 状態は、加入契約の自動転送プロセスから生じます。 加入契約の自動転送プロセスが更新段階で実行されるためには、新しい契約にいくつかの項目が追加されている必要があります。

- 以前の加入契約番号 (EA Portal にあります)
- 以前の加入契約番号の有効期限が、新しい契約の有効期限開始日の 1 日前であること
- 新しい契約に、現在の日付またはそれよりも前の日付が付された請求済みの Azure 前払い注文があること
- 新しい加入契約が EA Portal で作成されていること

以前の加入契約と新しい加入契約との間で不足している使用量データが EA Portal になければ、転送のサポート チケットを作成する必要はありません。

### <a name="azure-prepayment"></a>Azure 前払い

Azure 前払いは、登録間で転送を行うことはできません。 Azure 前払いの残高は、契約によって、順序指定された登録に関連付けられています。 アカウントまたは登録の転送プロセスの一環として、Azure 前払いは転送されません。

### <a name="no-services-affected-for-account-and-enrollment-transfers"></a>アカウントおよび加入契約の転送の影響を受けるサービスはありません

アカウントまたは加入契約の転送中にダウンタイムは発生しません。 必要な情報がすべて指定されている場合は、要求どおりの日に完了できます。

## <a name="transfer-an-enterprise-subscription-to-a-pay-as-you-go-subscription"></a>エンタープライズ サブスクリプションを従量課金制サブスクリプションに譲渡する

従量課金制料金の個々のサブスクリプションにエンタープライズ サブスクリプションを譲渡するには、Azure エンタープライズ ポータルで新しいサポート リクエストを作成する必要があります。 サポート リクエストを作成するには、 **[ヘルプとサポート]** 領域の **[+ 新しいサポート リクエスト]** を選択します。

## <a name="change-azure-subscription-or-account-ownership"></a>Azure サブスクリプションまたはアカウントの所有権を変更する

Azure EA Portal では、アカウント所有者間でサブスクリプションを転送できます。 詳細については、「[Azure サブスクリプションまたはアカウントの所有権を変更する](ea-portal-administration.md#change-azure-subscription-or-account-ownership)」をご覧ください。

## <a name="subscription-transfer-effects"></a>サブスクリプションを転送した場合の影響

同じ Azure Active Directory テナント内のアカウントに Azure サブスクリプションを転送した場合、リソースを管理するための [Azure ロールベースのアクセス制御 (Azure RBAC)](../../role-based-access-control/overview.md) が付与されていたユーザー、グループ、サービス プリンシパルはすべて、そのアクセス権を維持します。

サブスクリプションに対する RBAC アクセス権を持つユーザーを表示するには、次の手順を実行します。

1. Azure portal で **[サブスクリプション]** を開きます。
2. 表示するサブスクリプションを選択し、 **[アクセス制御 (IAM)]** を選択します。
3. **[ロールの割り当て]** を選択します。 [ロールの割り当て] ページに、サブスクリプションに対する RBAC アクセス権が付与されているすべてのユーザーが一覧表示されます。

別の Azure AD テナント内のアカウントにサブスクリプションを転送した場合は、リソースを管理するための [RBAC](../../role-based-access-control/overview.md) が付与されていたユーザー、グループ、サービス プリンシパルはすべて、そのアクセス権を "_失います_"。 RBAC アクセス権がなくなっても、サブスクリプションへのアクセスは、次のようなセキュリティ メカニズムを通じて使用できる場合があります。

- サブスクリプションのリソースに対する管理者権限をユーザーに付与する管理証明書。 詳細については、「[Azure の管理証明書の作成とアップロード](../../cloud-services/cloud-services-certs-create.md)」をご覧ください。
- Storage などのサービス用のアクセス キー。 詳細については、「[Azure ストレージ アカウントの概要](../../storage/common/storage-account-overview.md)」を参照してください。
- Azure Virtual Machines などのサービス用のリモート アクセス資格情報。

転送先で Azure リソースへのアクセスを制限する必要がある場合、サービスに関連付けられているすべてのシークレットの更新を検討する必要があります。 ほとんどのリソースは、次の手順を使って更新できます。

1. [Azure portal](https://portal.azure.com/) にサインインします。
2. ハブ メニューで、 **[すべてのリソース]** を選択します。
3. リソースを選択します。
4. リソース ページで **[設定]** を選択し、既存のシークレットを表示して更新します。

## <a name="next-steps"></a>次のステップ

- Azure EA Portal の問題のトラブルシューティングに関するヘルプが必要な場合は、「[Troubleshoot Azure EA portal access (Azure EA Portal へのアクセスのトラブルシューティング)](ea-portal-troubleshoot.md)」を参照してください。