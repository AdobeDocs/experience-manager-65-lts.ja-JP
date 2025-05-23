---
title: AEM Forms ワークフローへのログイン
description: AEM Forms Workflow の問題をデバッグし、AEM Forms Workflow のデバッグログを有効にしてログを表示する方法について説明します。
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 90a44cab-3ecf-4a71-95d4-e8ce2d996980
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 100%

---

# AEM Forms ワークフローへのログイン{#logging-in-aem-forms-workflows}

Forms Workflow の手順では、ワークフローに関する問題をデバッグするのに便利な詳細なログを提供しています。ログを表示するには AEM Formsワークフローのデバッグログを有効にします。

デフォルトでは、すべてのログ情報は */crx-repository/logs/* ディレクトリに保存されている **error.log** ファイルにあります。

Forms ワークフローのデバッグログには、次の内容が含まれます。

* 各ワークフロー手順のエントリ。次に例を示します。\
  `[DEBUG] "Executing Invoke DDX Process step"`

* 各ワークフロー手順の終了。次に例を示します。\
  `[DEBUG] "Successfully finished Invoke DDX Process step"`

* サービス呼び出しメッセージ。次に例を示します。\
  `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* サービス終了メッセージ。次に例を示します。\
  `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* メタデータマップから読み取られた変数。次に例を示します。\
  `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* JCR リポジトリで書き込まれた変数。次に例を示します。

  ```verilog
     [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
  ```

* 完全なスタックトレースを含む例外メッセージ。次に例を示します。\
  `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* 動的な手順のメタデータパラメーター。次に例を示します。

  ```verilog
  [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
   [DEBUG] Locale to be used for Document of Record is <locale>
  ```

次の例は、「ドキュメントに署名」手順のログを示しています。

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

ログを使用して次の内容を評価します。

* 正しい Adobe Sign 設定を使用していること。
* 契約を正常に作成したら Adobe Sign サービスが終了すること。
* 「ドキュメントに署名」手順が成功メッセージとともに終了すること。

例外がある場合は、完全なスタックトレースを表示して、エラーの原因を評価できます。

## AEM Forms ワークフローのデバッグログの有効化 {#enable-debug-logging-for-aem-forms-workflows}

AEM Forms Workflow のデバッグログを有効にするには、次の手順を実行します。

1. AEM web コンソール設定マネージャーに移動します。

   https://&#39;[server]:[port]&#39;/system/console/configMgr

1. **[!UICONTROL Sling]**／**[!UICONTROL ログのサポート]**&#x200B;を選択します。
1. 「**[!UICONTROL 新規ロガーを追加]**」を選択します。
1. **[!UICONTROL デバッグ]**&#x200B;を&#x200B;**[!UICONTROL ログレベル]**&#x200B;として選択します。
1. ログファイルの場所を指定します。ログファイルのデフォルトの場所は *logs\error.log* です。
1. **[!UICONTROL ロガー]**&#x200B;列でパッケージの名前を **com.adobe.granite.workflow.core** として指定します。

   これらの手順を実行すると、**com.adobe.granite.workflow.core** パッケージのデバッグログを格納できるようになります。**[!UICONTROL +]** を選択して次のパッケージ名をリストに追加します。

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
