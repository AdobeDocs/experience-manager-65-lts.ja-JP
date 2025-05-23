---
title: ページエクスポーター
description: Adobe Experience Manager（AEM）のページエクスポーターの使用方法を説明します。
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
exl-id: 997637d5-1627-4102-8b7c-a0cfd871a7b2
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 99%

---

# ページエクスポーター{#the-page-exporter}

Adobe Experience Manager（AEM）を使用すると、画像ファイル、`.js` ファイル、`.css` ファイルを含む完全な web ページとして、ページをエクスポートできます。

設定が完了したら、URL の `html` を `export.zip` に置き換えることにより、ページのエクスポートをブラウザーからリクエストします。これにより、HTML 形式でレンダリングされたページと参照元のアセットを含む、アーカイブ（zip）ファイルが生成されます。ページ内のすべてのパス（例えば、画像へのパス）は、アーカイブに含まれるファイルまたはサーバー上のリソースを指すように書き換えられます。アーカイブ（zip）ファイルは、ブラウザーからダウンロードできます。

>[!NOTE]
>
>ブラウザーとその設定に応じて、ダウンロードは次のいずれかになります。
>
>* アーカイブファイル（`<page-name>.export.zip`）
>* フォルダー（`<page-name>`）（アーカイブファイルを実際に展開済み）

## ページのエクスポート {#exporting-a-page}

次の手順では、ページをエクスポートする方法を説明します。サイトにエクスポートテンプレートが存在すると仮定しています。エクスポートテンプレートは、ページをエクスポートする方法を定義したものであり、サイトに固有のものです。エクスポートテンプレートを作成するには、[サイト用のページエクスポーター設定の作成](#creating-a-page-exporter-configuration-for-your-site)の節を参照してください。

ページをエクスポートするには：

1. **Sites** コンソールで、対象のページに移動します。

1. ページを選択して、「**プロパティ**」ダイアログを開きます。

1. 「**詳細**」タブを選択します。

1. 「**エクスポート**」フィールドを展開して、エクスポートテンプレートを選択します。
サイトに必要なテンプレートを選択し、「**OK**」で確定します。

1. 「**保存して閉じる**」を選択して、ページプロパティのダイアログを閉じます。

1. ページのエクスポートをリクエストし、URL のサフィックス `html` を `export.zip` に置き換えます。

   次は例です。
   * localhost:4502/content/we-retail/language-masters/en.html

   次の方法でアクセスされます。
   * localhost:4502/content/we-retail/language-masters/en.export.zip

1. アーカイブファイルをファイルシステムにダウンロードします。

1. ファイルシステムで、必要に応じてそのファイルを解凍します。展開すると、選択したページと同じ名前のフォルダーが作成されます。このフォルダーには次が含まれます。

   * サブフォルダー `content`（リポジトリ内のページへのパスを反映した一連のサブフォルダーのルート）

      * この構造の中にある、選択したページの HTML ファイル（`<page-name>.html`）

   * その他のリソース（`.js` ファイル、 `.css` ファイル、画像など）。エクスポートテンプレートの設定に従って配置されます。

1. ページの HTML ファイル（`<unzip-dir>/<path>/<to>/<page>/<page-path>.html`）をブラウザーで開き、レンダリングを確認します。

## サイト用のページエクスポーター設定の作成 {#creating-a-page-exporter-configuration-for-your-site}

ページエクスポーターは、[コンテンツ同期フレームワーク](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/contentsync/package-summary.html)に基づいています。「**ページプロパティ**」ダイアログで利用できる設定は、ページに必要な依存関係を定義するエクスポートテンプレートです。

ページのエクスポートがトリガーされると、エクスポートテンプレートが参照され、ページパスとデザインパスの両方が動的に適用されます。その後、標準のコンテンツ同期機能を使用して、zip ファイルが作成されます。

標準インストールの AEM では、`/etc/contentsync/templates/default` の下にデフォルトテンプレートが含まれています。

* このテンプレートは、リポジトリ内にエクスポートテンプレートが見つからない場合のフォールバックテンプレートです。

* `default` テンプレートは、ページをエクスポートするための設定方法を示していて、新しいエクスポートテンプレートのベースとして使用できます。

* テンプレートのノード構造を JSON 形式でブラウザーに表示するには、次の URL をリクエストします。
  `http://localhost:4502/etc/contentsync/templates/default.json`

新しいページエクスポーターのテンプレートは、次の方法で簡単に作成できます。

* `default` テンプレートをコピーします。

* サイトに適した新しい名前を割り当て、

* その上で、必要な更新を行います。

完全に新しいテンプレートを作成するには：

1. **CRXDE Lite** で、`/etc/contentsync/templates` の下にノードを作成します。

   * `Name`：サイトに適した名前（例：`<mysite>`）。ページエクスポーターテンプレートを選択すると、この名前がページプロパティのダイアログボックスに表示されます。

   * `Type`：`nt:unstructured`

2. テンプレートノード（ここでは `mysite`）の下に、次で説明する設定ノードを使用してノード構造を作成します。

## ページのページエクスポーターテンプレートのアクティブ化 {#activating-a-page-exporter-configuration-for-your-pages}

テンプレートを設定したら、使用可能にします。

1. CRXDE で `/content` ブランチの対象ページに移動します。個々のページや、サブツリーのルートページの場合があります。

1. ページの `jcr:content` ノードで、次のプロパティを作成します。
   * `Name`：`cq:exportTemplate`
   * `Type`：`String`
   * `Value`：テンプレートへのパス（例： `/etc/contentsync/templates/mysite`）

### ページエクスポーター設定ノード {#page-exporter-configuration-nodes}

[コンテンツ同期フレームワーク](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/contentsync/package-summary.html)を使用しているため、テンプレートはノード構造で構成されています。各ノードには、zip ファイルの作成プロセスで特定のアクションを定義する `type` プロパティが含まれています。

<!-- For more details about the type property, see the Overview of configuration types section in the Content Sync framework page.
-->

次のノードを使用してエクスポートテンプレートを作成することができます。

* `page`
page ノードを使用して、ページの HTML を zip ファイルにコピーします。次のような特徴があります。

   * 必須ノード。
   * `/etc/contentsync/templates/<mysite>` の下にある。
   * プロパティ `Name` を `page` に設定して定義されている。
   * ノードタイプは `nt:unstructured`。

  `page` ノードには以下のプロパティがあります。

   * 値 `pages` が設定された `type` プロパティ。

   * `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。
  <!--
  * The other properties are described in the Overview of configuration types section of the Content Sync framework.
  -->

* `rewrite`
rewrite ノードでは、エクスポートしたページでリンクを書き換える方法を定義します。書き換え後のリンクは、zip ファイルに含まれるファイルを指すか、サーバー上のリソースを指します。
  <!-- See the Content Sync page for a complete description of the `rewrite` node. -->

* `design`
design ノードを使用して、エクスポートされるページに使用されているデザインをコピーします。次のような特徴があります。

   * オプション。
   * `/etc/contentsync/templates/<mysite>` の下にある。
   * プロパティ `Name` を `design` に設定して定義される。
   * ノードタイプは `nt:unstructured`。

  `design` ノードには次のプロパティがあります。

   * 値 `copy` に設定された `type` プロパティ。

   * `path` プロパティはありません。現在のページパスが設定に動的にコピーされます。

* `generic`
汎用ノードは、clientlibs の `.js` ファイルや `.css` ファイルのようなリソースを zip ファイルにコピーする際に使用します。次のような特徴があります。

   * オプション。
   * `/etc/contentsync/templates/<mysite>` の下にある。
   * 特定の名前はない。
   * ノードタイプは `nt:unstructured`。
   * `type` プロパティと `type` に関連したプロパティを持ちます。<!--Has a `type` property and any `type` related properties as defined in the Overview of configuration types section of the Content Sync framework.-->

  例えば、次の設定ノードは `mysite.clientlibs.js` ファイルを zip ファイルにコピーします。

  ```xml
  "mysite.clientlibs.js": {
      "extension": "js",
      "type": "clientlib",
      "path": "/etc/designs/mysite/clientlibs",
      "jcr:primaryType": "nt:unstructured"
  }
  ```

**カスタム設定の実装**

カスタム設定も可能です。

<!--
As you may have noticed in the node structure, the **Geometrixx** page export template has a `logo` node with a `type` property set to `image`. This is a special configuration type that has been created to copy the image logo to the zip file. 
-->

特定の要件を満たすには、[カスタム更新ハンドラー](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/contentsync/handler/package-summary.html)を実装する必要があります。

<!-- To meet some specific requirements, you may need to implement a custom `type` property. To do so, see the Implementing a custom update handler section in the Content Sync page.
-->

## プログラムによるページの書き出し {#programmatically-exporting-a-page}

プログラムによってページを書き出すには、[PageExporter](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/index.html?com/day/cq/wcm/contentsync/PageExporter.html) OSGI サービスを使用できます。このサービスを使用すると、次のことができます。

* ページを書き出して HTTP サーブレット応答に書き込む。
* ページを書き出して zip ファイルを特定の場所に保存する。

`export` セレクターおよび `zip` 拡張子にバインドされているサーブレットは PageExporter サービスを使用します。

## トラブルシューティング {#troubleshooting}

Zip ファイルのダウンロードで問題が発生した場合は、リポジトリで `/var/contentsync` ノードを削除して、エクスポートリクエストを再度送信できます。
