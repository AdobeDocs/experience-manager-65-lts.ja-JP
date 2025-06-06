---
title: 永続的な GraphQL クエリ
description: Adobe Experience Manager で GraphQL クエリを永続化してパフォーマンスを最適化する方法を説明します。クライアントアプリケーションで HTTP GET メソッドを使用して永続クエリをリクエストでき、応答を Dispatcher および CDN レイヤーにキャッシュできるので、最終的にクライアントアプリケーションのパフォーマンスが向上します。
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments,GraphQL API
role: Developer
exl-id: 686d5510-8cdb-49eb-9ed0-f360be9bdc6d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 100%

---

# 永続的な GraphQL クエリ {#persisted-queries-caching}

永続的なクエリは、Adobe Experience Manager（AEM）サーバーで作成および保存される GraphQL クエリです。永続的なクエリは、クライアントアプリケーションから GET リクエストでリクエストできます。GET リクエストの応答は、Dispatcher および CDN（コンテンツ配信ネットワーク）レイヤーでキャッシュできるので、最終的には、要求元のクライアントアプリケーションのパフォーマンスが向上します。これは、標準の GraphQL クエリとは異なります。標準クエリは、応答を簡単にはキャッシュできない POST リクエストを使用して実行されます。

<!--
>[!NOTE]
>
>Persisted Queries are recommended. See [GraphQL Query Best Practices (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) for details, and the related Dispatcher configuration.
-->

AEM では [GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md) を使用して、[実稼動環境に移行](#transfer-persisted-query-production)する前に GraphQL クエリを開発、テストおよび永続化できます。カスタマイズが必要な場合（例えば、[キャッシュをカスタマイズする](/help/sites-developing/headless/graphql-api/graphiql-ide.md#caching-persisted-queries)場合）、API を使用できます。[GraphQL クエリを永続化する方法](#how-to-persist-query)で示される cURL の例を参照してください。

## 永続的なクエリとエンドポイント {#persisted-queries-and-endpoints}

持続的なクエリでは、常に[適切な Sites 設定](/help/sites-developing/headless/graphql-api/graphql-endpoint.md)に関連するエンドポイントを使用する必要があるため、次のどちらかまたは両方を使用できます。

* グローバル設定とエンドポイント：
クエリは、すべてのコンテンツフラグメントモデルにアクセスできます。
* 特定の Sites 設定およびエンドポイント：
特定の Sites 設定用の永続クエリを作成するには、対応する Sites 設定固有のエンドポイント（関連するコンテンツフラグメントモデルへのアクセスを提供）が必要です。例えば、WKND Sites 設定専用の永続クエリを作成するには、対応する WKND 固有の Sites 設定と、WKND 固有のエンドポイントを事前に作成する必要があります。

>[!NOTE]
>
>詳しくは、[設定ブラウザーでのコンテンツフラグメント機能の有効化](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)を参照してください。
>
>適切な Sites 設定用に、**GraphQL 永続クエリ**&#x200B;を有効にする必要があります。

例えば、`my-query` という特定のクエリがあり、このクエリが Sites 設定 `my-conf` のモデル `my-model` を使用する場合は、次のようになります。

* 特定エンドポイント `my-conf` を使用してクエリを作成すると、クエリは次のように保存されます。
  `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* `global` エンドポイントを使用して同じクエリを作成できますが、クエリは次のように保存されます。
  `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>これらは 2 つの異なるクエリで、異なるパスに保存されます。
>
>同じモデルを使用していますが、異なるエンドポイントを介しています。

## GraphQL クエリを永続化する方法 {#how-to-persist-query}

最初に AEM オーサー環境でクエリを永続化し、その後、アプリケーションで使用するために、実稼動 AEM パブリッシュ環境に[クエリを移行](#transfer-persisted-query-production)することをお勧めします

クエリを永続化するには、次のような様々な方法があります。

* GraphiQL IDE - [永続クエリの保存](/help/sites-developing/headless/graphql-api/graphiql-ide.md#saving-persisted-queries)を参照してください（推奨される方法）
* cURL - 次の例を参照してください。
* その他のツール（[Postman](https://www.postman.com/) など）

GraphiQL IDE は、クエリを保持するための&#x200B;**推奨**&#x200B;される方法です。**cURL** コマンドラインツールを使用して特定のクエリを永続化するには、次の手順に従います。

1. 新しいエンドポイント URL `/graphql/persist.json/<config>/<persisted-label>` に PUT してクエリを準備します。

   例えば、次のようにして、永続的クエリを作成します。

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. この段階で、応答を確認します。

   例えば、以下が成功するかどうかを確認します。

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. その後、URL `/graphql/execute.json/<shortPath>` を GET して、永続的クエリをリクエストできます。

   例えば、次のような永続的クエリを使用します。

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. 既存のクエリパスに POST して、永続的クエリを更新します。

   例えば、次のような永続的クエリを使用します。

   ```shell
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. ラップされたプレーンクエリを作成します。

   次に例を示します。

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. キャッシュコントロール付きのラップされたプレーンクエリを作成します。

   次に例を示します。

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. パラメーター付きの永続的クエリを作成します。

   次に例を示します。

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```


## 永続クエリの実行方法 {#execute-persisted-query}

永続クエリを実行するには、クライアントアプリケーションで次の構文を使用して GET リクエストを実行します。

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

`PERSISTENT_PATH` は、永続クエリが保存される場所への短縮パスです。

1. 例えば、`wknd` は設定名で、`plain-article-query` は永続クエリの名前です。クエリを実行するには：

   ```shell
   $ curl -X GET \
       https://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. パラメーター付きのクエリを実行します。

   >[!NOTE]
   >
   > 永続クエリを実行する場合は、クエリ変数と値を適切に[エンコード](#encoding-query-url)する必要があります。

   次に例を示します。

   ```bash
   $ curl -X GET \
       "https://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   詳しくは、[クエリ変数](#query-variables)の使用を参照してください。

## クエリ変数の使用 {#query-variables}

クエリ変数は、永続クエリで使用できます。クエリ変数をリクエストに付加するには、先頭にセミコロン（`;`）を付けた変数名と値を使用します。複数の変数はセミコロンで区切ります。

次のようなパターンになります。

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

例えば、次のクエリには、アクティビティ値に基づいてリストをフィルタリングするための変数 `activity` が含まれています。

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

このクエリは、パス `wknd/adventures-by-activity` の下に保持できます。`activity=Camping` で永続クエリを呼び出すには、リクエストは次のようになります。

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

なお、`%3B` は `;` の UTF-8 エンコーディングで、`%3D` は `=` のエンコーディングです。永続クエリを実行するには、クエリ変数と特殊文字を[適切にエンコード](#encoding-query-url)する必要があります。

## 永続クエリのキャッシュ {#caching-persisted-queries}

永続クエリが推奨されるのは、[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) と CDN（コンテンツ配信ネットワーク）レイヤーでキャッシュされ、最終的に要求元のクライアントアプリケーションのパフォーマンスを向上させることができるからです。

デフォルトでは、AEM は有効期間（TTL）の定義に基づいてキャッシュを無効にします。これらの TTL は、次のパラメーターで定義できます。これらのパラメーターには様々な方法でアクセスでき、使用するメカニズムに応じて名前が異なります。

| キャッシュタイプ | [HTTP ヘッダー](https://developer.mozilla.org/ja/docs/Web/HTTP/Headers/Cache-Control) | cURL | OSGi 設定 |
|--- |--- |--- |--- |
| ブラウザー | `max-age` | `cache-control : max-age` | `cacheControlMaxAge` |
| CDN | `s-maxage` | `surrogate-control : max-age` | `surrogateControlMaxAge` |
| CDN | `stale-while-revalidate` | `surrogate-control : stale-while-revalidate ` | `surrogateControlStaleWhileRevalidate` |
| CDN | `stale-if-error` | `surrogate-control : stale-if-error` | `surrogateControlStaleIfError` |

{style="table-layout:auto"}

### オーサーインスタンス {#author-instances}

オーサーインスタンスの場合、デフォルト値は次のとおりです。

* `max-age`：60
* `s-maxage`：60
* `stale-while-revalidate`：86400
* `stale-if-error`：86400

これらは

* OSGi 設定で上書きできません
* cURL を使用して HTTP ヘッダー設定を定義するリクエストで上書きできます。リクエストには、`cache-control` や `surrogate-control` に適した設定を含める必要があります。例については、[永続クエリレベルでのキャッシュの管理](#cache-persisted-query-level)を参照してください。

<!-- CQDOC-20186 -->
<!-- following entry is only when the GraphiQL IDE is ready; add cross-reference too -->
<!--
* can be overwritten if you specify values in the **Headers** dialog of the [GraphiQL IDE](#http-cache-headers-graphiql-ide)
-->

### パブリッシュインスタンス {#publish-instances}

パブリッシュインスタンスの場合、デフォルト値は次のとおりです。

* `max-age`：60
* `s-maxage`：7200
* `stale-while-revalidate`：86400
* `stale-if-error`：86400

これらは

<!-- CQDOC-20186 -->
<!-- following entry is only when the GraphiQL IDE is ready -->
<!--
* [from the GraphQL IDE](#http-cache-headers-graphiql-ide)
-->

* [永続クエリレベルで](#cache-persisted-query-level)上書きできます。それには、コマンドラインインターフェイスで cURL を使用して AEM にクエリをポストし、永続クエリを公開する必要があります。

* [OSGi 設定で上書きできます](#cache-osgi-configration)

<!-- CQDOC-20186 -->
<!-- keep for future use; check link -->
<!--
### Managing HTTP Cache Headers in the GraphiQL IDE {#http-cache-headers-graphiql-ide}

The GraphiQL IDE - see [Saving Persisted Queries](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache)
-->

### 永続化されたクエリレベルでのキャッシュの管理 {#cache-persisted-query-level}

これを行うには、コマンドラインインターフェイスで cURL を使用して AEM にクエリを実行する必要があります。

PUT（作成）メソッドの例を次に示します。

```bash
curl -u admin:admin -X PUT \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

POST（更新）メソッドの例を次に示します。

```bash
curl -u admin:admin -X POST \
--url "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
--header "Content-Type: application/json" \
--data '{ "query": "{articleList { items { _path author } } }", "cache-control": { "max-age": 300 }, "surrogate-control": {"max-age":600, "stale-while-revalidate":1000, "stale-if-error":1000} }'
```

`cache-control` は、作成時に設定することもできますし（PUT リクエストを使用）、後で設定することもできます（例えば、POST リクエストを使用）。AEM ではデフォルト値を提供できるので、永続クエリを作成する際に cache-control はオプションです。cURL を使用してクエリを永続化する例については、[GraphQL クエリを永続化する方法](#how-to-persist-query)を参照してください。

### OSGi 設定を使用したキャッシュの管理 {#cache-osgi-configration}

キャッシュをグローバルに管理するには、**永続的なクエリサービス設定**&#x200B;に対して [OSGi 設定を指定](/help/sites-deploying/configuring-osgi.md)できます。それ以外の場合、この OSGi 設定は[パブリッシュインスタンスのデフォルト値](#publish-instances)を使用します。

>[!NOTE]
>
>OSGi の設定は、パブリッシュインスタンスにのみ適しています。この設定はオーサーインスタンス上に存在しますが、無視されます。

## アプリで使用するクエリ URL のエンコード {#encoding-query-url}

アプリケーションで使用するには、クエリ変数の構築時に使用される特殊文字（セミコロン（`;`）、等号（`=`）、スラッシュ（`/`））を、対応する UTF-8 エンコーディングで変換する必要があります。

次に例を示します。

```bash
curl -X GET \ "https://localhost:4502/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

URL は次の部分に分解できます。

| URL の部分 | 説明 |
|----------| -------------|
| `/graphql/execute.json` | 永続クエリのエンドポイント |
| `/wknd/adventure-by-path` | 永続クエリのパス |
| `%3B` | `;` のエンコーディング |
| `adventurePath` | クエリ変数 |
| `%3D` | `=` のエンコーディング |
| `%2F` | `/` のエンコーディング |
| `%2Fcontent%2Fdam...` | コンテンツフラグメントへのエンコードされたパス |

プレーンテキストでは、リクエスト URI は次のようになります。

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

クライアントアプリで永続クエリを使用するには、AEM ヘッドレス クライアント SDK を [JavaScript](https://github.com/adobe/aem-headless-client-js)、[Java](https://github.com/adobe/aem-headless-client-java) または [NodeJS](https://github.com/adobe/aem-headless-client-nodejs) に使用する必要があります。ヘッドレスクライアント SDK は、自動的にリクエスト内のクエリ変数を適切にエンコードします。

## 実稼動環境への永続クエリの移行  {#transfer-persisted-query-production}

永続クエリは、常に、AEM オーサーサービスで作成してから、AEM パブリッシュサービスに公開（レプリケート）する必要があります。多くの場合、永続クエリは、ローカル環境や開発環境などの下位環境で作成およびテストされます。その後、永続クエリを上位レベルの環境に昇格し、最終的に実稼動 AEM パブリッシュ環境で使用できるようにして、クライアントアプリケーションが使用できるようにする必要があります。

### 永続クエリのパッケージ化

永続クエリは、[AEM パッケージ](/help/sites-administering/package-manager.md)に組み込むことができます。その後、AEM パッケージをダウンロードして、様々な環境にインストールできます。AEM パッケージは、AEM オーサー環境から AEM パブリッシュ環境にレプリケートすることもできます。

パッケージを作成するには：

1. **ツール**／**デプロイメント**／**パッケージ**&#x200B;に移動します。
1. 「**パッケージを作成**」をタップして新しいパッケージを作成します。これにより、パッケージを定義するためのダイアログボックスが開きます。
1. パッケージ定義ダイアログの「**一般**」で、「wknd-persistent-queries」などの&#x200B;**名前**&#x200B;を入力します。
1. 「1.0」のようなバージョン番号を入力します。
1. 「**フィルター**」で、新しい&#x200B;**フィルター**&#x200B;を追加します。パスファインダーを使用して、設定の下にある `persistentQueries` フォルダーを選択します。例えば、`wknd` 設定の場合、フルパスは `/conf/wknd/settings/graphql/persistentQueries` になります。
1. 「**保存**」を選択して新しいパッケージ定義を保存し、ダイアログを閉じます。
1. 新しく作成されたパッケージ定義で「**ビルド**」ボタンを選択します。

パッケージが構築されたら、次の操作を実行できます。

* パッケージを&#x200B;**ダウンロード**&#x200B;し、別の環境で再アップロードする。
* **その他**／**レプリケート**&#x200B;をタップして、パッケージを&#x200B;**レプリケート**&#x200B;する。これにより、接続された AEM パブリッシュ環境にパッケージがレプリケートされます。

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, among others).
-->
