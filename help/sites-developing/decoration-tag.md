---
title: 装飾タグ
description: Web ページのコンポーネントがレンダリングされる際に、レンダリングしたコンポーネントをラッピングする HTML 要素を生成できます。AEM では、含まれているコンポーネントをラップする装飾タグを制御する明確でシンプルなロジックを開発者向けに提供しています。
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 085192a0-0415-4861-8bea-a66cd50d9487
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 100%

---

# 装飾タグ{#decoration-tag}

Web ページのコンポーネントがレンダリングされる際に、レンダリングしたコンポーネントをラッピングする HTML 要素を生成できます。これは主に 2 つの目的を果たします。

* HTML 要素でラップされている場合、コンポーネントの編集のみ可能です。
* ラッピング要素は、以下を提供する HTML クラスの適用に使用します。

   * レイアウト情報
   * スタイル設定情報

AEM では、含まれているコンポーネントをラップする装飾タグを制御する明確でシンプルなロジックを開発者向けに提供しています。装飾タグがレンダリングされるかどうか、またその方法は、このページで説明する 2 つの要素の組み合わせによって定義されます。

* コンポーネント自体は、一連のプロパティを使用して装飾タグを設定できます。
* コンポーネント（HTL、JSP、Dispatcher など）を含むスクリプトは、パラメーターを含めることで装飾タグの側面を定義できます。

## レコメンデーション {#recommendations}

予期しない問題発生の回避に役立つ、ラッパー要素を含めるタイミングに関する一般的な推奨事項を以下に示します。

* ページの CSS と JavaScripts がすべての場合で同じように機能できるように、ラッパー要素の存在が、WCMMode（編集またはプレビューモード）、インスタンス（オーサーまたはパブリッシュ）または環境（ステージングまたは実稼動）間で差異がないようにする必要があります。
* ページエディターがコンポーネントを適切に初期化および更新できるように、ラッパー要素を編集可能なすべてのコンポーネントに追加する必要があります。
* 編集できないコンポーネントで、ラッパー要素が特定の機能を果たさない場合は、結果のマークアップが不必要に肥大化しないように、ラッパー要素を回避できます。

## コンポーネントの制御 {#component-controls}

次のプロパティおよびノードをコンポーネントに適用して、装飾タグの動作を制御できます。

* **`cq:noDecoration {boolean}`：**&#x200B;このプロパティは、コンポーネントに追加できます。true の値は、コンポーネントに対してラッパー要素を生成しないよう AEM を強制します。

* **`cq:htmlTag`ノード：**&#x200B;このノードは、コンポーネントに追加でき、次のプロパティを持つことができます。

   * **`cq:tagName {String}`：**&#x200B;これは、デフォルトの DIV 要素の代わりにコンポーネントをラッピングするために使用されるカスタム HTML タグを指定するために使用できます。
   * **`class {String}`：**&#x200B;これは、ラッパーに追加する css クラス名を指定するために使用できます。
   * 他のプロパティ名は、指定されたものと同じ文字列値を持つ HTML 属性として追加されます。

## スクリプトの制御 {#script-controls}

ただし、ラッパーの動作は、[HTL](/help/sites-developing/decoration-tag.md#htl) または [JSP](/help/sites-developing/decoration-tag.md#jsp) のどちらを使用して要素を含めるかによって異なります。

### HTL {#htl}

通常、HTL のラッパー動作は、次のように要約できます。

* デフォルトでは、ラッパー DIV はレンダリングされない（`data-sly-resource="foo"` のみ行う場合）。
* すべての wcm モード（オーサーおよびパブリッシュの両方で無効、プレビュー、編集）は同じようにレンダリングされます。

また、ラッパーの動作も完全に制御できます。

* HTL スクリプトは、ラッパータグの結果の動作を完全に制御します。
* コンポーネントプロパティ（`cq:noDecoration`、`cq:tagName` など）もラッパータグを定義します。

HTL スクリプトおよびその関連ロジックからラッパータグの動作を完全に制御できます。

HTL での開発について詳しくは、[HTL ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=ja)を参照してください。

#### デシジョンツリー {#decision-tree}

このデシジョンツリーは、ラッパータグの動作を決定するロジックの概要を示します。

![chlimage_1-75](assets/chlimage_1-75a.png)

#### ユースケース {#use-cases}

次の 3 つの使用例は、ラッパータグの処理方法の例です。また、目的のラッパータグの動作を制御するのがいかに簡単であるかを説明しています。

以下のすべての例は、次のコンテンツ構造とコンポーネントを前提としています。

```
/content/test/
  @resourceType = "test/components/one"
  child/
    @resourceType = "test/components/two"
```

```
/apps/test/components/
  one/
    one.html
  two/
    two.html
    cq:htmlTag/
      @cq:tagName = "article"
      @class = "component-two"
```

#### 使用例 1：コードの再利用のためのコンポーネントを含める {#use-case-include-a-component-for-code-reuse}

最も一般的な使用例は、コードの再利用のためにコンポーネントが他のコンポーネントを含む場合です。この場合、含まれるコンポーネントは、独自のツールバーやダイアログで編集できるようにする必要がないので、ラッパーは不要で、コンポーネントの `cq:htmlTag` は無視されます。これはデフォルトの動作と見なすことができます。

`one.html: <sly data-sly-resource="child"></sly>`

`two.html: Hello World!`

`/content/test.html` に出力される結果：

**`Hello World!`**

この例は、画像を表示するためのコア画像コンポーネントを含むコンポーネントになります。その場合、通常、コンポーネントが持つすべてのプロパティを表す Map オブジェクトを data-sly-resource に渡すことで、仮想子コンポーネントを含んで構成される合成リソースを使用します。

#### 使用例 2：編集可能なコンポーネントを含める {#use-case-include-an-editable-component}

もうひとつの一般的な使用例は、コンテナコンポーネントがレイアウトコンテナのような編集可能な子コンポーネントを含む場合です。この場合、含まれた各子は、必ずエディターが機能するためのラッパーを必要とします（`cq:noDecoration` プロパティで明示的に無効になっている場合を除く）。

含まれるコンポーネントは、この場合、独立したコンポーネントなので、エディターが機能するためにはラッパー要素が必要で、適用するレイアウトおよびスタイルを定義する必要があります。この動作をトリガーするために、`decoration=true` オプションがあります。

`one.html: <sly data-sly-resource="${'child' @ decoration=true}"></sly>`

`two.html: Hello World!`

`/content/test.html` に出力される結果：

**`<article class="component-two">Hello World!</article>`**

#### 使用例 3：カスタム動作 {#use-case-custom-behavior}

複雑な使用例はいくつもありますが、明示的に次を提供する HTL を利用することで簡単に実現できます。

* **`decorationTagName='ELEMENT_NAME'`**：ラッパーの要素名を定義します。
* **`cssClassName='CLASS_NAME'`**：設定する CSS クラス名を定義します。

`one.html: <sly data-sly-resource="${'child' @ decorationTagName='aside', cssClassName='child'}"></sly>`

`two.html: Hello World!`

`/content/test.html` に出力される結果：

**`<aside class="child">Hello World!</aside>`**

## JSP {#jsp}

`cq:includ` または `sling:include` を使用してコンポーネントを含める場合、AEM のデフォルトの動作は、DIV を使用して要素をラッピングできます。ただし、このラッピングは 2 つの方法でカスタマイズできます。

* `cq:noDecoration` を使用してコンポーネントをラッピングしないように明示的に AEM に指定します。
* カスタム HTML タグを使用して `cq:htmlTag`／`cq:tagName` または `decorationTagName` を使用するコンポーネントをラッピングします。

### デシジョンツリー {#decision-tree-1}

次のデシジョンツリーで、`cq:noDecoration`、`cq:htmlTag`、`cq:tagName` および `decorationTagName` がどのようにラッパー動作に影響するかを説明します。

![chlimage_1-3](assets/chlimage_1-3a.jpeg)
