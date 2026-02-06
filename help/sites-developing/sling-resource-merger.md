---
title: AEMでの Sling Resource Merger の使用
description: Sling Resource Merger は、リソースのアクセスとマージのためのサービスを提供します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 6fb6e522-fb81-4ba2-90b2-aad68f8bfa9e
source-git-commit: 9bc1cad84bb14b7513ede1fff2c1a37768dac442
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 39%

---

# AEMでの Sling Resource Merger の使用{#using-the-sling-resource-merger-in-aem}

## 目的 {#purpose}

Sling Resource Merger は、リソースのアクセスとマージのためのサービスを提供します.次の両方に対して差分メカニズムを提供します。

* [設定済み検索パス](/help/sites-developing/overlays.md#configuring-the-search-paths)を使用するリソースの&#x200B;**[オーバーレイ](/help/sites-developing/overlays.md)**。

* リソースタイプ階層を（**プロパティを通じて）使用するタッチ操作対応 UI のコンポーネントダイアログ（**）の`cq:dialog`オーバーライド`sling:resourceSuperType`。

Sling Resource Merger は、オーバーレイおよびオーバーライドの両方のリソース（およびそのプロパティ）を元のリソースとプロパティに組み合わせます。

* カスタマイズされた定義のコンテンツの方が、元の定義のコンテンツよりも優先されます。 つまり、*オーバーレイ* または *オーバーライド* します。

* 必要な場合には、カスタマイズされた定義に含まれる[プロパティ](#properties)が、元の定義から結合されたコンテンツをどう使用するかを指定します。

>[!CAUTION]
>
>Sling Resource Merger および関連する手法は、[Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/index.html) に対してのみ使用できます。これはつまり、標準のタッチ操作対応 UI でのみ使用できるという意味です。特に、この方法で定義された特定のオーバーライドは、コンポーネントのタッチ操作対応ダイアログに対してのみ適用できます。
>
>他の領域（タッチ操作対応コンポーネントの他の部分やクラシック UI など）をオーバーレイまたはオーバーライドするには、適切なノードと構造をオリジナルからコピーします。 カスタマイズを定義する場所にコピーを配置します。

### AEM の目的 {#goals-for-aem}

AEM で Sling Resource Merger を使用する目的は、次のとおりです。

* `/libs` にカスタマイズの変更が加えられないようにする。
* `/libs` からレプリケートされる構造を減らす。

  Sling Resource Merger を使用する場合、`/libs` から構造全体をコピーすることはお勧めしません。 その理由は、カスタマイズに保持される情報が多くなりすぎるからです（通常は `/apps`）。 情報を不必要に複製すると、システムがアップグレードされたときに問題が発生する可能性が高くなります。

>[!NOTE]
>
>オーバーライドは、検索パスに依存しません。 接続を確立するには、プロパティ `sling:resourceSuperType` を使用します。
>
>ただし、オーバーライドは `/apps` で定義されるのが一般的です。AEMでは、カスタマイズを `/apps` で定義することがベストプラクティスとされています。 なぜなら、`/libs` の下にあるものは何も変更してはならないからです。

>[!CAUTION]
>
>`/libs` パス内は一切変更し&#x200B;*ない*&#x200B;でください。
>
>インスタンスを次回アップグレードする際に `/libs` のコンテンツが上書きされるからです。 また、ホットフィックスまたは機能パックを適用すると、上書きされる場合があります。
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

  子を含め、リソースが完全に非表示になっているかどうかを示します。

* `sling:hideChildren`（`String` または `String[]`）

  非表示にする子ノード、または子ノードのリストが含まれます。 ノードのプロパティは維持されます。

  ワイルドカード `*` を指定した場合はすべて非表示になります。

* `sling:orderBefore`（`String`）

  これには、現在のノードが前に配置されている兄弟ノードの名前が含まれます。

これらのプロパティは、対応する/元のリソース/プロパティ（`/libs` から）がオーバーレイ/オーバーライド（多くの場合、`/apps` で）によってどのように使用されるかに影響します。

### 構造の作成 {#creating-the-structure}

オーバーレイまたはオーバーライドを作成するには、元のノードを同じ構造で、目的の場所（通常は `/apps`）に再作成する必要があります。次に例を示します。

* オーバーレイ

   * サイトコンソールのナビゲーションエントリの定義（パネルに表示されるもの）は次の場所で定義されています。


     `/libs/cq/core/content/nav/sites/jcr:title`

   * オーバーレイするには、次のノードを作成します。

     `/apps/cq/core/content/nav/sites`

     次に、必要に応じて `jcr:title` プロパティを更新します。

* オーバーライド

   * テキストコンソールのタッチ操作対応ダイアログボックスの定義は、次のように定義されます。

     `/libs/foundation/components/text/cq:dialog`

   * オーバーライドするには、次のノードを作成します。 例：

     `/apps/the-project/components/text/cq:dialog`

どちらかを作成するには、スケルトン構造を再作成するだけで済みます。 構造の再作成を簡単にするために、すべての中間ノードのタイプは `nt:unstructured` にできます（元のノードタイプを反映する必要はありません）。 例：`/libs`。

上記のオーバーレイの例では、次のノードが必要となります。

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
>Sling Resource Merger を使用する場合（つまり、標準のタッチ操作対応 UI を使用する場合）は、`/libs` から構造全体をコピーしないことをお勧めします。 これは、`/apps` に保持される情報が多くなりすぎるからです。 その結果、システムがアップグレードされると、問題が発生する可能性があります。

### ユースケース {#use-cases}

標準機能を使用すると、これらのユースケースで次のことが可能です。

* **プロパティの追加**

  プロパティは `/libs` 定義に存在しませんが、`/apps` オーバーレイ/オーバーライドでは必須です。

   1. `/apps` 内に、対応するノードを作成します。
   1. このノード&grave;&grave;で新しいプロパティを作成します。

* **プロパティの再定義（自動作成されたプロパティ以外）**

  プロパティは `/libs` で定義されますが、`/apps` オーバーレイ/オーバーライドでは新しい値が必要です。

   1. `/apps` 内に、対応するノードを作成します。
   1. このノード（`apps` の下）に一致するプロパティを作成

      * プロパティは、Sling リソースリゾルバーの設定に基づいて優先度が決まります。
      * プロパティタイプの変更がサポートされています。

        `/libs` で使用されているものとは異なるプロパティタイプを使用する場合、その定義したプロパティタイプが使用されます。

  >[!NOTE]
  >
  >プロパティタイプの変更がサポートされています。

* **自動作成されたプロパティの再定義**

  デフォルトでは、自動作成されたプロパティ（`jcr:primaryType` など）は、現在 `/libs` にあるノードタイプが確実に考慮されるようにオーバーレイ/オーバーライドの対象にはなりません。 オーバーレイ/オーバーライドを適用するには、`/apps` でノードを再作成し、プロパティを明示的に非表示にして再定義する必要があります。

   1. `/apps` 以下に、必要な `jcr:primaryType` を持つ、対応するノードを作成します。
   1. 自動作成されたプロパティに設定された値で、そのノードに `sling:hideProperties` プロパティを作成します。例：`jcr:primaryType`

      `/apps` で定義されたこのプロパティは、`/libs` で定義されたものよりも優先されるようになりました

* **ノードおよびその子の再定義**

  ノードとその子は `/libs` で定義されますが、`/apps` オーバーレイ/オーバーライドでは新しい設定が必要です。

   1. 次のアクションを組み合わせます。

      1. ノードの子の非表示（そのノードのプロパティは維持）
      1. プロパティ/プロパティの再定義

* **プロパティの非表示**

  プロパティは `/libs` で定義されますが、`/apps` オーバーレイ/オーバーライドでは必須ではありません。

   1. `/apps` 内に、対応するノードを作成します。
   1. `String` 型または `String[]` 型の `sling:hideProperties` プロパティを作成します。を使用して、非表示/無視するプロパティを指定します。 ワイルドカードも使用できます。次に例を示します。

      * `*`
      * `["*"]`
      * `jcr:title`
      * `["jcr:title", "jcr:description"]`

* **ノードおよびその子の非表示**

  ノードとその子は `/libs` で定義されますが、`/apps` オーバーレイ/オーバーライドでは必須ではありません。

   1. `/apps` 以下に、対応するノードを作成します。
   1. `sling:hideResource` プロパティを作成します

      * 型：`Boolean`
      * 値：`true`

* **ノードの子の非表示（そのノードのプロパティは維持）**

  ノード、そのプロパティおよびその子が `/libs` に定義されていて、ノードとそのプロパティは、`/apps` のオーバーレイ/オーバーライドでは必要ですが、`/apps` のオーバーレイ/オーバーライドでは、一部またはすべての子ノードが必要ではありません。

   1. `/apps` 以下に、対応するノードを作成します。
   1. `sling:hideChildren` プロパティを作成します。

      * 型：`String[]`
      * 値：非表示/無視する子ノードのリスト（`/libs` で定義）

      ワイルドカード&amp;ast；を使用すると、すべての子ノードを非表示または無視できます。

* **ノードの並べ替え**

  ノードとその兄弟が `/libs` 内で定義されていて、順序を変更するには、`/apps` のオーバーレイまたはオーバーライドでノードを再作成します。 `/libs` 内の適切な兄弟ノードを参照して、新しい位置を定義します。


   * `sling:orderBefore` プロパティを使用します。

      1. `/apps` 以下に、対応するノードを作成します。
      1. `sling:orderBefore` プロパティを作成します。

         現在のノードを `/libs` の前に配置するノードを指定します。

         * 型：`String`
         * 値：`<before-SiblingName>`

### コードから Sling Resource Merger を呼び出します {#invoking-the-sling-resource-merger-from-your-code}

Sling Resource Merger には 2 つのカスタムリソースプロバイダーが含まれています。1 つはオーバーレイ用、もう 1 つはオーバーライド用です。各は、マウントポイントを使用してコード内で呼び出すことができます。

>[!NOTE]
>
>リソースにアクセスする場合は、適切なマウントポイントを使用することをお勧めします。
>
>このアプローチは Sling Resource Merger を呼び出し、完全に結合されたリソースを返します。 また、`/libs` からコピーする必要がある構造の量も削減されます。

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
