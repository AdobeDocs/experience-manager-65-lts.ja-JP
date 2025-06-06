---
title: アダプティブフォームからフォームデータモデルサービスを呼び出すための API
description: アダプティブフォームフィールド内から WSDL で記述された、web サービスを呼び出す API について説明します。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: e36be2da-af72-485f-87a6-cef6172037c6
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 100%

---

# アダプティブフォームからフォームデータモデルサービスを呼び出すための API {#api-to-invoke-form-data-model-service-from-adaptive-forms}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

## 概要 {#overview}

AEM Forms を使用すると、アダプティブフォームフィールド内からフォームデータモデルで構成されたサービスを呼び出すことで、フォーム作成者はフォームへの記入作業を簡略化および強化することができます。データモデルサービスを呼び出すには、ビジュアルエディターでルールを作成するか、[ルールエディター](/help/forms/using/rule-editor.md)のコードエディターの `guidelib.dataIntegrationUtils.executeOperation` API を使用して JavaScript を指定します。

このドキュメントでは、`guidelib.dataIntegrationUtils.executeOperation` API を使用して JavaScript を記述してサービスを呼び出す方法に焦点を当てています。

## API の使用 {#using-the-api}

`guidelib.dataIntegrationUtils.executeOperation` API は、アダプティブフォームのフィールド内から サービスを呼び出します。API 構文は以下のとおりです。

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

`guidelib.dataIntegrationUtils.executeOperation` API の構造は、サービス操作の詳細を指定します。この構造の構文は以下のとおりです。

```javascript
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

API 構造は、サービス操作の以下の詳細を指定します。

<table>
 <tbody>
  <tr>
   <th>パラメーター</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><code>operationInfo</code></td>
   <td>フォームデータモデルの識別子、操作タイトル、操作名を指定する構造</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>フォームデータモデルへのリポジトリパスをその名前も含めて指定します</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>実行するサービス操作の名前を指定します</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>1 つ以上のフォームオブジェクトをサービス操作の入力引数にマップします</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>1 つ以上のフォームオブジェクトをサービス操作からの出力値にマップしてフォームフィールドを埋め込みます<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>サービス操作の入力引数に基づいて値を返します。コールバック関数として使用されるオプションのパラメーターです。<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>success コールバック関数が入力引数に基づいて出力値を表示できない場合に、エラーメッセージを表示します。コールバック関数として使用されるオプションのパラメーターです。<br /> </td>
  </tr>
 </tbody>
</table>

## サービスを呼び出すスクリプトのサンプル {#sample-script-to-invoke-a-service}

以下のサンプルスクリプトでは、`guidelib.dataIntegrationUtils.executeOperation` API を使用して、`employeeAccount` フォームデータモデルで構成された `getAccountById` サービス操作を呼び出しています。

`getAccountById` 操作は、`empId` 引数の入力値として `employeeID` フォームフィールドにある値を使用し、該当する従業員の名前、口座番号、口座残高を戻します。この出力値は指定されたフォームフィールドに入力されます。例えば、`name` 引数の値は `fullName` フォーム要素に入力され、`accountNumber` 引数の値は `account` フォーム要素に入力されます。

```javascript
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

## コールバック関数での API の使用 {#using-the-api-callback}

コールバック関数で `guidelib.dataIntegrationUtils.executeOperation` API を使用してフォームデータモデルサービスを呼び出すこともできます。API 構文は以下のとおりです。

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

コールバック関数は、`success` および `failure` コールバック関数を持つことができます。

### success コールバック関数と failure コールバック関数を持つサンプルスクリプト {#callback-function-success-failure}

以下のサンプルスクリプトでは、`guidelib.dataIntegrationUtils.executeOperation` API を使用して、`employeeOrder` フォームデータモデルで構成された `GETOrder` サービス操作を呼び出しています。

`GETOrder` 操作は、`Order ID` フォームフィールドの値を `orderId` 引数の入力として受け取り、`success` コールバック関数に注文数量の値を返します。`success` コールバック関数が注文数を返さない場合、`failure` コールバック関数は `Error occured` メッセージを表示します。

>[!NOTE]
>
>`success` コールバック関数を使用する場合、指定したフォームフィールドに出力値が入力されません。

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
