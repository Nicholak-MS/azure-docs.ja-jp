---
title: 'クイックスタート: Python daemon からの Microsoft Graph の呼び出し | Azure'
titleSuffix: Microsoft identity platform
description: このクイックスタートでは、Python プロセスでアクセス トークンを取得し、Microsoft ID プラットフォームによって保護されている API を、アプリ自体の ID を使用して呼び出す方法について説明します
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: portal
ms.workload: identity
ms.date: 01/10/2022
ROBOTS: NOINDEX
ms.author: jmprieur
ms.custom: aaddev, identityplatformtop40, devx-track-python, "scenarios:getting-started", "languages:Python", mode-api
ms.openlocfilehash: c762f47fe93780c6f405b3cabc546ecd6fec8f16
ms.sourcegitcommit: 3f20f370425cb7d51a35d0bba4733876170a7795
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/27/2022
ms.locfileid: "137803744"
---
# <a name="quickstart-acquire-a-token-and-call-microsoft-graph-api-from-a-python-console-app-using-apps-identity"></a>クイック スタート:トークンを取得し、Python コンソール アプリからアプリの ID を使用して Microsoft Graph API を呼び出す

このクイックスタートでは、Python アプリケーションでアプリの ID を使ってアクセス トークンを取得して、Microsoft Graph API を呼び出し、ディレクトリ内の[ユーザーの一覧](/graph/api/user-list)を表示する方法を示すコード サンプルをダウンロードして実行します。 このコード サンプルでは、ユーザーの ID ではなく、アプリケーション ID を使用して、無人のジョブまたは Windows サービスを実行する方法を示します。 

## <a name="prerequisites"></a>前提条件

このサンプルを実行するには、以下が必要です。

- [Python 2.7 以降](https://www.python.org/downloads/release/python-2713)または [Python 3 以降](https://www.python.org/downloads/release/python-364/)
- [MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python)

> [!div class="sxs-lookup"]
### <a name="download-and-configure-the-quickstart-app"></a>クイックスタート アプリをダウンロードして構成する

#### <a name="step-1-configure-your-application-in-azure-portal"></a>手順 1:Azure portal でのアプリケーションの構成
このクイックスタート用サンプル コードを動作させるには、クライアント シークレットを作成し、Graph API の **User.Read.All** アプリケーションのアクセス許可を追加します。
> [!div class="nextstepaction"]
> [これらの変更を行います]()

> [!div class="alert alert-info"]
> ![構成済み](media/quickstart-v2-netcore-daemon/green-check.png) アプリケーションはこれらの属性で構成されています。

#### <a name="step-2-download-the-python-project"></a>手順 2:Python プロジェクトのダウンロード

> [!div class="sxs-lookup nextstepaction"]
> [コード サンプルをダウンロードします](https://github.com/Azure-Samples/ms-identity-python-daemon/archive/master.zip)

> [!div class="sxs-lookup"]
> > [!NOTE]
> > `Enter_the_Supported_Account_Info_Here`

#### <a name="step-3-admin-consent"></a>手順 3:管理者の同意

この時点でアプリケーションを実行すると、*HTTP 403 - Forbidden* エラー "`Insufficient privileges to complete the operation`" が表示されます。 これは、すべての "*アプリ専用のアクセス許可*" には管理者の同意が必要であるために発生します。ディレクトリのグローバル管理者にお使いのアプリケーションに同意してもらう必要があります。 ご自身のロールに応じて、次のオプションのいずれかを選択します。

##### <a name="global-tenant-administrator"></a>グローバル テナント管理者

グローバル管理者の場合は、 **[API のアクセス許可]** ページに移動し、 **[Enter_the_Tenant_Name_Here に管理者の同意を与えます]** を選択します。
> [!div id="apipermissionspage"]
> [[API のアクセス許可] ページに移動する]()

##### <a name="standard-user"></a>標準ユーザー

テナントの標準ユーザーの場合は、お使いのアプリケーションに管理者の同意を与えるようグローバル管理者に依頼してください。 これを行うには、次の URL を管理者に知らせます。

```url
https://login.microsoftonline.com/Enter_the_Tenant_Id_Here/adminconsent?client_id=Enter_the_Application_Id_Here
```


#### <a name="step-4-run-the-application"></a>手順 4:アプリケーションの実行

このサンプルの依存関係を 1 回インストールする必要があります。

```console
pip install -r requirements.txt
```

次に、コマンド プロンプトまたはコンソールを使用して、アプリケーションを実行します。

```console
python confidential_client_secret_sample.py parameters.json
```

コンソール出力には、Azure AD ディレクトリ内のユーザーの一覧を表すいくつかの Json フラグメントが表示されます。

> [!IMPORTANT]
> このクイック スタート アプリケーションは、クライアント シークレットを使用して、それ自体を機密クライアントとして識別します。 クライアント シークレットはプロジェクト ファイルにプレーン テキストとして追加されるため、セキュリティ上の理由から、アプリケーションを運用アプリケーションと見なす前に、クライアント シークレットの代わりに証明書を使用することをお勧めします。 証明書の使用方法の詳細については、このサンプルと同じ GitHub リポジトリの 2 つ目のフォルダー **2-Call-MsGraph-WithCertificate** にある [これらの手順](https://github.com/Azure-Samples/ms-identity-python-daemon/blob/master/2-Call-MsGraph-WithCertificate/README.md)を参照してください。

## <a name="more-information"></a>詳細情報

### <a name="msal-python"></a>MSAL Python

[MSAL Python](https://github.com/AzureAD/microsoft-authentication-library-for-python) は、ユーザーをサインインし、Microsoft ID プラットフォームによって保護されている API にアクセスするトークンを要求するために使用するライブラリです。 説明したとおり、このクイック スタートでは、委任されたアクセス許可ではなく、アプリケーション自体の ID を使用してトークンを要求しています。 ここで使用される認証フローは、" *[クライアント資格情報 OAuth フロー](v2-oauth2-client-creds-grant-flow.md)* " と呼ばれます。 デーモン アプリでの MSAL Python の使用方法の詳細については、[この記事](scenario-daemon-overview.md)を参照してください。

 MSAL Python は、次の pip コマンドを実行してインストールできます。

```powershell
pip install msal
```

### <a name="msal-initialization"></a>MSAL の初期化

MSAL への参照を追加するには、次のコードを追加します。

```Python
import msal
```

続いて、次のコードを使用して MSAL を初期化します。

```Python
app = msal.ConfidentialClientApplication(
    config["client_id"], authority=config["authority"],
    client_credential=config["secret"])
```

> | 各値の説明: |説明 |
> |---------|---------|
> | `config["secret"]` | Azure portal 上でアプリケーションに対して作成されるクライアント シークレット。 |
> | `config["client_id"]` | Azure portal に登録されているアプリケーションの "**アプリケーション (クライアント) ID**"。 この値は、Azure portal のアプリの **[概要]** ページで確認できます。 |
> | `config["authority"]`    | ユーザーが認証するための STS エンドポイント。 通常、パブリック クラウド上では `https://login.microsoftonline.com/{tenant}` です。{tenant} はご自分のテナントの名前またはテナント ID です。|

詳細については、[`ConfidentialClientApplication` のリファレンス ドキュメント](https://msal-python.readthedocs.io/en/latest/#confidentialclientapplication)を参照してください。

### <a name="requesting-tokens"></a>トークンの要求

アプリの ID を使用してトークンを要求するには、`AcquireTokenForClient` メソッドを使用します。

```Python
result = None
result = app.acquire_token_silent(config["scope"], account=None)

if not result:
    logging.info("No suitable token exists in cache. Let's get a new one from AAD.")
    result = app.acquire_token_for_client(scopes=config["scope"])
```

> |各値の説明:| 説明 |
> |---------|---------|
> | `config["scope"]` | 要求されるスコープが含まれています。 機密クライアントの場合は、`{Application ID URI}/.default` のような形式を使用して、要求されるスコープが Azure portal で設定されるアプリ オブジェクト内に静的に定義されたものであることを示す必要があります (Microsoft Graph では、`{Application ID URI}` は `https://graph.microsoft.com` を指します)。 カスタム Web API の場合、`{Application ID URI}` は、Azure portal で **[アプリの登録]** の **[API の公開]** セクションに定義されます。|

詳細については、[`AcquireTokenForClient` のリファレンス ドキュメント](https://msal-python.readthedocs.io/en/latest/#msal.ConfidentialClientApplication.acquire_token_for_client)を参照してください。

[!INCLUDE [Help and support](../../../includes/active-directory-develop-help-support-include.md)]

## <a name="next-steps"></a>次のステップ

デーモン アプリケーションの詳細については、シナリオのランディング ページを参照してください。

> [!div class="nextstepaction"]
> [Web API を呼び出すデーモン アプリケーション](scenario-daemon-overview.md)
