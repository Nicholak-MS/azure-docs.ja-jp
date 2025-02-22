---
title: 進行中のサーバー検出、ソフトウェア インベントリ、SQL 検出のトラブルシューティング
description: サーバー検出、ソフトウェア インベントリ、SQL および Web アプリの検出に関するヘルプを提供します。
author: Vikram1988
ms.author: vibansa
ms.manager: abhemraj
ms.topic: troubleshooting
ms.date: 07/01/2020
ms.openlocfilehash: ffa77200a3f0341e74a049b7db3196ef1d726e73
ms.sourcegitcommit: add71a1f7dd82303a1eb3b771af53172726f4144
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2021
ms.locfileid: "123423872"
---
# <a name="troubleshoot-ongoing-server-discovery-software-inventory-and-sql-and-web-apps-discovery"></a>進行中のサーバー検出、ソフトウェア インベントリ、SQL および Web アプリの検出のトラブルシューティング

この記事は、進行中のサーバー検出、ソフトウェア インベントリ、SQL Server インスタンス、データベースの検出に関する問題のトラブルシューティングを行う際に役立ちます。

## <a name="discovered-servers-not-showing-in-the-portal"></a>検出されたサーバーがポータルに表示されない

このエラーは、ポータルにサーバーが表示されず、検出状態が **検出中** の場合に発生します。
 
### <a name="remediation"></a>修復

サーバーがポータルに表示されない場合は、数分お待ちください。vCenter Server で実行されているサーバーの検出に約 15 分かかるためです。 また、アプライアンスに追加された各 Hyper-V ホストの場合はホスト上で実行されているサーバーを検出するのに 2 分かかり、物理アプライアンスに追加された各サーバーの検出に 1 分かかります。

それでも状態が変わらない場合は、次のようにします。

- **[サーバー]** タブで **[最新の情報に更新]** を選択して、Azure Migrate: Discovery and Assessment および Azure Migrate: Server Migration で検出されたサーバーの数を確認します。

上記の手順が機能せず、VMware サーバーを検出している場合は、次のようにします。

1. 指定した vCenter アカウントに、少なくとも 1 つのサーバーにアクセスできるアクセス許可が正しく設定されていることを確認してください。
1. vCenter アカウントに vCenter VM フォルダー レベルでアクセス権が付与されているかどうかを VMware で確認します。 Azure Migrate で VMware 上のサーバーを検出することはできません。 検出のスコープ設定についての[詳細をご覧ください](set-discovery-scope.md)。

## <a name="server-data-not-updating-in-the-portal"></a>サーバー データがポータルで更新されない

このエラーは、検出されたサーバーがポータルに表示されないか、サーバー データが期限切れになっている場合に発生します。 

### <a name="remediation"></a>修復

検出されたサーバー構成データの変更がポータルに表示されるのに最大 30 分かかり、ソフトウェア インベントリ データの変更が表示されるのに数時間かかるため、数分お待ちください。 この時間が経過してもデータがない場合は、最新の情報に更新してから、次の手順を行います。

1. **Windows、Linux、SQL Server** で、**Azure Migrate: Discovery and Assessment** の **[概要]** を選択します。
1. **[管理]** で、 **[アプライアンス]** を選択します。
1. **[サービスの更新]** を選択します。
更新操作が終了するまで待ちます。 これで、最新の情報が表示されるはずです。

## <a name="deleted-servers-appear-in-the-portal"></a>削除されたサーバーがポータルに表示される

このエラーは、削除されたサーバーがポータルに引き続き表示される場合に発生します。

### <a name="remediation"></a>修復

データが引き続き表示される場合は、30 分間待ってから、次の手順を行います。

1. **Windows、Linux、SQL Server** で、**Azure Migrate: Discovery and Assessment** の **[概要]** を選択します。
1. **[管理]** で、 **[アプライアンス]** を選択します。
1. **[サービスの更新]** を選択します。
更新操作が終了するまで待ちます。 これで、最新の情報が表示されるはずです。

## <a name="you-imported-a-csv-but-see-discovery-is-in-progress"></a>CSV をインポートしたが、"検出は現在進行中です" と表示される

この状態は、検証の失敗が原因で CSV のアップロードに失敗した場合に表示されます。

### <a name="remediation"></a>修復

CSV をもう一度インポートします。 前回のアップロードのエラー レポートをダウンロードし、ファイルの修復ガイダンスに従って、エラーを修正します。 エラー レポートは、 **[Discover servers]\(サーバーの検出\)** ページの **[インポートの詳細]** セクションからダウンロードします。

## <a name="you-dont-see-software-inventory-details-after-you-update-guest-credentials"></a>ゲスト資格情報を更新した後、ソフトウェア インベントリの詳細が表示されない

このエラーは、ゲスト資格情報を更新した後もインベントリの詳細が表示されない場合に発生します。

### <a name="remediation"></a>修復

ソフトウェア インベントリ検出は 24 時間ごとに 1 回実行されます。 このプロセスは、検出されるサーバーの数によっては数分かかる場合があります。 詳細をすぐに確認するには、次のように更新します。

1. **Windows、Linux、SQL Server** で、**Azure Migrate: Discovery and Assessment** の **[概要]** を選択します。
1. **[管理]** で、 **[アプライアンス]** を選択します。
1. **[サービスの更新]** を選択します。
更新操作が終了するまで待ちます。 これで、最新の情報が表示されるはずです。

## <a name="unable-to-export-software-inventory"></a>ソフトウェア インベントリをエクスポートできない

このエラーは、共同作成者権限を持っていない場合に発生します。

### <a name="remediation"></a>修復

ポータルからインベントリをダウンロードするユーザーに、サブスクリプションに対する共同作成者権限があることを確認します。

## <a name="common-software-inventory-errors"></a>一般的なソフトウェア インベントリ エラー

Azure Migrate では、ソフトウェア インベントリがサポートされており、これには Azure Migrate: Discovery and Assessment が使用されます。 現在、ソフトウェア インベントリは VMware でのみサポートされています。 ソフトウェア インベントリの要件については、[こちら](how-to-discover-applications.md)をご覧ください。

ソフトウェア インベントリ エラーの一覧を次の表にまとめました。

> [!Note]
> エージェントレスの依存関係分析でも同じエラーが発生するおそれがあります。これは、必要なデータを収集するために、ソフトウェア インベントリと同じ方法に従うためです。

| **Error** | **原因** | **操作** |
|--|--|--|
| **9000**: サーバー上の VMware ツールの状態を検出できません。 | VMware ツールがサーバーにインストールされていないか、インストールされているバージョンが破損しているおそれがあります。 | バージョン 10.2.1 より後の VMware ツールが確実にサーバーにインストールされ、実行されているようにします。 |
| **9001**: VMware ツールがサーバーにインストールされていません。 | VMware ツールがサーバーにインストールされていないか、インストールされているバージョンが破損しているおそれがあります。 | バージョン 10.2.1 より後の VMware ツールが確実にサーバーにインストールされ、実行されているようにします。 |
| **9002**: VMware ツールがサーバーで実行されていません。 | VMware ツールがサーバーにインストールされていないか、インストールされているバージョンが破損しているおそれがあります。 | バージョン 10.2.0 より後の VMware ツールが確実にサーバーにインストールされ、実行されているようにします。 |
| **9003**: サーバーで実行されているオペレーティング システムの種類はサポートされていません。 | サーバーで実行されているオペレーティング システムが Windows または Linux ではありません。 | サポートされている OS の種類は Windows と Linux だけです。 サーバーで Windows または Linux OS が実行されている場合は、vCenter Server で指定されているオペレーティング システムの種類を調べてください。 |
| **9004**: サーバーが実行中の状態ではありません。 | サーバーは電源オフの状態です。 | サーバーが実行中の状態であることを確認してください。 |
| **9005**: サーバーで実行されているオペレーティング システムの種類はサポートされていません。 | サーバーで実行されているオペレーティング システムが Windows または Linux ではありません。 | サポートされている OS の種類は Windows と Linux だけです。 \<FetchedParameter> オペレーティング システムは現在サポートされていません。 |
| **9006**: サーバーから検出メタデータ ファイルをダウンロードするために必要な URL が空です。 | この問題は、アプライアンス上の検出エージェントが想定どおりに動作していないことが原因で一時的に発生するおそれがあります。 | この問題は通常、24 時間以内に次のサイクルで自動的に解決されます。 問題が解決しない場合は、Microsoft サポート ケースを送信してください。 |
| **9007**: スクリプトを実行してメタデータを収集するプロセスがサーバーに見つかりません。 | この問題は、アプライアンス上の検出エージェントが想定どおりに動作していないことが原因で一時的に発生するおそれがあります。 | この問題は通常、24 時間以内に次のサイクルで自動的に解決されます。 問題が解決しない場合は、Microsoft サポート ケースを送信してください。 |
| **9008**: メタデータを収集するためにサーバーで実行されているプロセスの状態を取得できません。 | この問題は、内部エラーが原因で一時的に発生する場合があります。 | この問題は通常、24 時間以内に次のサイクルで自動的に解決されます。 問題が解決しない場合は、Microsoft サポート ケースを送信してください。 |
| **9009**: Windows ユーザー アカウント制御 (UAC) によって、サーバー上の検出操作の実行が妨げられています。 | Windows UAC の設定により、インストールされているアプリケーションをサーバーから検出することが制限されています。 | 影響を受けているサーバーのコントロール パネルで、 **[ユーザー アカウント制御]** 設定のレベルを下げてください。 |
| **9010**: サーバーの電源がオフになっています。 | サーバーは電源オフの状態です。 | サーバーが確実に電源オンの状態になるようにしてください。 |
| **9011**: サーバー上で、検出されたメタデータを含むファイルが見つかりません。 | この問題は、内部エラーが原因で一時的に発生する場合があります。 | この問題は通常、24 時間以内に次のサイクルで自動的に解決されます。 問題が解決しない場合は、Microsoft サポート ケースを送信してください。 |
| **9012**: サーバー上で、検出されたメタデータを含むファイルが空です。 | この問題は、内部エラーが原因で一時的に発生する場合があります。 | この問題は通常、24 時間以内に次のサイクルで自動的に解決されます。 問題が解決しない場合は、Microsoft サポート ケースを送信してください。 |
| **9013**: サーバーにログインするたびに、新しい一時ユーザー プロファイルが作成されます。 | サーバーにログインするたびに、新しい一時ユーザー プロファイルが作成されます。 | Microsoft サポート ケースを送信して、この問題のトラブルシューティングの支援を受けてください。 |
| **9014**: ESXi ホストで発生したエラーが原因で、検出されたメタデータを含むファイルを取得できません。 エラー コード: %ErrorCode、詳細: %ErrorMessage | ESXi ホスト \<HostName> でエラーが発生しました。 エラー コード: %ErrorCode、詳細: %ErrorMessage | サーバーが実行されている ESXi ホストでポート 443 が開いていることを確認してください。<br/><br/> この問題の修復方法については、[こちら](troubleshoot-discovery.md#error-9014-httpgetrequesttoretrievefilefailed)をご覧ください。|
| **9015**: サーバー検出で指定された vCenter Server ユーザー アカウントでゲスト操作権限が有効になっていません。 | ゲスト操作に必要な権限が vCenter Server ユーザー アカウントで有効になっていません。 | サーバーとやりとりし、必要なデータをプルするために、vCenter Server ユーザー アカウントで、 **[Virtual Machines]\(仮想マシン\)**  >  **[Guest Operations]\(ゲスト操作\)** の権限が確実に有効になっているようにします。 <br/><br/> 必要な権限を持つ vCenter Server アカウントを設定する方法の詳細については、[こちら](tutorial-discover-vmware.md#prepare-vmware)をご覧ください。 |
| **9016**: サーバー上のゲスト操作エージェントが古くなっているため、メタデータを検出できません。 | VMware ツールがサーバーにインストールされていないか、インストールされているバージョンが最新ではありません。 | VMware ツールがサーバーにインストールされ、最新の状態で実行されていることを確認します。 VMware ツールのバージョンは、バージョン 10.2.1 以降である必要があります。 |
| **9017**: サーバー上で、検出されたメタデータを含むファイルが見つかりません。 | この問題は、内部エラーが原因で一時的に発生する場合があります。 | Microsoft サポート ケースを送信して、この問題のトラブルシューティングの支援を受けてください。 |
| **9018**: PowerShell がサーバーにインストールされていません。 | PowerShell がサーバー上に見つかりません。 | PowerShell バージョン 2.0 以降がサーバーにインストールされていることを確認してください。 <br/><br/> この問題の修復方法については、[こちら](troubleshoot-discovery.md#error-9018-powershellnotfound)をご覧ください。|
| **9019**: サーバーでのゲスト操作エラーが原因でメタデータを検出できません。 | サーバーで VMware ゲスト操作が失敗しました。 この問題は、サーバーで次の資格情報を試行したときに発生しました: ```<FriendlyNameOfCredentials>.``` | アプライアンス上で指定されたサーバー資格情報が確実に有効であり、資格情報で指定されたユーザー名がユーザー プリンシパル名 (UPN) 形式であるようにしてください。 (考えられる原因の中で、Azure Migrate によって試行された資格情報のフレンドリ名を見つけます)。 |
| **9020**: サーバー上で、検出されたメタデータを含めるために必要なファイルを作成できません。 | アプライアンス上で指定された資格情報に関連付けられているロールまたはオンプレミスのグループ ポリシーによって、必要なフォルダー内でのファイル作成が制限されています。 この問題は、サーバーで次の資格情報を試行したときに発生しました: ```<FriendlyNameOfCredentials>.``` | 1. アプライアンス上で指定された資格情報に、サーバー内のフォルダー \<folder path/folder name> でのファイル作成アクセス許可があるかどうかを確認します。 <br/>2. アプライアンス上で指定された資格情報に必要なアクセス許可がない場合は、別の資格情報セットを指定するか、既存のものを編集します。 (考えられる原因の中で、Azure Migrate によって試行された資格情報のフレンドリ名を見つけます)。 |
| **9021**: サーバー上で、検出されたメタデータを含めるために必要なファイルを正しいパスで作成できません。 | VMware ツールから、ファイルを作成するためのファイル パスが正しくないことが報告されています。 | バージョン 10.2.0 より後の VMware ツールが確実にサーバーにインストールされ、実行されているようにします。 |
| **9022**: Get-WmiObject コマンドレットをサーバーで実行するためのアクセスが拒否されました。 | アプライアンス上で指定された資格情報に関連付けられているロールまたはオンプレミスのグループ ポリシーによって、WMI オブジェクトへのアクセスが制限されています。 この問題は、サーバーで次の資格情報を試行したときに発生しました: \<FriendlyNameOfCredentials>。 | 1. アプライアンス上で指定された資格情報に、ファイル作成管理者権限があり、WMI が有効になっているかどうかを調べます。 <br/> 2. アプライアンス上の資格情報に必要なアクセス許可がない場合は、別の資格情報セットを指定するか、既存のものを編集します。 (考えられる原因の中で、Azure Migrate によって試行された資格情報のフレンドリ名を見つけます)。<br/><br/> この問題の修復方法については、[こちら](troubleshoot-discovery.md#error-9022-getwmiobjectaccessdenied)をご覧ください。|
| **9023**: %SystemRoot% 環境変数の値が空のため、PowerShell を実行できません。 | サーバーの %SystemRoot% 環境変数の値が空です。 | 1. 影響を受けているサーバーで echo %systemroot% コマンドを実行して、この環境変数が空の値を返しているか調べます。 <br/> 2. 問題が解決しない場合は、Microsoft サポート ケースをお送りください。 |
| **9024**: %TEMP% 環境変数の値が空のため、検出を実行できません。 | サーバーの %TEMP% 環境変数の値が空です。 | 1. 影響を受けているサーバーで echo %temp% コマンドを実行して、この環境変数が空の値を返しているか調べます。 <br/> 2. 問題が解決しない場合は、Microsoft サポート ケースをお送りください。 |
| **9025**: サーバー上の PowerShell が破損しているため、検出を実行できません。 | サーバー上の PowerShell が破損しています。 | 影響を受けているサーバーで PowerShell を再インストールして、実行されていることをご確認ください。 |
| **9026**: サーバーでゲスト操作を実行できません。 | サーバーの現在の状態では、ゲスト操作の実行は許可されていません。 | 1. 影響を受けているサーバーが確実に稼働中であるようにします。<br/> 2. 問題が解決しない場合は、Microsoft サポート ケースをお送りください。 |
| **9027**: サーバー上でゲスト操作エージェントが実行されていないため、メタデータを検出できません。 | サーバー上のゲスト操作エージェントにアクセスできません。 | バージョン 10.2.0 より後の VMware ツールが確実にサーバーにインストールされ、実行されているようにします。 |
| **9028**: サーバー上のストレージが足りないため、検出されたメタデータを含めるために必要なファイルを作成できません。 | サーバー ディスクに十分なストレージ スペースがありません。 | 影響を受けているサーバーのディスク ストレージに十分なスペースを確保してください。 |
| **9029**: アプライアンス上で指定された資格情報に、PowerShell を実行するためのアクセス許可がありません。 | アプライアンス上で指定された資格情報に、PowerShell を実行するためのアクセス許可がありません。 この問題は、サーバーで次の資格情報を試行したときに発生しました: \<FriendlyNameOfCredentials>。 | 1. アプライアンス上の資格情報で確実にサーバー上の PowerShell にアクセスできるようにします。<br/> 2. アプライアンス上の資格情報に必要なアクセス権がない場合は、別の資格情報セットを指定するか、既存のものを編集します。 (考えられる原因の中で、Azure Migrate によって試行された資格情報のフレンドリ名を見つけます)。 |
| **9030**: サーバーがホストされている ESXi ホストが切断状態であるため、検出されたメタデータを収集できません。 | サーバーが存在している ESXi ホストは切断状態です。 | サーバーを実行している ESXi ホストが接続状態であるか確認してください。 |
| **9031**: サーバーがホストされている ESXi ホストが応答していないため、検出されたメタデータを収集できません。 | サーバーが存在している ESXi ホストは無効な状態です。 | サーバーを実行している ESXi ホストが実行中で接続済みの状態であることを確認してください。 |
| **9032**: 内部エラーが原因で検出できません。 | この問題は内部エラーが原因で発生しました。 | [こちらの Web サイト](troubleshoot-discovery.md#error-9032-invalidrequest)の手順に従って、問題を修復してください。 問題が解決しない場合は、Microsoft サポート ケースを開いてください。 |
| **9033**: サーバーに対してアプライアンス上で指定された資格情報のユーザー名に無効な文字が含まれているため、検出できません。 | アプライアンスに指定された資格情報のユーザー名に無効な文字が含まれています。 この問題は、サーバーで次の資格情報を試行したときに発生しました: \<FriendlyNameOfCredentials>。 | アプライアンス上で指定された資格情報のユーザー名に確実に無効な文字が含まれないようにします。 アプライアンス構成マネージャーに戻って、資格情報を編集できます。 (考えられる原因の中で、Azure Migrate によって試行された資格情報のフレンドリ名を見つけます)。 |
| **9034**: サーバーに対してアプライアンス上で指定された資格情報のユーザー名が UPN 形式でないため、検出できません。 | アプライアンス上の資格情報に、UPN 形式のユーザー名が含まれません。 この問題は、サーバーで次の資格情報を試行したときに発生しました: \<FriendlyNameOfCredentials>。 | アプライアンス上の資格情報に、確実に UPN 形式のユーザー名が含まれるようにします。 アプライアンス構成マネージャーに戻って、資格情報を編集できます。 (考えられる原因の中で、Azure Migrate によって試行された資格情報のフレンドリ名を見つけます)。 |
| **9035**: PowerShell の言語モードが正しく設定されていないため、検出できません。 | PowerShell の言語モードが **全言語** に設定されていません。 | PowerShell の言語モードが確実に **全言語** に設定されているようにします。 |
| **9036**: サーバーに対してアプライアンス上で指定された資格情報のユーザー名が UPN 形式でないため、検出できません。 | アプライアンス上の資格情報に、UPN 形式のユーザー名が含まれません。 この問題は、サーバーで次の資格情報を試行したときに発生しました: \<FriendlyNameOfCredentials>。 | アプライアンス上の資格情報に、確実に UPN 形式のユーザー名が含まれるようにします。 アプライアンス構成マネージャーに戻って、資格情報を編集できます。 (考えられる原因の中で、Azure Migrate によって試行された資格情報のフレンドリ名を見つけます)。 |
| **9037**: サーバーからの応答時間が長いため、メタデータ収集が一時的に中断しています。 | サーバーの応答に時間がかかりすぎています。 | この問題は通常、24 時間以内に次のサイクルで自動的に解決されます。 問題が解決しない場合は、Microsoft サポート ケースを送信してください。 |
| **10000**: サーバーで実行されているオペレーション システムの種類はサポートされていません。 | サーバーで実行されているオペレーティング システムが Windows または Linux ではありません。 | サポートされている OS の種類は Windows と Linux だけです。 \<GuestOSName> オペレーティング システムは現在サポートされていません。 |
| **10001**: サーバー上で、検出メタデータを収集するために必要なスクリプトが見つかりません。 | 検出を実行するために必要なスクリプトが、想定される場所から削除または除去された可能性があります。 | Microsoft サポート ケースを送信して、この問題のトラブルシューティングの支援を受けてください。 |
| **10002**: サーバーで検出操作がタイムアウトになりました。 | この問題は、アプライアンス上の検出エージェントが想定どおりに動作していないことが原因で一時的に発生するおそれがあります。 | この問題は通常、24 時間以内に次のサイクルで自動的に解決されます。 解決しない場合は、[こちらの Web サイト](troubleshoot-discovery.md#error-10002-scriptexecutiontimedoutonvm)の手順に従って問題を修復してください。 問題が解決しない場合は、Microsoft サポート ケースを開いてください。|
| **10003**: 検出操作を実行するプロセスがエラーで終了しました。 | 検出操作を実行するプロセスが、エラーのため突然終了しました。| この問題は通常、24 時間以内に次のサイクルで自動的に解決されます。 問題が解決しない場合は、Microsoft サポート ケースを送信してください。 |
| **10004**: サーバー OS の種類に対する資格情報がアプライアンス上で指定されていません。 | サーバー OS の種類に対する資格情報がアプライアンス上で追加されませんでした。 | 1. 影響を受けているサーバーの OS の種類に対する資格情報を確実にアプライアンス上で追加するようにします。<br/> 2. 複数のサーバー資格情報をアプライアンスで追加できるようになりました。 |
| **10005**: サーバーに対して、アプライアンス上で指定された資格情報が無効です。 | アプライアンス上で指定された資格情報が無効です。 この問題は、サーバーで次の資格情報を試行したときに発生しました: ```\<FriendlyNameOfCredentials>.``` | 1. アプライアンス上で指定された資格情報が確実に有効であること、この資格情報を使用してサーバーにアクセスできるようにします。<br/> 2. 複数のサーバー資格情報をアプライアンスで追加できるようになりました。<br/> 3. アプライアンス構成マネージャーに戻り、別の資格情報のセットを指定するか、既存のものを編集します。 (考えられる原因の中で、Azure Migrate によって試行された資格情報のフレンドリ名を見つけます)。 <br/><br/> この問題の修復方法については、[こちら](troubleshoot-discovery.md#error-10005-guestcredentialnotvalid)をご覧ください。|
| **10006**: サーバーで実行されているオペレーション システムの種類はサポートされていません。 | サーバーで実行されているオペレーティング システムが Windows または Linux ではありません。 | サポートされている OS の種類は Windows と Linux だけです。 \<GuestOSName> オペレーティング システムは現在サポートされていません。 |
| **10007**: サーバーからの検出されたメタデータを処理できません。 | 検出されたメタデータを含むファイルの内容を解析しているときエラーが発生しました。 | Microsoft サポート ケースを送信して、この問題のトラブルシューティングの支援を受けてください。 |
| **10008**: 検出されたメタデータを含めるために必要なファイルをサーバーに作成できません。 | アプライアンス上で指定された資格情報に関連付けられているロールまたはオンプレミスのグループ ポリシーによって、必要なフォルダー内でのファイル作成が制限されています。 この問題は、サーバーで次の資格情報を試行したときに発生しました: ```<FriendlyNameOfCredentials>.``` | 1. アプライアンス上で指定された資格情報に、サーバー内のフォルダー \<folder path/folder name> でのファイル作成アクセス許可があるかどうかを調べます。<br/> 2. アプライアンス上で指定された資格情報に必要なアクセス許可がない場合は、別の資格情報セットを指定するか、既存のものを編集します。 (考えられる原因の中で、Azure Migrate によって試行された資格情報のフレンドリ名を見つけます)。 |
| **10009**: 検出されたメタデータをサーバー上のファイルに書き込めません。 | アプライアンスで指定された資格情報に関連付けられているロール、またはオンプレミスのグループ ポリシーによって、サーバー上のファイルへの書き込みが制限されています。 この問題は、サーバーで次の資格情報を試行したときに発生しました: \<FriendlyNameOfCredentials>。 | 1. アプライアンス上で指定された資格情報に、サーバー内のフォルダー <フォルダー パス/フォルダー名> へのファイル書き込みアクセス許可があるかどうかを調べます。<br/> 2. アプライアンス上で指定された資格情報に必要なアクセス許可がない場合は、別の資格情報セットを指定するか、既存のものを編集します。 (考えられる原因の中で、Azure Migrate によって試行された資格情報のフレンドリ名を見つけます)。 |
| **10010**: メタデータを収集するために必要なコマンド %CommandName; がサーバー上で見つからないため、検出できません。 | コマンド %CommandName; を含むパッケージがサーバーにインストールされていません。 | コマンド %CommandName; を含むパッケージが確実にサーバーにインストールされているようにします。 |
| **10011**: アプライアンス上で指定された資格情報が、対話型セッションのログインとログオフに使用されました。 | 対話型のログインとログオフにより、使用されているアカウントのプロファイルでレジストリ キーが強制的にアンロードされます。 この条件により、キーを後で使用することができなくなります。 | [こちらの Web サイト](/sharepoint/troubleshoot/administration/800703fa-illegal-operation-error#resolutionus/sharepoint/troubleshoot/administration/800703fa-illegal-operation-error)に記載されている解決方法を使用してください。 |
| **10012**: サーバーに対する資格情報が、アプライアンス上で指定されていません。 | サーバーに対して資格情報が指定されていないか、アプライアンス上で指定したドメイン資格情報のドメイン名が正しくありません。 このエラーの原因の詳細については、[こちら](troubleshoot-discovery.md#error-10012-credentialnotprovided)をご覧ください。 | 1. サーバーに対してアプライアンス上で資格情報が確実に指定され、資格情報を使用してサーバーにアクセスできるようにします。 <br/> 2. サーバー向けの複数の資格情報をアプライアンスで追加できるようになりました。 アプライアンス構成マネージャーに戻り、サーバーの資格情報を指定します。|

## <a name="error-9014-httpgetrequesttoretrievefilefailed"></a>エラー 9014: HTTPGetRequestToRetrieveFileFailed

### <a name="cause"></a>原因
この問題は、アプライアンス内の VMware 検出エージェントが、依存関係データを含む出力ファイルを、サーバー ファイル システムから、サーバーがホストされている ESXi ホストを経由してダウンロードしようとしたときに発生します。

### <a name="remediation"></a>修復
- アプライアンス サーバー上で PowerShell を開き、次のコマンドを実行することで、アプライアンスからポート 443 (依存関係データをプルするために ESXi ホストで開く必要があります) 上の ESXi ホスト " _(名前はエラー メッセージに示されています)_ " への TCP 接続をテストできます。
 
   ````
   Test -NetConnection -ComputeName <Ip address of the ESXi host> -Port 443
   ````

- コマンドから正常な接続が返された場合は、**Azure Migrate プロジェクト** > **Discovery and Assessment** >  **[概要]**  >  **[管理]**  >  **[アプライアンス]** に移動し、アプライアンス名を選択して、 **[Refresh services]\(サービスの更新\)** を選択します。

## <a name="error-9018-powershellnotfound"></a>エラー 9018: PowerShellNotFound

### <a name="cause"></a>原因
このエラーは通常、Windows Server 2008 以前を実行しているサーバーで表示されます。

### <a name="remediation"></a>修復
必要な PowerShell バージョン (2.0 以降) をサーバーの次の場所にインストールします: ($SYSTEMROOT)\System32\WindowsPowershell\v1.0\powershell.exe。 PowerShell を Windows Server にインストールする方法の詳細については、[こちら](/powershell/scripting/windows-powershell/install/installing-windows-powershell)をご覧ください。

必要な PowerShell バージョンをインストールしたら、[こちらの Web サイト](troubleshoot-discovery.md#mitigation-verification-by-using-vmware-powercli)の手順に従って、エラーが解決したかどうかを検証してください。

## <a name="error-9022-getwmiobjectaccessdenied"></a>エラー 9022: GetWMIObjectAccessDenied

### <a name="remediation"></a>修復
アプライアンスに指定されたユーザー アカウントが WMI 名前空間および副名前空間にアクセスできることを確認します。 アクセスを設定するには:

1.  このエラーを報告しているサーバーに移動します。
1. **[スタート]** メニューで **[ファイル名を指定して実行]** を検索して選択します。 **[ファイル名を指定して実行]** ダイアログで、 **[名前]** テキスト ボックスに「**wmimgmt.msc**」と入力し、**Enter** を選択します。
1. wmimgmt コンソールが開き、左側のペインに **[WMI コントロール (ローカル)]** が表示されます。 それを右クリックして、メニューから **[プロパティ]** を選択します。
1. **[WMI コントロール (ローカル) のプロパティ]** ダイアログで、 **[セキュリティ]** タブを選択します。
1. **[セキュリティ]** を選択して **[セキュリティ Root]** ダイアログを開きます。
1. **[詳細設定]** を選択して、 **[Root のセキュリティの詳細設定]** ダイアログを開きます。 
1. **[追加]** を選択して、 **[Root のアクセス許可エントリ]** ダイアログを開きます。
1. **[プリンシパルの選択]** をクリックして、 **[Select Users, Computers, Service Accounts or Groups]\(ユーザー、コンピューター、サービス アカウントまたはグループの選択\)** ダイアログを開きます。
1. WMI へのアクセス権を付与するユーザー名またはグループを選択して、 **[OK]** を選択します。
1. 実行アクセス許可を確実に付与し、 **[適用先]** ドロップダウン リストで **[この名前空間と副名前空間]** を選択します。
1. **[適用]** を選択して設定を保存し、すべてのダイアログを閉じます。

必要なアクセス権を取得したら、[こちらの Web サイト](troubleshoot-discovery.md#mitigation-verification-by-using-vmware-powercli)の手順に従って、エラーが解決したかどうかを検証してください。

## <a name="error-9032-invalidrequest"></a>エラー 9032: InvalidRequest

### <a name="cause"></a>原因
この問題には複数の理由が考えられます。 理由の 1 つは、アプライアンス構成マネージャーで指定されたユーザー名 (サーバー資格情報) に無効な XML 文字が含まれている場合です。 無効な文字があると、SOAP 要求の解析中にエラーが発生します。

### <a name="remediation"></a>修復
- サーバー資格情報のユーザー名に無効な XML 文字が含まれておらず、username@domain.com 形式であることをご確認ください。 この形式は、一般に UPN 形式と呼ばれています。
- アプライアンス上の資格情報を編集したら、[こちらの Web サイト](troubleshoot-discovery.md#mitigation-verification-by-using-vmware-powercli)の手順に従って、エラーが解決したかどうかを検証してください。


## <a name="error-10002-scriptexecutiontimedoutonvm"></a>エラー 10002: ScriptExecutionTimedOutOnVm

### <a name="cause"></a>原因
- このエラーは、サーバーが遅いか応答がなく、依存関係データをプルするために実行されたスクリプトがタイムアウトし始めると発生します。
- このエラーが検出エージェントによってサーバー上で検出されると、その後は、応答しないサーバーが過負荷にならないように、サーバー上のエージェントレスの依存関係分析はアプライアンスによって試行されません。
- サーバーの問題を確認し、検出サービスを再起動するまで、エラーが表示され続けます。

### <a name="remediation"></a>修復

1. このエラーが発生しているサーバーにサインインします。
1. PowerShell で次のコマンドを実行します。

   ````
   Get-WMIObject win32_operatingsystem;
   Get-WindowsFeature  | Where-Object {$_.InstallState -eq 'Installed' -or ($_.InstallState -eq $null -and $_.Installed -eq 'True')};
   Get-WmiObject Win32_Process;
   netstat -ano -p tcp | select -Skip 4;
   ````
1. コマンドの結果が数秒で出力された場合は、**Azure Migrate プロジェクト** > **Discovery and Assessment** >  **[概要]**  >  **[管理]**  >  **[アプライアンス]** に移動し、アプライアンス名を選択し、 **[Refresh services]\(サービスの更新\)** を選択して検出サービスを再開します。
1. コマンドから出力が返されずにタイムアウトする場合は、次のことを行う必要があります。

   - サーバー上の CPU またはメモリを大きく消費しているプロセスがどれかを見つけ出す。
   - さらに多くのコアまたはメモリをそのサーバーに提供して、コマンドを再実行してみる。

## <a name="error-10005-guestcredentialnotvalid"></a>エラー 10005: GuestCredentialNotValid

### <a name="remediation"></a>修復
- アプライアンス構成マネージャーで **[Revalidate credentials]\(資格情報の再検証\)** を選択して、資格情報 " _(エラーに表示されるフレンドリ名)_ " が確実に有効であるようにします。
- アプライアンスに指定されたのと同じ資格情報を使用して、影響を受けているサーバーに確実にサインインできるようにします。
- そのサーバーに対して、(サーバーがドメインに参加している場合は同じドメインの) 別のユーザー アカウントを、管理者アカウントの代わりに使用して再試行できます。
- この問題は、グローバル カタログとドメイン コントローラー間の通信が切断されているときに発生する可能性があります。 この問題を調べるには、ドメイン コントローラーで新しいユーザー アカウントを作成し、同じものをアプライアンスに指定します。 また、ドメイン コントローラーの再起動が必要になる場合もあります。
- 修復手順を行ったら、[こちらの Web サイト](troubleshoot-discovery.md#mitigation-verification-by-using-vmware-powercli)の手順に従って、エラーが解決したかどうかを検証してください。

## <a name="error-10012-credentialnotprovided"></a>エラー 10012: CredentialNotProvided

### <a name="cause"></a>原因
このエラーは、ドメイン名が正しくないドメイン資格情報をアプライアンス構成マネージャーで指定したときに発生します。 たとえば、ユーザー名が user@abc.com のドメイン資格情報を指定したが、ドメイン名を def.com と指定した場合、サーバーが def.com に接続されていると、これらの資格情報は試行されず、このエラー メッセージが表示されます。

### <a name="remediation"></a>修復
- アプライアンス構成マネージャーにアクセスしてサーバー資格情報を追加するか、原因で説明されているように、既存のものを編集します。
- 修復手順を行ったら、[こちらの Web サイト](troubleshoot-discovery.md#mitigation-verification-by-using-vmware-powercli)の手順に従って、エラーが解決したかどうかを検証してください。

## <a name="mitigation-verification-by-using-vmware-powercli"></a>VMware PowerCLI を使用した軽減策の検証
上記のエラーの軽減手順を使用したら、アプライアンス サーバーからいくつかの PowerCLI コマンドを実行して、軽減策が機能したかどうかを検証してください。 コマンドが成功した場合は、問題が解決されたことを意味します。 そうでない場合は、もう一度確認して修復手順に従ってください。

1. 次のコマンドを実行して、PowerCLI をアプライアンス サーバーで設定します。
   ````
   Install-Module -Name VMware.PowerCLI -AllowClobber
   Set-PowerCLIConfiguration -InvalidCertificateAction Ignore
   ````
1. コマンドに vCenter Server の IP アドレスを、プロンプトに資格情報を入力して、アプライアンスから vCenter Server に接続します。
   ````
   Connect-VIServer -Server <IPAddress of vCenter Server>
   ````
1. サーバー名とサーバー資格情報を (アプライアンス上で指定したように) 指定して、アプライアンスからターゲット サーバーに接続します。
   ````
   $vm = get-VM <VMName>
   $credential = Get-Credential
   ````
1. ソフトウェア インベントリの場合は、次のコマンドを実行して、正常に出力されることを確認します。

   - Windows サーバーの場合:

      ```` 
        Invoke-VMScript -VM $vm -ScriptText "powershell.exe 'Get-WMIObject win32_operatingsystem'" -GuestCredential $credential

        Invoke-VMScript -VM $vm -ScriptText "powershell.exe Get-WindowsFeature" -GuestCredential $credential
      ```` 
   - Linux サーバーの場合:
      ````
      Invoke-VMScript -VM $vm -ScriptText "ls" -GuestCredential $credential
      ````
1. エージェントレスの依存関係分析の場合は、次のコマンドを実行して、正常に出力されることを確認します。

   - Windows サーバーの場合:

      ```` 
      Invoke-VMScript -VM $vm -ScriptText "powershell.exe 'Get-WmiObject Win32_Process'" -GuestCredential $credential 
  
      Invoke-VMScript -VM $vm -ScriptText "powershell.exe 'netstat -ano -p tcp'" -GuestCredential $credential 
      ```` 
   - Linux サーバーの場合:
      ````
      Invoke-VMScript -VM $vm -ScriptText "ps -o pid,cmd | grep -v ]$" -GuestCredential $credential

      Invoke-VMScript -VM $vm -ScriptText "netstat -atnp | awk '{print $4,$5,$7}'" -GuestCredential $credential
      ````
1. 軽減策が効いたことを確認したら、**Azure Migrate プロジェクト** > **Discovery and Assessment** >  **[概要]**  >  **[管理]**  >  **[アプライアンス]** に移動し、アプライアンス名を選択し、 **[Refresh services]\(サービスの更新\)** を選択して検出サイクルを開始します。

## <a name="discovered-sql-server-instances-and-databases-not-in-the-portal"></a>検出された SQL Server インスタンスおよびデータベースがポータルに表示されない

アプライアンスで検出を開始した後、インベントリ データがポータルに表示され始めるまで最大 24 時間かかることがあります。

アプライアンス構成マネージャーで Windows 認証または SQL Server 認証の資格情報を指定していない場合は、資格情報を追加して、アプライアンスから、それらを使用してそれぞれの SQL Server インスタンスに接続できるようにします。

接続されると、アプライアンスによって、SQL Server インスタンスおよびデータベースの構成とパフォーマンスのデータが収集されます。 SQL Server 構成データは 24 時間ごとに更新され、パフォーマンス データは 30 秒ごとにキャプチャされます。 データベースの状態や互換性レベルなど、SQL Server インスタンスおよびデータベースのプロパティが変更されると、ポータル上で更新されるまで最大 24 時間かかることがあります。

## <a name="sql-server-instance-is-showing-up-in-a-not-connected-state-on-the-portal"></a>SQL Server インスタンスが、ポータルに "未接続" 状態と表示される

SQL Server インスタンスおよびデータベースの検出中に発生した問題を表示するには、プロジェクトの **[検出済みサーバー]** ページの接続状態列で、 **[未接続]** 状態を選択します。

完全に検出されなかった、あるいは未接続の状態にある SQL インスタンスが含まれるサーバーについて評価を作成すると、準備状態に **不明** マークが付くことがあります。

## <a name="common-sql-server-instances-and-database-discovery-errors"></a>一般的な SQL Server インスタンスおよびデータベースの検出エラー

Azure Migrate では、オンプレミスのマシンで実行されている SQL Server インスタンスおよびデータベースの検出がサポートされており、これには Azure Migrate: Discovery and Assessment を使用します。 現在、SQL 検出は VMware でのみサポートされています。 始めるには、[検出](tutorial-discover-vmware.md)に関するチュートリアルを参照してください。

一般的な SQL 検出エラーを次の表にまとめました。

| **Error** | **原因** | **操作** | **ガイド**
|--|--|--|--|
|**30000**: この SQL Server に関連付けられている資格情報が機能しませんでした。|手動で関連付けられた資格情報が無効であるか、または自動的に関連付けられた資格情報で SQL Server にアクセスできなくなりました。|アプライアンス上に SQL Server の資格情報を追加し、次の SQL 検出サイクルまで待つか、強制的に更新してください。| - |
|**30001**: アプライアンスから SQL Server に接続できません。|1. アプライアンスに SQL Server へのネットワーク通信経路がありません。<br/>2. ファイアウォールによって、SQL Server とアプライアンスの間の接続がブロックされています。|1. アプライアンスから SQL Server に到達できるようにします。<br/>2. アプライアンスから SQL Server への着信接続を許可します。| - | 
|**30003**: 証明書が信頼できません。|信頼できる証明書が、SQL Server を実行しているコンピューターにインストールされていません。|信頼できる証明書をサーバーに設定してください。 [詳細については、こちらを参照してください](/troubleshoot/sql/connect/error-message-when-you-connect)。| [表示](/troubleshoot/sql/connect/error-message-when-you-connect) |
|**30004**: 不十分なアクセス許可。|このエラーは、SQL Server インスタンスをスキャンするために必要なアクセス許可がないことが原因で発生することがあります。 |SQL Server インスタンスおよびデータベースを検出できるように、アプライアンス上で指定された資格情報またはアカウントに sysadmin ロールを付与してください。 [詳細については、こちらを参照してください](/sql/t-sql/statements/grant-server-permissions-transact-sql)。| [表示](/sql/t-sql/statements/grant-server-permissions-transact-sql) |
|**30005**: SQL Server ログインの既定のマスター データベースに問題があるため接続できませんでした。|データベース自体が無効であるか、ログインにデータベースでの CONNECT 権限がありません。|ALTER LOGIN を使用して、既定のデータベースをマスター データベースに設定します。<br/>SQL Server インスタンスおよびデータベースを検出できるように、アプライアンス上で指定された資格情報またはアカウントに sysadmin ロールを付与してください。 [詳細については、こちらを参照してください](/sql/relational-databases/errors-events/mssqlserver-4064-database-engine-error)。| [表示](/sql/relational-databases/errors-events/mssqlserver-4064-database-engine-error) |
|**30006**: SQL Server ログインは Windows 認証では使用できません。|1. ログインが SQL Server ログインの可能性がありますが、サーバーは Windows 認証しか受け付けません。<br/>2. SQL Server 認証を使用して接続しようとしていますが、使用しているログインが SQL Server に存在しません。<br/>3. ログインで Windows 認証を使用している可能性がありますが、そのログインは、認識できない Windows プリンシパルです。 認識できない Windows プリンシパルとは、ログインを Windows で確認できないことを意味します。 この問題は、Windows ログインが、信頼されていないドメインからであることが原因で発生することがあります。|SQL Server 認証を使用して接続しようとしている場合は、SQL Server が混合認証モードで構成されていること、および SQL Server ログインが存在することを確認します。<br/>Windows 認証を使用して接続しようとしている場合は、正しいドメインに適切にログインしていることを確認します。 [詳細については、こちらを参照してください](/sql/relational-databases/errors-events/mssqlserver-18452-database-engine-error)。| [表示](/sql/relational-databases/errors-events/mssqlserver-18452-database-engine-error) |
|**30007**: パスワードの有効期限が切れました。|このアカウントのパスワードの有効期限が切れています。|SQL Server ログイン パスワードの有効期限が切れているおそれがあります。 パスワードをリセットするか、パスワードの有効期限を延長してください。 [詳細については、こちらを参照してください](/sql/relational-databases/native-client/features/changing-passwords-programmatically)。| [表示](/sql/relational-databases/native-client/features/changing-passwords-programmatically) |
|**30008**: パスワードを変更する必要があります。|このアカウントのパスワードを変更する必要があります。|SQL Server の検出用に提供した資格情報のパスワードを変更してください。 [詳細については、こちらを参照してください](/previous-versions/sql/sql-server-2008-r2/cc645934(v=sql.105))。| [表示](/previous-versions/sql/sql-server-2008-r2/cc645934(v=sql.105)) |
|**30009**: 内部エラーが発生しました。|SQL Server インスタンスおよびデータベースの検出中に内部エラーが発生しました。 |問題が解決しない場合は、Microsoft サポートにお問い合わせください。| - |
|**30010**: データベースが見つかりません。|選択されたサーバー インスタンスからデータベースが見つかりません。|SQL データベースを検出できるように、アプライアンス上で指定された資格情報またはアカウントに sysadmin ロールを付与してください。| - |
|**30011**: SQL インスタンスまたはデータベースの評価中に内部エラーが発生しました。|評価の実行中に内部エラーが発生しました。|問題が解決しない場合は、Microsoft サポートにお問い合わせください。| - |
|**30012**: SQL 接続できませんでした。|1. サーバー上のファイアウォールで接続が拒否されました。<br/>2. SQL Server Browser サービス (sqlbrowser) が開始されていません。<br/>3. おそらくサーバーが起動していないことが原因で、SQL Server がクライアント要求に応答しませんでした。<br/>4. SQL Server クライアントがサーバーに接続できません。 このエラーは、サーバーがリモート接続を受け入れるように構成されていないことが原因で発生することがあります。<br/>5. SQL Server クライアントがサーバーに接続できません。 このエラーは、クライアントがサーバー名を解決できないか、サーバー名が間違っていることが原因で発生することがあります。<br/>6. TCP または名前付きパイプ プロトコルが有効ではありません。<br/>7. 指定された SQL Server インスタンス名が有効ではありません。|接続の問題のトラブルシューティングを行うには、[こちらの対話型ユーザー ガイド](https://go.microsoft.com/fwlink/?linkid=2153317)をご利用ください。 ガイドに従った後、サービスでデータが更新されるまで 24 時間お待ちください。 引き続き問題が発生する場合は、Microsoft サポートにお問い合わせください。| [表示](https://go.microsoft.com/fwlink/?linkid=2153317) |
|**30013**: SQL Server インスタンスへの接続確立中にエラーが発生しました。|1. SQL Server 名をアプライアンスから解決できません。<br/>2. SQL Server でリモート接続が許可されません。|アプライアンスから SQL Server に ping を実行できる場合は、24 時間待ってから、この問題が自動的に解決されるかどうかを調べてください。 そうではない場合は、Microsoft サポートにお問い合わせください。 [詳細については、こちらを参照してください](/sql/relational-databases/errors-events/mssqlserver-53-database-engine-error)。| [表示](/sql/relational-databases/errors-events/mssqlserver-53-database-engine-error) |
|**30014**: ユーザー名またはパスワードが無効です。| このエラーは、無効なパスワードまたはユーザー名を含む認証の失敗が原因で発生する可能性があります。|ユーザー名とパスワードが有効な資格情報を指定してください。 [詳細については、こちらを参照してください](/sql/relational-databases/errors-events/mssqlserver-18456-database-engine-error)。| [表示](/sql/relational-databases/errors-events/mssqlserver-18456-database-engine-error) |
|**30015**: SQL Server インスタンスの検出中に内部エラーが発生しました。|SQL Server インスタンスの検出中に内部エラーが発生しました。|問題が解決しない場合は、Microsoft サポートにお問い合わせください。| - |
|**30016**: タイムアウトが発生したため、インスタンス '%Instance;' への接続に失敗しました。| この問題は、サーバーのファイアウォールによる接続の拒否が原因で発生することがあります。|SQL Server のファイアウォールが接続を受け入れるように構成されているかどうかを確認します。 エラーが解決しない場合は、Microsoft サポートにお問い合わせください。 [詳細については、こちらを参照してください](/sql/relational-databases/errors-events/mssqlserver-neg2-database-engine-error)。| [表示](/sql/relational-databases/errors-events/mssqlserver-neg2-database-engine-error) |
|**30017**: 内部エラーが発生しました。|ハンドルされていない例外です。|問題が解決しない場合は、Microsoft サポートにお問い合わせください。| - |
|**30018**: 内部エラーが発生しました。|SQL インスタンスの一時 DB サイズやファイル サイズなどのデータを収集中に内部エラーが発生しました。|24 時間お待ちください。問題が解決しない場合は、Microsoft サポートにお問い合わせください。| - |
|**30019**: 内部エラーが発生しました。|データベースやインスタンスのメモリ使用率などのパフォーマンス メトリックを収集中に内部エラーが発生しました。|24 時間お待ちください。問題が解決しない場合は、Microsoft サポートにお問い合わせください。| - |

## <a name="common-web-apps-discovery-errors"></a>Web アプリの検出に関する一般的なエラー

Azure Migrate では、オンプレミスのマシンで実行されている ASP.NET Web アプリの検出がサポートされており、これには Azure Migrate: Discovery and Assessment を使用します。 現在、Web アプリの検出は VMware でのみサポートされています。 始めるには、[検出](tutorial-discover-vmware.md)に関するチュートリアルを参照してください。

Web アプリの一般的な検出エラーを次の表にまとめました。

| **Error** | **原因** | **操作** |
|--|--|--|
| **40001:** IIS 管理コンソール機能が有効になっていません。 | IIS Web アプリの検出では、IIS のローカル バージョンに付属している管理 API を使用して IIS 構成を読み取ります。 この API は、IIS の IIS 管理コンソール機能が有効になっている場合に使用できます。 この機能が有効になっていないか、OS が IIS Web アプリの検出でサポートされているバージョンではありません。| IIS 管理コンソール機能 (管理ツールの一部) を含む Web サーバー (IIS) のロールが確実に有効になっており、サーバー OS が Windows Server 2008 R2 以降のバージョンであるようにします。|
| **40002:** アプライアンスからサーバーに接続できません。 | ログイン資格情報が無効であるか、マシンを使用できないため、サーバーへの接続に失敗しました。 | サーバーに指定されたログイン資格情報が正しいこと、およびサーバーがオンラインであり WS-Management PowerShell のリモート接続を受け入れていることを確認します。 |
| **40003:** 資格情報が無効なため、サーバーに接続できません。 | ログイン資格情報が無効であるため、サーバーへの接続に失敗しました。 | サーバーに対して指定されたログイン資格情報が確実に正しく、WS-Management PowerShell のリモート処理が有効であるようにします。 |
| **40004:** IIS 構成にアクセスできません。 | アクセス許可がないか、アクセス許可が不十分です。 | サーバーに対して指定されたユーザー資格情報が管理者レベルの資格情報であり、ユーザーが IIS ディレクトリ (%windir%\System32\inetsrv) および IIS サーバー構成ディレクトリ (%windir%\System32\inetsrv\config) の下にあるファイルにアクセスする権限を持っていることをご確認ください。 |
| **40005:** IIS 検出を完了できません。 | VM での検出を完了できませんでした。 この問題は、サーバー上の構成へのアクセスに関する問題が原因で発生する場合があります。 エラーは '%detailedMessage;' でした。 | サーバーに対して指定されたユーザー資格情報が管理者レベルの資格情報であり、ユーザーが IIS ディレクトリ (%windir%\System32\inetsrv) および IIS サーバー構成ディレクトリ (%windir%\System32\inetsrv\config) の下にあるファイルにアクセスする権限を持っていることをご確認ください。 次に、エラーの詳細について Microsoft サポートにお問い合わせください。 |
| **40006:** 未分類の例外です。 | 新しいエラーのシナリオです。 | エラーの詳細とログについて Microsoft サポートにお問い合わせください。 ログは、アプライアンス サーバーのパス C:\ProgramData\Microsoft Azure\Logs にあります。 |
| **40007:** Web サーバーの Web アプリが見つかりません。 | この Web サーバーには、ホストされているアプリケーションがありません。 | Web サーバーの構成を確認します。 |

## <a name="next-steps"></a>次のステップ

[VMware](how-to-set-up-appliance-vmware.md)、[Hyper-V](how-to-set-up-appliance-hyper-v.md)、または[物理サーバー](how-to-set-up-appliance-physical.md)用にアプライアンスを設定します。
