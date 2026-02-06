---
title: Adobe Experience Manager Sites でのエクスペリエンスフラグメント開発
description: Adobe Experience Manager でのエクスペリエンスフラグメントのカスタマイズ方法について説明します。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: bc621086-8128-4836-a580-dca99f61c439
source-git-commit: d894bb145d70fba819cc8452056e9e46112e69d9
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 63%

---

# エクスペリエンスフラグメント {#experience-fragments}

## 基本知識 {#the-basics}

[エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md)は、ページ内で参照できるコンテンツおよびレイアウトを含む 1 つ以上のコンポーネントのグループです。

プライマリまたはバリアントのエクスペリエンスフラグメント、あるいはその両方が、次を使用します。

* `sling:resourceType`：`/libs/cq/experience-fragments/components/xfpage`

`/libs/cq/experience-fragments/components/xfpage/xfpage.html` ールがないため、次の状態に戻ります。

* `sling:resourceSuperType`：`wcm/foundation/components/page`

## プレーンなHTML レンディション {#the-plain-html-rendition}

URL で `.plain.` セレクターを使用すると、プレーン HTML レンディションにアクセスできます。

この機能は、ブラウザーから利用できます。 ただし、その主な目的は、他のアプリケーション（例えば、サードパーティ web アプリ、カスタムモバイル実装など）が、URL のみを使用して、エクスペリエンスフラグメントのコンテンツに直接アクセスできるようにすることです。

プレーン HTML レンディションは、次のようなパスにプロトコル、ホストおよびコンテキストパスを追加します。

* タイプが `src`、`href`、`action` のいずれか

* または、`-src` か `-href` で終わる

次に例を示します。

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>リンクは、常にパブリッシュインスタンスを参照します。 サードパーティがこれらのリンクを使用するので、オーサリングインスタンスではなく、常にパブリッシュインスタンスからリンクを呼び出します。
>
>詳しくは、[URL の外部化 &#x200B;](/help/sites-developing/externalizer.md) を参照してください。

![xf-14](assets/xf-14.png)

プレーンレンディションセレクターでは、追加のスクリプトとは異なり、変換 [`Sling Rewriter`](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) を使用します。プレーンレンディションは変換ツールとして使用され、次のように設定されます。

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### HTML レンディションの生成の設定 {#configuring-html-rendition-generation}

HTML レンディションは、`Sling Rewriter` パイプラインを使用して生成されます。 パイプラインは、`/libs/experience-fragments/config/rewriter/experiencefragments` で定義されます。HTML 変換サービスでは、次のオプションをサポートしています。

* `allowedCssClasses`
   * 最終レンディションに残す CSS クラスに一致する正規表現。
   * 顧客が特定の CSS クラスを取り除きたい場合に役立ちます
* `allowedTags`
   * 最終的なレンディションで許可される HTML タグのリスト。
   * デフォルトでは、設定なしで次のタグが許可されます。html、head、title、body、img、p、span、ul、li、a、b、i、em、strong、h1、h2、h3、h4、h5、h6、br、`noscript`、div、link および script。

オーバーレイを使用してリライターを設定することをお勧めします。 [オーバーレイ](/help/sites-developing/overlays.md)を参照してください

## ソーシャルのバリエーション {#social-variations}

ソーシャルバリエーションをソーシャルメディア（テキストおよび画像）に投稿できます。Adobe Experience Manager（AEM）では、これらのソーシャルバリエーションに、テキストコンポーネントや画像コンポーネントなどのコンポーネントを含めることができます。

任意の画像またはテキストリソースタイプから、任意の深度でソーシャル投稿画像とテキストを取得できます。 リソースは、構築ブロックまたはレイアウトコンテナのいずれかから取得できます。

また、ソーシャルバリエーションを使用すると、（パブリッシュ環境で）ソーシャルアクションを行う際に構築ブロックを考慮に入れることもできます。

的確なテキストと画像をソーシャルメディアネットワークに投稿するには、カスタマイズした独自のコンポーネントを開発する場合、いくつかの規則に従う必要があります。

次のプロパティを使用する必要があります。

* 画像を抽出する場合

   * `fileReference`
   * `fileName`

* テキストを抽出する場合

   * `text`

この規則を使用するコンポーネントのみが考慮されます。

## エクスペリエンスフラグメントのテンプレート {#templates-for-experience-fragments}

>[!CAUTION]
>
>エクスペリエンスフラグメントでサポートされているのは、[編集可能なテンプレート](/help/sites-developing/page-templates-editable.md)***だけ***&#x200B;です。
>
>エクスペリエンスフラグメントは、編集可能なテンプレートに基づくページでのみ使用できます。

エクスペリエンスフラグメントの新しいテンプレートを開発する際は、[編集可能なテンプレート](/help/sites-developing/page-templates-editable.md)の標準的な手法に従うことができます。

**エクスペリエンスフラグメントを作成** ウィザードが検出するエクスペリエンスフラグメントテンプレートを作成するには、次のいずれかのルールセットに従う必要があります。

1. 次の両方：

   1. テンプレート（初期ノード）のリソースタイプは、次のものから継承する必要があります。
      `cq/experience-fragments/components/xfpage`

   1. テンプレートの名前は次の文字列で始まる必要があります。
      `experience-fragments`
このフォルダーの `/content/experience-fragments` プロパティには、`cq:allowedTemplates` で始まる名前を持つすべてのテンプレートが含まれるので、ユーザーは `experience-fragment` でエクスペリエンスフラグメントを作成できます。 ユーザーは、このプロパティを更新して、独自の命名方式やテンプレート場所を取り入れることができます。

1. [使用可能なテンプレート](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder)はエクスペリエンスフラグメントコンソールで設定できます。
<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## エクスペリエンスフラグメントのコンポーネント {#components-for-experience-fragments}

[エクスペリエンスフラグメントで使用するコンポーネントの開発は、標準的な方法に従って行います。](/help/sites-developing/components.md)

唯一の追加設定は、コンポーネントをテンプレートで確実に使用できるようにするだけです。この機能は、[&#x200B; コンテンツポリシー &#x200B;](/help/sites-developing/page-templates-editable.md#content-policies) で実現されます。

## エクスペリエンスフラグメントの Link Rewriter Provider - HTML {#the-experience-fragment-link-rewriter-provider-html}

AEM では、エクスペリエンスフラグメントを作成できます。エクスペリエンスフラグメントは、

* コンポーネントグループとレイアウトで構成されます。
* AEM ページとは独立して存在できます。

このようなグループのユースケースの 1 つは、Adobe Target などのサードパーティのタッチポイントにコンテンツを埋め込む場合です。

### デフォルトのリンク書き換え {#default-link-rewriting}

[Target にエクスポート](/help/sites-administering/experience-fragments-target.md)機能を使用すると、次の操作が可能です。

* エクスペリエンスフラグメントを作成する
* エクスペリエンスフラグメントにコンポーネントを追加する
* エクスペリエンスフラグメントを HTML 形式または JSON 形式で Adobe Target オファーとして書き出す

この機能は、[AEM のオーサーインスタンスで有効にする](/help/sites-administering/experience-fragments-target.md#Prerequisites)ことができます。有効な Adobe Target 設定と、Link Externalizer の設定が必要です。

Link Externalizer は、Target オファーの HTML バージョンを作成する際に必要な正しい URL を決定するために使用します。オファーは、その後 Adobe Target に送信されます。Adobe Targetでは、Target HTML オファー内のすべてのリンクへの公開アクセスが必要です。 エクスペリエンスフラグメントと、これらのリンクが参照するリソースを、使用前に公開します。


デフォルトでは、Target HTML オファーを作成すると、AEM のカスタム Sling セレクターにリクエストが送信されます。このセレクターの名前は `.nocloudconfigs.html` です。これはエクスペリエンスフラグメントのプレーン HTML レンダリングを作成しますが、その名前が示すとおり、クラウド設定を含んでいません（クラウド設定は余分な情報です）。

HTMLページを生成すると、`Sling Rewriter` のパイプラインで出力に変更が加えられます。

1. `html`、`head`、`body` の各要素が `div` 要素に置き換わります。`meta`、`noscript` および `title` 要素は削除されます（これらは元の `head` 要素の子要素であり、`div` 要素に置き換えられた場合には考慮されません）。

   このような処理が行われるのは、HTML Target オファーを Target アクティビティに確実に含めることができるようにするためです。

1. AEM では、HTML に存在するすべての内部リンクを変更して、公開されたリソースを指すようにします。

   変更するリンクを決定するために、AEM では HTML 要素の次の属性パターンに従います。

   1. `src` 属性
   1. `href` 属性
   1. `*-src` 属性（data-src、custom-src など）
   1. `*-href` 属性（`data-href`、`custom-href`、`img-href` など）

   >[!NOTE]
   >
   >通常、HTML 内の内部リンクは相対リンクですが、カスタムコンポーネントの HTML で完全な URL が指定されている場合もあります。デフォルトでは、AEM はこれらの完全な URL を無視し、変更しません。

   これらの属性内のリンクはAEM Link Externalizer `publishLink()` を通過し、URL を公開済みインスタンス上にあるかのように、また、公開済みインスタンス上にある URL として再作成します。

標準の実装を使用する場合、上記のプロセスで十分に、エクスペリエンスフラグメントから Target オファーを生成し、それをAdobe Targetに書き出します。 ただし、このプロセスで考慮されないユースケースとしては、次のようなものがあります。

* Sling マッピングは、パブリッシュインスタンスでのみ使用できます。
* Dispatcherがリダイレクトする。

これらのユースケースのために、AEM には Link Rewriter Provider インターフェイスが用意されています。

### Link Rewriter プロバイダーインターフェイス {#link-rewriter-provider-interface}

（[デフォルトのリンク書き換え](#default-link-rewriting)では対応していない）より複雑な場合のために、AEM では Link Rewriter Provider フェイスを提供しています。このワークフローは、バンドルにサービスとして実装できる `ConsumerType` インターフェイスです。 このインターフェイスは、エクスペリエンスフラグメントからレンダリングされる HTML オファーの内部リンクに対して AEM で実行される変更をバイパスします。このインターフェイスを使用すると、内部 HTML リンクの書き換えプロセスをビジネスニーズに合わせてカスタマイズできます。

このインターフェイスをサービスとして実装する使用例としては、例えば次のものがあります。

* Sling マッピングは、パブリッシュインスタンスでは有効になっていますが、オーサーインスタンスでは有効になっていません。
* Dispatcherまたは同様のテクノロジーを使用して、URL を内部にリダイレクトします。
* リソースには `sling:alias` のメカニズムが存在します。

>[!NOTE]
>
>このインターフェイスでは、生成された Target オファーからの内部 HTML リンクのみ処理します。

Link Rewriter Provider インターフェイス（`ExperienceFragmentLinkRewriterProvider`）は次のとおりです。

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Link Rewriter プロバイダーインターフェイスの使用方法 {#how-to-use-the-link-rewriter-provider-interface}

このインターフェイスを使用するには、まず、Link Rewriter Provider インターフェイスを実装する新しいサービスコンポーネントを含むバンドルを作成する必要があります。

このサービスは、様々なリンクにアクセスできるように、エクスペリエンスフラグメントの「Target に書き出し」機能でのリンク書き換えにプラグインするために使用します。

例えば、`ComponentService` の場合は次のようになります。

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

このサービスが機能するには、次の 3 つのメソッドをサービス内に実装する必要があります。

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

エクスペリエンスフラグメントの特定のバリエーションに対して「Adobe Target に書き出し」機能が呼び出された場合に、リンクを書き換える必要があるかどうかをシステムに指定する必要があります。これは、次の方法を使用して **実装** できます。


`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

例：

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

このメソッドは、現在「Adobe Target に書き出し」システムによる書き換えの対象となっているエクスペリエンスフラグメントバリエーションをパラメーターとして受け取ります。

上記の例では、次の内容を書き換えます。

* `src` に指定されているリンク

* `href` 属性のみ

* 特定のエクスペリエンスフラグメントの場合：
  `/content/experience-fragment/master`

Target に書き出しシステムは、それを通過する他のエクスペリエンスフラグメントを無視し、このサービスはそれらに影響を与えません。

#### rewriteLink {#rewritelink}

書き換えプロセスの影響を受けたエクスペリエンスフラグメントのバリエーションについては、次に、リンクの書き換えをサービスが処理できるようにします。 内部 HTML でリンクが検出されるたびに、次のメソッドが呼び出されます。

`rewriteLink(String link, String tag, String attribute)`

このメソッドは入力として次のパラメーターを受け取ります。

* `link`：
処理中のリンクの `String` 表現です。通常は、オーサーインスタンス内のリソースを指す相対 URL です。

* `tag`：
処理中の HTML 要素の名前です。

* `attribute`
正確な属性名です。

例えば、Target システムに書き出しがこの要素を処理している場合は、`CSSInclude` を次のように定義できます。

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

`rewriteLink()` メソッドの呼び出しは、次のパラメーターを使用して行います。

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

サービスを作成する際は、指定された入力に基づいて判断し、それに応じてリンクを書き換えることができます。

例えば、URL の `/etc.clientlibs` の部分を削除し、適切な外部ドメインを追加するとします。 話を簡単にするために、`rewriteLinkExample2` に示すように、サービスのリソースリゾルバーにアクセスできるとします。

>[!NOTE]
>
>サービスユーザーを通じてリソースリゾルバーを取得する方法について詳しくは、[AEMのサービスユーザー &#x200B;](/help/sites-administering/security-service-users.md) を参照してください。

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>上記のメソッドが `null` を返した場合、Target システムに書き出しは、リンクをそのままの状態（リソースへの相対リンク）にしておきます。

#### 優先度 - getPriority {#priorities-getpriority}

様々なタイプのエクスペリエンスフラグメントをサポートするために、複数のサービスが必要になる場合があります。 また、汎用サービスを使用して、すべてのエクスペリエンスフラグメントを外部化し、マッピングすることもできます。 このような場合、使用するサービスに関するの競合が発生する可能性があるので、AEM では、様々なサービスの&#x200B;**優先度**&#x200B;を定義できるようになっています。優先度は、次のメソッドを使用して指定します。

* `getPriority()`

このメソッドを使用すると、複数のサービスを使用しても、同じエクスペリエンスフラグメントについては `shouldRewrite()` メソッドが true を返すようにすることができます。`getPriority()` メソッドから最高の優先度が返されるサービスが、対象となっているエクスペリエンスフラグメントバリエーションを処理するサービスになります。

例えば、エクスペリエンスフラグメントのすべてのバリエーションについて `shouldRewrite()` メソッドが `true` を返す場合にすべてのエクスペリエンスフラグメントの基本マッピングを処理する `GenericLinkRewriterProvider` を用意することができます。一部の特定のエクスペリエンスフラグメントについては、特別な処理が必要になる場合があります。その場合は、一部のエクスペリエンスフラグメントバリエーションについてのみ `shouldRewrite()` メソッドが true を返すような `SpecificLinkRewriterProvider` を用意することができます。それらのエクスペリエンスフラグメントバリエーションを処理するために `SpecificLinkRewriterProvider` が必ず選択されるようにするには、そのプロバイダーの `getPriority()` メソッドで返される優先度が `GenericLinkRewriterProvider.` の場合より高くなるようにする必要があります。
