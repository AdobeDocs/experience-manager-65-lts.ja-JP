---
title: AEM Forms ワークフローの変数
description: 変数を作成、変数の値を設定し、AEM Forms Workflow ステップで使用してください。
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 1a0d00f9-45f7-45af-ab34-d1c164980abb
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '2055'
ht-degree: 99%

---

# AEM Forms ワークフローの変数{#variables-in-aem-forms-workflows}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/variable-in-aem-workflows.html?lang=ja) |
| AEM 6.5 | この記事 |

ワークフローモデルの変数は、そのデータタイプに基づいて値を格納する方法です。ワークフローステップで変数の名前を使用して、変数に格納されている値を取得できます。変数名を使用して、ルーティング上の決定を行う式を定義することもできます。

AEM ワークフローモデルでは、次のことができます。

* 保存する情報タイプに基づいて、データタイプの [変数を作成します](../../forms/using/variable-in-aem-workflows.md#create-a-variable)。
* [変数の値を設定する](../../forms/using/variable-in-aem-workflows.md#set-a-variable)には、「変数を設定する」ワークフローステップを使用します。
* すべての AEM Forms Workflow ステップで[変数を使用して](../../forms/using/variable-in-aem-workflows.md#use-a-variable)格納された値を取得し、OR 分割ステップおよび移動ステップでルーティング式を定義します。

変数は、既存の [MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) インターフェイスの拡張です。ECMAScript で [MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) を使用すると、変数を使用して保存されたメタデータにアクセスできます。

## 変数の作成 {#create-a-variable}

変数は、ワークフローモデルのサイドキックにある「変数」セクションを使用して作成します。AEM ワークフロー変数は、次のデータタイプをサポートしています。

* **プリミティブデータタイプ**：Long、Double、Boolean、Date、String
* **複雑なデータタイプ**：[ドキュメント](https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html)、[XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html?lang=ja)、[JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html?lang=ja)、フォームデータモデルインスタンス。

>[!NOTE]
>
>ワークフローでは、日付型変数に対して ISO8601 形式のみをサポートします。

ドキュメントとフォームデータモデルのデータタイプには、[AEM Forms アドオンパッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html) が必要です。ArrayList データタイプを使用して、変数コレクションを作成します。すべてのプリミティブデータタイプと複合データタイプに対して ArrayList 変数を作成できます。例えば、ArrayList 変数を作成し、サブタイプとして String を選択して、変数を使用して複数の文字列値を格納します。

変数を作成するには、次の手順を実行します。

1. AEM インスタンスで、![ツール](/help/forms/using/assets/hammer.png)／ワークフロー／モデルに移動します。
1. 「**[!UICONTROL 作成]**」を選択し、ワークフローモデルのタイトルとオプション名を指定します。モデルを選択し、「**[!UICONTROL 編集]**」を選択します。
1. ワークフローモデルのサイドキックにある使用可能な変数アイコンを選択し、「**[!UICONTROL 変数を追加]**」を選択します。

   ![変数を追加](assets/variables_add_variable_new.png)

1. 「変数の追加」ダイアログで、名前を指定し、変数のタイプを選択します。
1. 「**[!UICONTROL タイプ]**」ドロップダウンリストからデータタイプを選択し、次の値を指定します。

   * プリミティブデータタイプ - 変数のオプションのデフォルト値を指定します。
   * JSON または XML - オプションの JSON または XML スキーマパスを指定します。システムは、このスキーマで使用可能なプロパティを別の変数にマッピングおよび保存しながら、スキーマパスを検証します。
   * フォームデータモデル - フォームデータモデルのパスを指定します。
   * ArrayList - コレクションのサブタイプを指定します。

1. 変数の説明（オプション）を指定し、![done_icon](assets/done_icon.png) を選択して変更を保存します。変数は、左側のペインで使用可能なリストに表示されます。

変数を作成する場合、次のプラクティスをお勧めします。

* ワークフローで必要な数の変数を作成します。ただし、データベースのリソースを確保するため、必要最低限の変数を使用し、必要に応じて変数を再利用してください。
* 変数では大文字と小文字が区別されます。ワークフローで変数を参照する場合には同じように大文字と小文字を区別してください。
* 変数名に特殊文字を使用しないでください。

## 変数の設定 {#set-a-variable}

「変数を設定」ステップを使用して、変数の値を設定し、値が設定される順序を定義できます。変数は、変数の設定ステップで変数のマッピングがリストされている順序で設定されます。

変数値を変更すると、変更が発生したプロセスのインスタンスのみに影響します。例えば、ワークフローが開始され変数データが変更されると、変更はそのワークフローのインスタンスのみに影響します。変更は、以前に開始された、または後で開始されたワークフローの他のインスタンスには影響しません。

変数のデータタイプに応じて、次のオプションを使用して変数の値を設定できます。

* **リテラル：**&#x200B;指定する値が正確に分かっている場合は、このオプションを使用します。

* **式：**&#x200B;使用する値が式に基づいて計算される場合は、このオプションを使用します。式は、提供された式エディターで作成されます。

* **JSON ドット表記：**&#x200B;このオプションを使用して、JSON または FDM タイプの変数から値を取得します。
* **XPATH：**&#x200B;このオプションを使用して XML タイプ変数から値を取得します。

* **ペイロード基準：**&#x200B;変数として格納する値が、ペイロードを基準としたパスにある場合は、このオプションを使用します。

* **絶対パス：**&#x200B;変数として格納する値が絶対パスにある場合は、このオプションを使用します。

また、JSON DOT 表記法または XPATH 表記法を使用して、JSON または XML タイプの変数の特定の要素を更新することもできます。

### 変数間マッピングの追加 {#add-mapping-between-variables}

変数間のマッピングを追加するには、次の手順を実行します。

1. ワークフローの編集ページで、ワークフローモデルのサイドキックにある「ステップ」アイコンを選択します。
1. 「**変数を設定**」ステップをワークフローエディターにドラッグ＆ドロップし、ステップを選択して ![configure_icon](assets/configure_icon.png)（設定）を選択します。
1. 「変数を設定」ダイアログで、 **[!UICONTROL マッピング]**／**[!UICONTROL マッピングを追加]** を選択します。
1. 「**変数のマップ**」セクションで、データを格納する変数を選択し、マッピングモードを選択して、変数に格納する値を指定します。マッピングモードは、変数のタイプによって異なります。
1. より多くの変数をマップして、意味のある式を作成します。![done_icon](assets/done_icon.png) を選択して、変更を保存します。

### 例 1：XML 変数をクエリして、文字列変数の値を設定 {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

XML タイプの変数を選択し、XML ファイルを格納します。XML 変数をクエリして、XML ファイルで使用可能なプロパティの文字列変数の値を設定します。「**XML 変数に XPATH を指定**」フィールドを使用して、文字列変数に格納するプロパティを定義します。

この例では、**formdata** XML 変数を選択して **cc-app.xml** ファイルを格納します。**formdata** 変数をクエリして、**emailaddress** 文字列変数の値を設定し、**cc-app.xml** ファイルで使用できる **emailAddress** プロパティの値を格納します。

### 例 2：式を使用して、他の変数に基づいて値を格納 {#example2}

式を使用して変数の和を計算し、結果を変数に格納します。

この例では、式エディターを使用して式を定義し、**assetscost** 変数と **balanceamount** 変数の和を計算し、その結果を **totalvalue** 変数に格納します。

## 式エディターの使用 {#use-expression-editor}

実行時の変数の値を計算するのにも式を使用します。変数は、式を定義する式エディターを提供します。

式エディターを使用して、次の操作を行います。

* 他のワークフロー変数、数値または数式を使用して、変数の値を設定します。
* ワークフロー変数、文字列、数値、または式を数式内で使用
* 変数の値を設定する条件を追加します。
* 条件の間に演算子を追加します。

![式エディター](assets/variables_expression_editor_new.png)

これは、次の変更を加えたアダプティブフォームのルールエディターに基づいています。変数のルールエディター：

* 関数はサポートしていません。
* ルールの概要を表示するための UI は提供していません。
* コードエディターはありません。
* オブジェクトの値の有効化と無効化はサポートしていません。
* オブジェクトのプロパティの設定はサポートしていません。
* Web サービスの呼び出しはサポートしていません。

詳しくは、[アダプティブフォームのルールエディター](../../forms/using/rule-editor.md)を参照してください。

## 変数を使用 {#use-a-variable}

変数を使用して、入力と出力を取得したり、ステップの結果を保存したりできます。ワークフローエディターには、次の 2 種類のワークフローステップが用意されています。

* 変数をサポートするワークフローステップ
* 変数をサポートしないワークフローステップ

### 変数をサポートするワークフローステップ {#workflow-steps-with-support-for-variables}

移動ステップ、OR‧分割ステップ、およびすべての‧AEM‧Forms‧Workflow‧ステップでは、変数をサポートしています。

#### OR 分割ステップ {#or-split-step}

OR 分割は、ワークフロー内に分割を作成し、以降は 1 つの分岐だけがアクティブになります。これを使用すると、ワークフローに条件付き処理パスを導入できます。必要に応じて、各分岐にワークフローステップを追加できます。

分岐のルーティング式は、ルール定義、ECMA スクリプト、または外部スクリプトを使用して定義できます。

変数を使用して、式エディターを使用したルーティング式を定義できます。OR 分割ステップでルーティング式を使用する方法について詳しくは、「[OR 分割ステップ](/help/sites-developing/workflows-step-ref.md#or-split)」を参照してください。

この例では、ルーティング式を定義する前に、[例 2 ](../../forms/using/variable-in-aem-workflows.md#example2)を使用して **totalvalue** 変数の値を設定します。**totalvalue** 変数の値が 50000 より大きい場合、分岐 1 はアクティブになります。同様に、**totalvalue** 変数の値が 50000 未満の場合に、Branch 2 をアクティブにするルールを定義できます。

同様に、外部スクリプトパスを選択するか、ルーティング式の ECMA スクリプトを指定して、アクティブな分岐を評価します。「**[!UICONTROL 分岐名の変更]**」を選択して、分岐に別名を指定します。

その他の例については、[ワークフローモデルの作成](../../forms/using/aem-forms-workflow.md#create-a-workflow-model)を参照してください。

#### 移動ステップ {#go-to-step}

**移動ステップ**&#x200B;を使用すると、ルーティング式の結果に応じて、ワークフローモデル内で実行する次のステップを指定できます。

OR 分割ステップと同様に、ルール定義、ECMA スクリプト、または外部スクリプトを使用して、移動ステップのルーティング式を定義できます。

変数を使用して、式エディターを使用したルーティング式を定義できます。移動ステップでルーティング式を使用する方法について詳しくは、「[移動ステップ](/help/sites-developing/workflows-step-ref.md#goto-step)」を参照してください。

![移動のルール](assets/variables_goto_rule1_new.png)

この例では、**actiontaken** 変数の値が **Need more info** に等しい場合、移動ステップは次のステップとして「Review Credit Card Application」を指定します。

移動ステップでのルール定義の使用するその他の例については、[For ループのシミュレーション](/help/sites-developing/workflows-step-ref.md#simulateforloop)を参照してください。

#### Forms ワークフロー中心のワークフローステップ {#forms-workflow-centric-workflow-steps}

すべての AEM Forms Workflow ステップは、変数をサポートします。詳しくは、[OSGi での Forms 中心のワークフローを参照してください](../../forms/using/aem-forms-workflow-step-reference.md)。

### 変数をサポートしないワークフローステップ {#workflow-steps-without-support-for-variables}

[MetaDataMap](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) インターフェイスを使用して、変数をサポートしないワークフロー手順の変数にアクセスできます。

#### 変数値の取得 {#retrieve-the-variable-value}

ECMA スクリプトで次の API を使用して、データタイプに基づいて既存の変数の値を取得します。

| 変数データタイプ | API |
|---|---|
| プリミティブ（Long、Double、Boolean、Date、String） | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| ドキュメント | Packages.com.adobe.aemfd.docmanager.Document doc = workItem.getWorkflowData().getMetaDataMap().get(&quot;docVar&quot;, Packages.com.adobe.aemfd.docmanager.Document.class); |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| フォームデータモデル | Packages.com.adobe.aem.dermis.api.FormDataModelInstance fdmObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

ドキュメントおよびフォームデータモデルの変数データタイプには、[AEM Forms アドオンパッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)が必要です。

**例**

次の API を使用して、string データタイプの値を取得します。

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 変数値の更新 {#update-the-variable-value}

ECMA スクリプトで次の API を使用して、変数の値を更新します。

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**例**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

**Salary** 変数の値を 50000 に更新します。

### ワークフローを呼び出す変数の設定 {#apiinvokeworkflow}

API を使用して変数を設定し、それらを渡してワークフローインスタンスを呼び出すことができます。

[workflowSession.startWorkflows](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) は、モデル、wfData、metaData を引数として使用します。MetaDataMap を使用して変数の値を設定します。

この API では、 **variableName** 変数は metaData.put(variableName, value) を使用して **value** に設定されます。

```javascript
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

**例**

**doc** ドキュメントオブジェクトをパス (&quot;a/b/c&quot;) に初期化し、**docVar** 変数の値をドキュメントオブジェクトに格納されているパスに設定します。

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

### ワークフロー変数を使用して、機密性の高いユーザーデータを JCR 外に保存 {#jcr-independent-persistance}

Forms Workflow を使用して処理されるデータには、個人を特定できる情報や個人情報などの機密性の高いユーザーデータが含まれることがあります。企業は、様々なワークフローステップで処理される（およびワークフロー変数を使用して渡される）データを、JCR ストレージから所有および管理する外部データストアに格納することを選択できます。外部ストレージへのワークフローデータの保持について詳しくは、[顧客が所有するデータストアに対するワークフロー変数の使用](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore)を参照してください。
[!DNL Adobe Experience Manager] は、ワークフロー API [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer) を提供して、外部の Azure BLOB ストレージにワークフロー変数を保存します。API の使用について詳しくは、[ワークフロー変数を使用して、機密データをパラメータ化し、外部データストアに保存する](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables)を参照してください。

## 変数の編集 {#edit-a-variable}

1. ワークフローの編集ページで、ワークフローモデルのサイドキックにある「変数」アイコンを選択します。左側のペインの「変数」セクションには、既存のすべての変数が表示されます。
1. 編集する変数名の横にある「![編集](assets/edit.png)」アイコンを選択します。
1. 変数情報を編集し、![done_icon](assets/done_icon.png) を選択して変更を保存します。変数の「**[!UICONTROL 名前]**」フィールドと「**[!UICONTROL タイプ]**」フィールドは編集できません。

## 変数の削除 {#delete-a-variable}

変数を削除する前に、ワークフローから変数のすべての参照を削除します。この変数がワークフローで使用されていないことを確認します。

以下の手順を実行し、変数を削除します。

1. ワークフローの編集ページで、ワークフローモデルのサイドキックにある「変数」アイコンを選択します。左側のペインの「変数」セクションには、既存のすべての変数が表示されます。
1. 削除する変数名の横にある「削除」アイコンを選択します。
1. ![done_icon](assets/done_icon.png) を選択して、変数を確認して削除します。

## 参照 {#references}

AEM Forms Workflow ステップで変数を使用するその他の例については、[AEM ワークフローの変数](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/variables-aem-workflow/introduction.html?lang=ja)を参照してください。
