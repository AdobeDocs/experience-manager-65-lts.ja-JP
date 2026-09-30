---
title: Sling アダプターの使用
description: Slingには、アダプタパターンが用意されており、アダプタブルインターフェイスを実装するオブジェクトを便利に変換できます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 7eae83bd-7982-4051-821f-b43f65c5af2b
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: d1f055e0688c24b55f80c7e2be974fe1d28ae8d5
workflow-type: tm+mt
source-wordcount: '2596'
ht-degree: 30%
---
# Sling アダプターの使用{#using-sling-adapters}

[Sling](https://sling.apache.org)は、[適応可能](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) インターフェイスを実装するオブジェクトを便利に変換する[&#x200B; アダプターパターン &#x200B;](https://sling.apache.org/documentation/the-sling-engine/adapters.html)を提供しています。 このインターフェイスは、オブジェクトを引数として渡されるクラスタイプに変換する汎用の [adaptTo()](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/Adaptable.html#adaptTo%28java.lang.Class%29) メソッドを提供します。

例えば、リソースオブジェクトを対応するノードオブジェクトに変換するには、次の操作を実行します。

```java
Node node = resource.adaptTo(Node.class);
```

## ユースケース {#use-cases}

次のようなユースケースがあります。

* 実装用のオブジェクトの取得

  例えば、汎用の [`Resource`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/Resource.html) インターフェイスの JCR ベース実装では、基盤の JCR [`Node`](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) にアクセスできます。

* 内部的なコンテキストオブジェクトを渡す必要があるオブジェクトのショートカット作成。

  例えば、JCR ベースの[`ResourceResolver`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/resource/ResourceResolver.html)は、リクエストの[`JCR Session`](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Session.html)への参照を保持しています。これは、次に、そのリクエストセッションに基づいて動作できる多くのオブジェクト（[`PageManager`](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html)や[`UserManager`](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/security/UserManager.html)など）に必要です。

* サービスへのショートカット。

  稀なケース - `sling.getService()` も簡単に使用できます。

### Null戻り値 {#null-return-value}

`adaptTo()`はnullを返します。

その理由は多岐にわたります。

* 実装はターゲットタイプをサポートしていません。
* このケースを処理するアダプターファクトリはアクティブではありません（例えば、サービス参照が欠落しているなど）
* 内部条件が失敗しました。
* サービスを利用できません。

null ケースを適切に処理することが重要です。 JSP レンダリングの場合、コンテンツの一部が空になると、JSP の失敗が許容される場合があります。

### キャッシュ {#caching}

パフォーマンスを改善する目的で、各実装では `obj.adaptTo()` 呼び出しから返されたオブジェクトを自由にキャッシュできます。 `obj` が同じであれば、返されるオブジェクトも同じです。

このキャッシュ処理は、すべての `AdapterFactory` ベースのケースで実行されます。

ただし、一般的なルールはなく、オブジェクトは新規インスタンスでも既存のインスタンスでもかまいません。 したがって、いずれの動作にも依存することはできません。 したがって、特に`AdapterFactory`内では、このシナリオでオブジェクトを再利用できることが重要です。

### 仕組み {#how-it-works}

`Adaptable.adaptTo()` の実装には、様々な方法があります。

* オブジェクト自体による実装（このメソッド自体を実装して特定のオブジェクトにマッピングします）。
* [`AdapterFactory`](https://sling.apache.org/apidocs/sling5/org/apache/sling/api/adapter/AdapterFactory.html) を使用。これは、任意のオブジェクトをマッピングできます。

  オブジェクトは、引き続き `Adaptable` インターフェイスを実装し、[`SlingAdaptable`](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/adapter/SlingAdaptable.html) を拡張する必要があります（これは、Central Adapter Manager の `adaptTo` 呼び出しを渡します）。

  `Resource`などの既存のクラスの`adaptTo` メカニズムにフックします。

* これら 2 つの組み合わせ。

最初のケースでは、Java™ docs に何の `adaptTo-targets` が可能かが示されます。 ただし、JCR ベースのリソースなどの特定のサブクラスの場合は、多くの場合は使用できません。 後者の場合、`AdapterFactory`の実装は通常、バンドルのプライベートクラスの一部であるため、クライアント APIで公開されたり、Java™ ドキュメントに一覧表示されたりすることはありません。 理論的には、[OSGi](/help/sites-deploying/configuring-osgi.md) サービスランタイムからすべての `AdapterFactory` 実装にアクセスし、「アダプタブル」（ソースとターゲット）の設定を調べることは可能ですが、相互にマッピングすることはできません。 最終的には、これは内部ロジックに依存し、ドキュメントに記載する必要があります。 したがって、参照します。

## 参照 {#reference}

### Sling {#sling}

[**Resource**](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html">ノード</a></td>
   <td>JCR ノードベースのリソースまたはノードを参照するJCR プロパティの場合</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Property.html">プロパティ</a></td>
   <td>JCR プロパティベースのリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Item.html">項目</a></td>
   <td>JCR ベースのリソース（ノードまたはプロパティ）の場合</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Map.html">Map</a></td>
   <td>JCR ノードベースのリソース（または値マップをサポートするその他のリソース）の場合は、プロパティのマップを返します。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a></td>
   <td>JCR ノードベースのリソースまたはその他のリソースが値マップをサポートしている場合は、プロパティの使いやすいマップを返します。 また、<br /> <code><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/ResourceUtil.html">ResourceUtil.getValueMap(Resource)</a></code>を使用して（より簡単に）実現することもできます（ヌルケースなどを処理します）。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/commons/inherit/InheritanceValueMap.html">InheritanceValueMap</a></td>
   <td>プロパティを検索する際にリソースの階層を考慮できるようにする<a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>の拡張機能。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/ModifiableValueMap.html">ModifiableValueMap</a></td>
   <td>ノード上のプロパティを変更できる<a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/ValueMap.html">ValueMap</a>の拡張機能。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/InputStream.html">InputStream</a></td>
   <td>JCR ノードベース （<code>nt:file</code>または<code>nt:resource</code>）、バンドルリソース、またはファイルシステムリソースの場合、ファイルリソースのバイナリコンテンツを返します。 バイナリ JCR プロパティリソースのデータを返します。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/net/URL.html">URL</a></td>
   <td>リソースのURLを返します。 JCR ノードベースのリソースのリポジトリ URL、バンドルリソースのJAR バンドル URL、またはファイルシステムリソースのファイル URLを返します。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/io/File.html">ファイル</a></td>
   <td>ファイルシステムリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://sling.apache.org/apidocs/sling5/org/apache/sling/api/scripting/SlingScript.html">SlingScript</a></td>
   <td>このリソースが、スクリプトエンジンがslingに登録されているスクリプト（jsp ファイルなど）である場合。</td>
  </tr>
  <tr>
   <td><a href="https://www.oracle.com/java/technologies/servlet-technology.html">サーブレット</a></td>
   <td>このリソースが、スクリプトエンジンがslingに登録されているスクリプト（jsp ファイルなど）である場合、またはサーブレットリソースである場合。</td>
  </tr>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Double.html">Double</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendar</a><br /> <a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Value.html">Value</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/String.html">String[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Boolean.html">Boolean[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/lang/Long.html">Long[]</a><br /> <a href="https://docs.oracle.com/javase/1.5.0/docs/api/java/util/Calendar.html">Calendar[]</a><br /> <a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Value.html">Value[]</a></td>
   <td>JCR プロパティベースのリソースである場合は、値を返します（値が適合する場合）。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>リソースが JCR ノードベースのリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/Page.html">ページ</a></td>
   <td>JCR ノードベースのリソースで、ノードが<code>cq:Page</code> （または<code>cq:PseudoPage</code>）の場合。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/components/Component.html">コンポーネント</a></td>
   <td>リソースが <code>cq:Component</code> ノードリソースである場合</td>
  </tr>  
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/designer/Design.html">デザイン</a></td>
   <td>リソースがデザインノード（<code>cq:Page</code>）である場合</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/Template.html">テンプレート</a></td>
   <td>リソースが <code>cq:Template</code> ノードリソースである場合</td>
  </tr>  
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/msm/api/Blueprint.html">ブループリント</a></td>
   <td>リソースが <code>cq:Template</code> ノードリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/dam/api/Asset.html">アセット</a></td>
   <td>リソースが <code>dam:Asset</code> ノードリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/dam/api/Rendition.html">Rendition</a></td>
   <td><code>dam:Asset</code> レンディションの場合（<code>dam:Asset</code>のレンディションフォルダーの<code>nt:file</code>）</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/tagging/Tag.html">タグ</a></td>
   <td>リソースが <code>cq:Tag</code> ノードリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/security/UserManager.html">UserManager</a></td>
   <td>JCR ベースのリソースであり、ユーザーがUserManagerにアクセスする権限を持っている場合は、JCR セッションに基づきます。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a></td>
   <td>Authorizableは、ユーザーとグループの共通の基本インターフェイスです。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/User.html">ユーザー</a></td>
   <td>ユーザーは、認証および偽装できる特別な認証可能です。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/search/SimpleSearch.html">SimpleSearch</a></td>
   <td>リソースの下を検索します（または、JCR ベースのリソースの場合はsetSearchIn （）を使用します）。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/workflow/status/WorkflowStatus.html">WorkflowStatus</a></td>
   <td>特定のページ/ワークフローペイロードノードのワークフローステータス。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/replication/ReplicationStatus.html">ReplicationStatus</a></td>
   <td>特定のリソースまたはその<code>jcr:content</code> サブノードのレプリケーションステータス （最初にチェック済み）。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/connector/ConnectorResource.html">ConnectorResource</a></td>
   <td>JCR ノードベースのリソースの場合、特定のタイプに対して適合されたコネクタリソースを返します。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/contentsync/config/package-summary.html">Config</a></td>
   <td>リソースが <code>cq:ContentSyncConfig</code> ノードリソースである場合</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/contentsync/config/package-summary.html">ConfigEntry</a></td>
   <td>リソースが <code>cq:ContentSyncConfig</code> ノードリソース配下にある場合</td>
  </tr>
 </tbody>
</table>

[**ResourceResolver**](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/ResourceResolver.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Session.html">Session</a></td>
   <td>リクエストのJCR セッション（JCR ベースのリソースリゾルバーの場合）（デフォルト）。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html">PageManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/components/ComponentManager.html">ComponentManager</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/designer/Designer.html">Designer</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/dam/api/AssetManager.html">AssetManager</a></td>
   <td>JCR ベースのリソースリゾルバーの場合は、JCR セッションに基づきます。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/tagging/TagManager.html">TagManager</a></td>
   <td>JCR ベースのリソースリゾルバーの場合は、JCR セッションに基づきます。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/UserManager.html">UserManager</a></td>
   <td>UserManagerは、ユーザーおよびグループである承認可能なオブジェクトにアクセスし、管理するための手段を提供します。 UserManagerは特定のセッションにバインドされています。
   </td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/Authorizable.html">Authorizable</a> </td>
   <td>現在のユーザー。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/jackrabbit/api/security/user/User.html">ユーザー</a><br /> </td>
   <td>現在のユーザー。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/search/QueryBuilder.html">QueryBuilder</a></td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/commons/Externalizer.html">Externalizer</a></td>
   <td>リクエストオブジェクトがなくても、絶対URLを外部化する場合。<br /> </td>
  </tr>
 </tbody>
</table>

[**SlingHttpServletRequest**](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/SlingHttpServletRequest.html) は次の項目に適応します。

現時点ではターゲットはありませんが、Adaptable を実装し、カスタムの AdapterFactory 内でソースとして使用することは可能です。

[**SlingHttpServletResponse**](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/SlingHttpServletResponse.html) は次の項目に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://docs.oracle.com/javase/1.5.0/docs/api/org/xml/sax/ContentHandler.html">ContentHandler</a><br />（XML）</td>
   <td>Sling リライター応答の場合</td>
  </tr>
 </tbody>
</table>

#### WCM {#wcm}

**この[&#x200B; ページ &#x200B;](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/Page.html)**&#x200B;は、次の内容に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><br /> </td>
   <td>ページのリソース。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>ラベル付きリソースは現在のリソースです。 つまり、あなたが見ているのと同じオブジェクトです。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>ページのノード。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>ページのリソースが適応できるすべての項目。</td>
  </tr>
 </tbody>
</table>

**[&#x200B; コンポーネント &#x200B;](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/components/Component.html)**&#x200B;は、次の用途に適応します。

| [Resource](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) | コンポーネントのリソース |
| --- | --- |
| [LabeledResource](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html) | ラベル付きリソースは現在のリソースです。 つまり、あなたが見ているのと同じオブジェクトです。 |
| [Node](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | コンポーネントのノード |
| ... | コンポーネントのリソースが適応できるすべての項目 |

**[&#x200B; テンプレート &#x200B;](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/wcm/api/Template.html)**&#x200B;は、次の用途に適応します。

<table>
 <tbody>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html">Resource</a><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html"><br /> </a></td>
   <td>テンプレートのリソース。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/commons/LabeledResource.html">LabeledResource</a></td>
   <td>ラベル付きリソースは現在のリソースです。 つまり、あなたが見ているのと同じオブジェクトです。</td>
  </tr>
  <tr>
   <td><a href="https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html">Node</a></td>
   <td>このテンプレートのノード。</td>
  </tr>
  <tr>
   <td>...</td>
   <td>テンプレートのリソースが適応可能なすべての項目。</td>
  </tr>
 </tbody>
</table>

#### セキュリティ {#security}

**Authorizable**、**User および** Group** は以下に適応します。

| [Node](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | ユーザー/グループのホームノードを返します。 |
| --- | --- |
| [ReplicationStatus](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/com/day/cq/replication/ReplicationStatus.html) | ユーザー/グループホームノードのレプリケーションステータスを返します。 |

#### DAM {#dam}

**Asset** は次の項目に適応します。

| [Resource](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) | アセットのリソース。 |
| --- | --- |
| [Node](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | アセットのノード。 |
| ... | アセットのリソースが適応可能なすべての項目。 |

#### タグ {#tagging}

**Tag** は次の項目に適応します。

| [Resource](https://experienceleague.adobe.com/en/tools/aem-api-documentation/6-5-lts/javadoc/org/apache/sling/api/resource/Resource.html) | タグのリソース。 |
| --- | --- |
| [Node](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/javax.jcr/javadocs/jcr-2.0/javax/jcr/Node.html) | タグのノード。 |
| ... | タグのリソースが適応可能なすべての項目。 |

#### その他 {#other}

さらに、Sling / JCR / OCMには、カスタム OCM （[&#x200B; オブジェクトコンテンツマッピング &#x200B;](https://jackrabbit.apache.org/jcr/object-content-mapping.html)）オブジェクトの` [AdapterFactory](https://sling.apache.org/site/adapters.html#Adapters-AdapterFactory)`も用意されています。
