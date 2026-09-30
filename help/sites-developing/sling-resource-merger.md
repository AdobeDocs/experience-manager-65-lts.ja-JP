---
title: AEMでのSling Resource Mergerの使用
description: Sling Resource Merger は、リソースのアクセスとマージのためのサービスを提供します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 6fb6e522-fb81-4ba2-90b2-aad68f8bfa9e
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
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 39%
---
# AEMでのSling Resource Mergerの使用{#using-the-sling-resource-merger-in-aem}

## 目的 {#purpose}

Sling Resource Merger は、リソースのアクセスとマージのためのサービスを提供します. 次の両方に対して差分メカニズムを提供します。

* [設定済み検索パス](/help/sites-developing/overlays.md#configuring-the-search-paths)を使用するリソースの&#x200B;**[オーバーレイ](/help/sites-developing/overlays.md)**。

* リソースタイプ階層を（**プロパティを通じて）使用するタッチ操作対応 UI のコンポーネントダイアログ（**）の`cq:dialog`オーバーライド`sling:resourceSuperType`。

Sling Resource Mergerは、オーバーレイとオーバーライドリソース（およびそのプロパティ）の両方を元のリソースとプロパティと組み合わせます。

* カスタマイズされた定義の内容は、元の定義よりも優先されます。 つまり、*オーバーレイ*&#x200B;または&#x200B;*オーバーライド*&#x200B;です。

* 必要な場合には、カスタマイズされた定義に含まれる[プロパティ](#properties)が、元の定義から結合されたコンテンツをどう使用するかを指定します。

>[!CAUTION]
>
>Sling Resource Merger および関連する手法は、[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/index.html) に対してのみ使用できます。 この状況は、標準のタッチ対応UIにのみ適していることを意味します。この方法で定義された特定のオーバーライドは、コンポーネントのタッチ対応ダイアログにのみ適用されます。
>
>他の領域（タッチ対応コンポーネントまたはクラシック UIの他の部分を含む）をオーバーレイまたはオーバーライドするには、元の領域から適切なノードと構造をコピーします。 カスタマイズを定義する場所にコピーを配置します。

### AEM の目的 {#goals-for-aem}

AEM で Sling Resource Merger を使用する目的は、次のとおりです。

* `/libs` にカスタマイズの変更が加えられないようにする。
* `/libs` からレプリケートされる構造を減らす。

  Sling Resource Mergerを使用する場合、`/libs`から構造全体をコピーすることはお勧めしません。 その理由は、カスタマイズに保持される情報が多すぎるためです（通常は`/apps`）。 情報を複製すると、システムがアップグレードされたときに問題が発生する可能性が不必要に高まります。

>[!NOTE]
>
>オーバーライドは検索パスに依存しません。 プロパティ `sling:resourceSuperType`を使用して接続を行います。
>
>ただし、AEMのベストプラクティスは`/apps`でカスタマイズを定義することなので、オーバーライドは`/apps`で定義されることがよくあります。 理由は、`/libs`の下の項目は変更できないためです。

>[!CAUTION]
>
>`/libs` パス内は一切変更し&#x200B;*ない*&#x200B;でください。
>
>理由は、次回インスタンスをアップグレードするときに`/libs`のコンテンツが上書きされるからです。 また、ホットフィックスまたは機能パックを適用すると、上書きされる可能性があります。
>
>設定およびその他の変更に推奨される方法は次のとおりです。
>
>1. 必要な項目（`/libs` 内に存在）を、`/apps` の下で再作成します。
>
>1. `/apps` 内で必要な変更を加えます
>

### プロパティ {#properties}

リソースマージャーには次のプロパティがあります。

* `sling:hideProperties`（`String` または `String[]`）

  非表示にするプロパティまたはプロパティのリストを指定します。

  ワイルドカード `*` を指定した場合はすべて非表示になります。

* `sling:hideResource`（`Boolean`）

  リソースがその子を含めて完全に隠されているかどうかを示します。

* `sling:hideChildren`（`String` または `String[]`）

  非表示にする子ノードまたは子ノードのリストが含まれます。 ノードのプロパティは維持されます。

  ワイルドカード `*` を指定した場合はすべて非表示になります。

* `sling:orderBefore`（`String`）

  現在のノードが前に配置されている兄弟ノードの名前が含まれます。

これらのプロパティは、対応する/元のリソース/プロパティ（`/libs`から）がオーバーレイ/オーバーライド（多くの場合`/apps`）でどのように使用されるかに影響します。

### 構造の作成 {#creating-the-structure}

オーバーレイまたはオーバーライドを作成するには、元のノードを同じ構造で、目的の場所（通常は `/apps`）に再作成する必要があります。 次に例を示します。

* オーバーレイ

  * サイトコンソールのナビゲーションエントリの定義（パネルに表示されるもの）は次の場所で定義されています。

    `/libs/cq/core/content/nav/sites/jcr:title`

  * オーバーレイするには、次のノードを作成します。

    `/apps/cq/core/content/nav/sites`

    次に、必要に応じて `jcr:title` プロパティを更新します。

* オーバーライド

  * テキストコンソールのタッチ操作対応ダイアログボックスの定義は、次のように定義されます。

    `/libs/foundation/components/text/cq:dialog`

  * 上書きするには、次のノードを作成します。 次に例を示します。

    `/apps/the-project/components/text/cq:dialog`

いずれかを作成するには、スケルトン構造を再作成するだけで済みます。 構造の再作成を簡単にするために、すべての中間ノードのタイプを`nt:unstructured`にすることができます（元のノードタイプを反映する必要はありません。 例：`/libs`。

したがって、上記のオーバーレイの例では、次のノードが必要です。

```shell
/apps
  /cq
    /core
      /content
        /nav
          /sites
```

>[!NOTE]
>
>Sling Resource Mergerを使用する場合（つまり、標準のタッチ対応UIを扱う場合）、`/libs`から構造全体をコピーすることはお勧めしません。 その理由は、`/apps`に保持されている情報が多すぎるためです。 その結果、システムがアップグレードされたときに問題が発生する可能性があります。

### ユースケース {#use-cases}

これらのユースケースでは、標準機能を使用して次の操作を行うことができます。

* **プロパティの追加**

  プロパティは`/libs`定義に存在しませんが、`/apps` オーバーレイ / オーバーライドで必要です。

  1. `/apps` 内に、対応するノードを作成します。
  1. このノード&grave;&grave;で新しいプロパティを作成します。

* **プロパティの再定義（自動作成されたプロパティ以外）**

  プロパティは`/libs`で定義されていますが、`/apps` オーバーレイ / オーバーライドには新しい値が必要です。

  1. `/apps` 内に、対応するノードを作成します。
  1. このノード（`apps`以下）に一致するプロパティを作成します

     * プロパティには、Sling リソースリゾルバー設定に基づく優先度があります。
     * プロパティタイプの変更がサポートされています。

       `/libs` で使用されているものとは異なるプロパティタイプを使用する場合、その定義したプロパティタイプが使用されます。

  >[!NOTE]
  >
  >プロパティタイプの変更がサポートされています。

* **自動作成されたプロパティの再定義**

  デフォルトでは、自動作成されたプロパティ（`jcr:primaryType`など）は、現在`/libs`の下にあるノードタイプが確実に尊重されるように、オーバーレイ/オーバーライドの対象にはなりません。 オーバーレイ/オーバーライドを適用するには、`/apps`でノードを再作成し、プロパティを明示的に非表示にして再定義する必要があります。

  1. `/apps` 以下に、必要な `jcr:primaryType` を持つ、対応するノードを作成します。
  1. 自動作成されたプロパティに設定された値で、そのノードに `sling:hideProperties` プロパティを作成します。例：`jcr:primaryType`

     `/apps`で定義されたこのプロパティは、`/libs`で定義されたものよりも優先されるようになりました

* **ノードおよびその子の再定義**

  ノードとその子は`/libs`で定義されていますが、`/apps` オーバーレイ / オーバーライドでは新しい設定が必要です。

  1. 次のアクションを組み合わせます。

     1. ノードの子の非表示（そのノードのプロパティは維持）
     1. プロパティ/プロパティの再定義

* **プロパティの非表示**

  プロパティは`/libs`で定義されていますが、`/apps` オーバーレイ / オーバーライドでは必要ありません。

  1. `/apps` 内に、対応するノードを作成します。
  1. `String` 型または `String[]` 型の `sling:hideProperties` プロパティを作成します。 非表示/無視するプロパティを指定するには、を使用します。 ワイルドカードも使用できます。 次に例を示します。

     * `*`
     * `["*"]`
     * `jcr:title`
     * `["jcr:title", "jcr:description"]`

* **ノードおよびその子の非表示**

  ノードとその子は`/libs`で定義されていますが、`/apps` オーバーレイ / オーバーライドでは必要ありません。

  1. `/apps` 以下に、対応するノードを作成します。
  1. `sling:hideResource` プロパティを作成します

     * 型：`Boolean`
     * 値：`true`

* **ノードの子の非表示（そのノードのプロパティは維持）**

  ノード、そのプロパティおよびその子が `/libs` に定義されていて、 ノードとそのプロパティは`/apps` オーバーレイ / オーバーライドで必要ですが、`/apps` オーバーレイ / オーバーライドでは一部またはすべての子ノードは必要ありません。

  1. `/apps` 以下に、対応するノードを作成します。
  1. `sling:hideChildren` プロパティを作成します。

     * 型：`String[]`
     * 値：非表示/無視する子ノード（`/libs`で定義）のリスト

     ワイルドカード &amp;ast；を使用すると、すべての子ノードを非表示にしたり、無視したりできます。

* **ノードの並べ替え**

  ノードとその兄弟が `/libs` 内で定義されていて、 順序を変更するには、`/apps` オーバーレイまたはオーバーライドでノードを再作成します。 `/libs`の適切な兄弟ノードを参照して、新しい位置を定義します。


  * `sling:orderBefore` プロパティを使用します。

    1. `/apps` 以下に、対応するノードを作成します。
    1. `sling:orderBefore` プロパティを作成します。

       現在のノードが次の前に配置されているノード（`/libs`など）を指定します。

       * 型：`String`
       * 値：`<before-SiblingName>`

### コードからSling Resource Mergerを呼び出します {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger には 2 つのカスタムリソースプロバイダーが含まれています。1 つはオーバーレイ用、もう 1 つはオーバーライド用です。 それぞれ、コード内でマウントポイントを使用して呼び出すことができます。

>[!NOTE]
>
>リソースにアクセスする場合は、適切なマウントポイントを使用することをお勧めします。
>
>このアプローチでは、Sling Resource Mergerが呼び出され、完全に結合されたリソースが返されます。 また、`/libs`からコピーする必要がある構造の量も減ります。

* オーバーレイ：

  * 目的：検索パスに基づいてリソースを結合する。
  * マウントポイント：`/mnt/overlay`
  * 使用方法：`mount point + relative path`
  * 例：

    * `getResource('/mnt/overlay' + '<relative-path-to-resource>');`

* オーバーライド：

  * 目的：スーパータイプに基づいてリソースを結合する。
  * マウントポイント：`/mnt/overide`
  * 使用方法：`mount point + absolute path`
  * 例：

    * `getResource('/mnt/override' + '<absolute-path-to-resource>');`

### 使用例 {#example-of-usage}

以下のページで、一部の例が紹介されています。

* オーバーレイ：

  * [コンソールのカスタマイズ](/help/sites-developing/customizing-consoles-touch.md)
  * [ページオーサリングのカスタマイズ](/help/sites-developing/customizing-page-authoring-touch.md)

* オーバーライド：

  * [ページプロパティの設定](/help/sites-developing/page-properties-views.md#configuring-your-page-properties)
