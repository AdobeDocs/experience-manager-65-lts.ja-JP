---
title: Sling アダプターの使用
description: Sling には、適応可能なインターフェイスを実装するオブジェクトを簡単に翻訳するためのアダプターパターンが用意されています。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 7eae83bd-7982-4051-821f-b43f65c5af2b
source-git-commit: cf22b13e0f7c8e66b598f85aab81b022480e60bc
workflow-type: tm+mt
source-wordcount: '1338'
ht-degree: 50%

---

# Sling アダプターの使用{#using-sling-adapters}

[Sling](https://sling.apache.org) では、[Adaptable](https://sling.apache.org/documentation/the-sling-engine/adapters.html) インターフェイスを実装するオブジェクトを便利に翻訳するための [&#x200B; アダプタパターン &#x200B;](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) が提供されています。 このインターフェイスは、オブジェクトを引数として渡されるクラスタイプに変換する汎用の [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) メソッドを提供します。

例えば、リソースオブジェクトを対応するノードオブジェクトに変換するには、次の操作を実行します。

```java
Node node = resource.adaptTo(Node.class);
```

## ユースケース {#use-cases}

次のようなユースケースがあります。

* 実装用のオブジェクトの取得

  例えば、汎用の [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) インターフェイスの JCR ベース実装では、基盤の JCR [`Node`](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) にアクセスできます。

* 内部的なコンテキストオブジェクトを渡す必要があるオブジェクトのショートカット作成。

  例えば、JCR ベースの [`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html) はリクエストの [`JCR Session`](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Session.html) への参照を保持します。これは、[`PageManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html) や [`UserManager`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/security/UserManager.html) など、そのリクエストセッションに基づいて動作できる多くのオブジェクトに必要です。

* サービスへのショートカット。

  稀なケース - `sling.getService()` も簡単に使用できます。

### 戻り値 Null {#null-return-value}

`adaptTo()` が null を返します。

その理由は様々で、具体的には以下のものがあります。

* この実装は、ターゲットタイプをサポートしていません。
* このケースを処理するアダプタ ファクトリがアクティブではありません（たとえば、サービス参照が見つからないなど）
* 内部条件が失敗しました。
* サービスを利用できません。

null ケースを適切に処理することが重要です。JSP レンダリングの場合、コンテンツの一部が空になると、JSP の失敗が許容される場合があります。

### キャッシュ {#caching}

パフォーマンスを改善する目的で、各実装では `obj.adaptTo()` 呼び出しから返されたオブジェクトを自由にキャッシュできます。`obj` が同じであれば、返されるオブジェクトも同じです。

このキャッシュ処理は、すべての `AdapterFactory` ベースのケースで実行されます。

ただし、一般的なルールはなく、オブジェクトは新規インスタンスでも既存のインスタンスでもかまいません。したがって、いずれの動作にも依存することはできません。したがって、このシナリオでオブジェクトを再利用できることが、特に `AdapterFactory` 内で重要です。

### 仕組み {#how-it-works}

`Adaptable.adaptTo()` の実装には、様々な方法があります。

* オブジェクト自体による実装（このメソッド自体を実装して特定のオブジェクトにマッピングします）。
* [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html) を使用。これは、任意のオブジェクトをマッピングできます。

  オブジェクトは、引き続き `Adaptable` インターフェイスを実装し、[`SlingAdaptable`](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/adapter/SlingAdaptable.html) を拡張する必要があります（これは、Central Adapter Manager の `adaptTo` 呼び出しを渡します）。

  `adaptTo` などの既存のクラスの `Resource` メカニズムにフックします。

* これら 2 つの組み合わせ。

最初のケースでは、Java™ docs に何の `adaptTo-targets` が可能かが示されます。ただし、JCR ベースのリソースなどの特定のサブクラスの場合は、多くの場合、この方法を使用できません。 後者の場合、`AdapterFactory` の実装は通常、バンドルのプライベートクラスの一部であるため、クライアント API で公開されず、Java™ ドキュメントにも記載されません。 理論的には、[OSGi](/help/sites-deploying/configuring-osgi.md) サービスランタイムからすべての `AdapterFactory` 実装にアクセスし、「アダプタブル」（ソースとターゲット）の設定を調べることは可能ですが、相互にマッピングすることはできません。最終的には、これは内部ロジックに依存し、ドキュメントに記載する必要があります。したがって、参照です。

## 参照 {#reference}

### Sling {#sling}

[**Resource**](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html">ノード</a></td>
   <td>JCR ノードベースのリソースまたはノードを参照する JCR プロパティの場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Property.html">プロパティ</a></td>
   <td>JCR プロパティベースのリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html">項目</a></td>
   <td>JCR ベースのリソース（ノードまたはプロパティ）の場合</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">Map</a></td>
   <td>JCR ノードベースのリソース（または値をサポートする他のリソース）の場合、プロパティのマップを返します。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>JCR ノードベースのリソースの場合は、プロパティの使いやすいマップを返し、それ以外のリソースに対応する値マップを返します。 また、<br /><code><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code> （大文字と小文字を区別するなど）を使用することで、（より簡単に）これを実現できます。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> の拡張。プロパティを探すときにリソースの階層を考慮することができます。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td>そのノードのプロパティを変更できる <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a> の拡張機能。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>JCR ノードベース（<code>nt:file</code> または <code>nt:resource</code>）、バンドルリソース、ファイルシステムリソースの場合は、ファイルリソースのバイナリコンテンツを返します。 バイナリ JCR プロパティリソースのデータを返します。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>リソースの URL を返します。 JCR ノードベースのリソースのリポジトリ URL、バンドルリソースの JAR バンドル URL、またはファイルシステムリソースのファイル URL を返します。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">ファイル</a></td>
   <td>ファイルシステムリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>このリソースが、Sling によってスクリプトエンジンが登録されているスクリプト（JSP ファイルなど）の場合。</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">サーブレット</a></td>
   <td>このリソースが、Sling によってスクリプトエンジンが登録されているスクリプト（jsp ファイルなど）である場合、またはこのリソースがサーブレットリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">Double</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendar</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Value.html">Value</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendar[]</a><br /> <a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>JCR プロパティベースのリソースの場合、値を返します（値はに適合します）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>リソースが JCR ノードベースのリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Page.html">Page</a></td>
   <td>JCR ノードベースのリソースで、ノードが <code>cq:Page</code> （または <code>cq:PseudoPage</code>）の場合。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/components/Component.html">コンポーネント</a></td>
   <td>リソースが <code>cq:Component</code> ノードリソースである場合</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/designer/Design.html">デザイン</a></td>
   <td>リソースがデザインノード（<code>cq:Page</code>）である場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Template.html">テンプレート</a></td>
   <td>リソースが <code>cq:Template</code> ノードリソースである場合</td>
  </tr>  
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">ブループリント</a></td>
   <td>リソースが <code>cq:Template</code> ノードリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/dam/api/Asset.html">Asset</a></td>
   <td>リソースが <code>dam:Asset</code> ノードリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/dam/api/Rendition.html">Rendition</a></td>
   <td><code>dam:Asset</code> レンディションの場合（<code>nt:file</code> のレンディションフォルダーの <code>dam:Asset</code> 下）</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/tagging/Tag.html">タグ</a></td>
   <td>リソースが <code>cq:Tag</code> ノードリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>JCR ベースのリソースであり、ユーザーが UserManager へのアクセス権を持っている場合は、JCR セッションに基づきます。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a></td>
   <td>Authorizable は、User と Group の共通の基本インターフェイスです。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/User.html">User</a></td>
   <td>ユーザーは、認証および権限借用が可能な、特別な認証可能なユーザーです。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>リソースが JCR ベースのリソースの場合は、そのリソースの下を検索します（または setSearchIn （）を使用します）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>特定のページ/ワークフローペイロードノードのワークフローステータス。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>特定のリソースまたはその <code>jcr:content</code> のサブノードのレプリケーションステータス（最初にチェック済み）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>JCR ノードベースのリソースの場合、特定のタイプに適合したコネクタリソースを返します。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/contentsync/config/package-summary.html">Config</a></td>
   <td>リソースが <code>cq:ContentSyncConfig</code> ノードリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>リソースが <code>cq:ContentSyncConfig</code> ノードリソース配下にある場合</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/ResourceResolver.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>リクエストの JCR セッション（JCR ベースのリソースリゾルバーの場合）（デフォルト）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>JCR セッションに基づきます（JCR ベースのリソースリゾルバーの場合）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>JCR セッションに基づきます（JCR ベースのリソースリゾルバーの場合）。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManager では、ユーザーおよびグループである認証可能なオブジェクトへのアクセスと管理の手段が提供されます。 UserManager は特定のセッションにバインドされています。
   </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a> </td>
   <td>現在のユーザー。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/User.html">ユーザー</a><br /> </td>
   <td>現在のユーザー。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>リクエストオブジェクトがなくても絶対 URL を外部化する場合 <br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) は次の項目に適応します。

現時点ではターゲットはありませんが、Adaptable を実装し、カスタムの AdapterFactory 内でソースとして使用することは可能です。

[**SlingHttpServletResponse**](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br />（XML）</td>
   <td>Sling リライター応答の場合</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**[page](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Page.html)** は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>ページのリソース。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>ラベル付きリソースは現在のリソースです。 つまり、表示しているオブジェクトと同じオブジェクトです。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>ページのノード。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>ページのリソースが適応できるすべての項目。</td>
  </tr>
 </tbody>
</table>

**[&#x200B; コンポーネント &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/components/Component.html)** は次の項目に適応します。

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) | コンポーネントのリソース |
| --- | --- |
| [LabeledResource](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html) | ラベル付きリソースは現在のリソースです。 つまり、表示しているオブジェクトと同じオブジェクトです。 |
| [Node](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | コンポーネントのノード |
| ... | コンポーネントのリソースが適応できるすべての項目 |

**[&#x200B; テンプレート &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/Template.html)** は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>テンプレートのリソース。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>ラベル付きリソースは現在のリソースです。 つまり、表示しているオブジェクトと同じオブジェクトです。</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>このテンプレートのノード。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>テンプレートのリソースが適応可能なすべての項目。</td>
  </tr>
 </tbody>
</table>

#### セキュリティ {#security}

**Authorizable**、**User および &#x200B;** Group** は以下に適応します。

| [Node](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | ユーザー/グループのホームノードを返します。 |
| --- | --- |
| [ReplicationStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/replication/ReplicationStatus.html) | ユーザー/グループのホームノードのレプリケーションステータスを返します。 |

#### DAM {#dam}

**Asset** は次の項目に適応します。

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) | アセットのリソース。 |
| --- | --- |
| [Node](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | アセットのノード。 |
| ... | アセットのリソースが適応可能なすべての項目。 |

#### タグ {#tagging}

**Tag** は次の項目に適応します。

| [Resource](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) | タグのリソース。 |
| --- | --- |
| [Node](https://developer.adobe.com/experience-manager/reference-materials/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | タグのノード。 |
| ... | タグのリソースが適応可能なすべての項目。 |

#### その他 {#other}

さらに、Sling、JCR、OCM では、カスタム OCM （` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)`Object Content Mapping[）オブジェクトの &#x200B;](https://jackrabbit.apache.org/jcr/object-content-mapping.html) も提供しています。
