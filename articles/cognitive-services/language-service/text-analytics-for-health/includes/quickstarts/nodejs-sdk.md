---
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: language-service
ms.topic: include
ms.date: 11/02/2021
ms.author: aahi
ms.custom: devx-track-js, ignite-fall-2021
ms.openlocfilehash: 1a1858d71e70c8f98fec561ee07bfdfbc21b7bac
ms.sourcegitcommit: 106f5c9fa5c6d3498dd1cfe63181a7ed4125ae6d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/02/2021
ms.locfileid: "131090081"
---
[リファレンスのドキュメント](/javascript/api/overview/azure/ai-text-analytics-readme?preserve-view=true&view=azure-node-latest) | [ライブラリのソース コード](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/textanalytics/ai-text-analytics) | [パッケージ (NPM)](https://www.npmjs.com/package/@azure/ai-text-analytics/v/5.1.0) | [サンプル](https://github.com/Azure/azure-sdk-for-js/tree/main/sdk/textanalytics/ai-text-analytics/samples)

## <a name="prerequisites"></a>前提条件

* Azure サブスクリプション - [無料アカウントを作成します](https://azure.microsoft.com/free/cognitive-services)
* 最新バージョンの [Node.js](https://nodejs.org/)。
* Azure サブスクリプションを入手したら、Azure portal で<a href="https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesTextAnalytics"  title="言語リソースを作成する"  target="_blank">言語リソースを作成</a>して、キーとエンドポイントを取得します。 デプロイされたら、 **[リソースに移動]** をクリックします。
    * 対象のアプリケーションを API に接続するには、作成したリソースのキーとエンドポイントが必要です。 このクイックスタートで後に示すコードに、自分のキーとエンドポイントを貼り付けます。
    * Free 価格レベル (`F0`) を使用してサービスを試用し、後から運用環境用の有料レベルにアップグレードすることができます。
* 分析機能を使うには、Standard (S) 価格レベルの言語リソースが必要です。

## <a name="setting-up"></a>設定

### <a name="create-a-new-nodejs-application"></a>新しい Node.js アプリケーションを作成する

コンソール ウィンドウ (cmd、PowerShell、Bash など) で、ご利用のアプリ用に新しいディレクトリを作成し、そこに移動します。 

```console
mkdir myapp 

cd myapp
```

`npm init` コマンドを実行し、`package.json` ファイルを使用して node アプリケーションを作成します。 

```console
npm init
```

### <a name="install-the-client-library"></a>クライアント ライブラリをインストールする

NPM パッケージをインストールします。

```console
npm install --save @azure/ai-text-analytics@5.1.0
```

## <a name="code-example"></a>コードの例

ファイルを開き、下のコードをコピーします。 `key` 変数はリソースのキーに置き換え、`endpoint` 変数はリソースのエンドポイントに置き換えてください。 

[!INCLUDE [find the key and endpoint for a resource](../../../includes/find-azure-resource-info.md)]

```javascript
"use strict";

const { TextAnalyticsClient, AzureKeyCredential } = require("@azure/ai-text-analytics");
const key = '<paste-your-key-here>';
const endpoint = '<paste-your-endpoint-here>';
// Authenticate the client with your key and endpoint
const textAnalyticsClient = new TextAnalyticsClient(endpoint, new AzureKeyCredential(key));

// Example method for extracting information from healthcare-related text 
async function healthExample(client) {
    console.log("== Recognize Healthcare Entities Sample ==");

    const documents = [
        "Prescribed 100mg ibuprofen, taken twice daily."
    ];
    const poller = await client.beginAnalyzeHealthcareEntities(documents, "en", {
        includeStatistics: true
    });

    poller.onProgress(() => {
        console.log(
            `Last time the operation was updated was on: ${poller.getOperationState().lastModifiedOn}`
        );
    });
    console.log(
        `The analyze healthcare entities operation was created on ${poller.getOperationState().createdOn
        }`
    );
    console.log(
        `The analyze healthcare entities operation results will expire on ${poller.getOperationState().expiresOn
        }`
    );

    const results = await poller.pollUntilDone();

    for await (const result of results) {
        console.log(`- Document ${result.id}`);
        if (!result.error) {
            console.log("\tRecognized Entities:");
            for (const entity of result.entities) {
                console.log(`\t- Entity "${entity.text}" of type ${entity.category}`);
            }
            if (result.entityRelations && (result.entityRelations.length > 0)) {
                console.log(`\tRecognized relations between entities:`);
                for (const relation of result.entityRelations) {
                    console.log(
                        `\t\t- Relation of type ${relation.relationType} found between the following entities:`
                    );
                    for (const role of relation.roles) {
                        console.log(`\t\t\t- "${role.entity.text}" with the role ${role.name}`);
                    }
                }
            }
        } else console.error("\tError:", result.error);
    }
}

healthExample(textAnalyticsClient).catch((err) => {
    console.error("The sample encountered an error:", err);
});
```

### <a name="output"></a>出力

```console
- Document 0
    Recognized Entities:
    - Entity "100mg" of type Dosage
    - Entity "ibuprofen" of type MedicationName
    - Entity "twice daily" of type Frequency
    Recognized relations between entities:
        - Relation of type DosageOfMedication found between the following entities:   
                - "100mg" with the role Dosage
                - "ibuprofen" with the role Medication
        - Relation of type FrequencyOfMedication found between the following entities:
                - "ibuprofen" with the role Medication
                - "twice daily" with the role Frequency
```
