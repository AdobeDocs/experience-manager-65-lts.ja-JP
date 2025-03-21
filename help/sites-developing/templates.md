---
title: テンプレート
description: テンプレートは、新しいページのベースとして使用するページを作成する際に使用します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 3b3cff43-4edc-4250-8e6d-08eb5906ffcd
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 100%

---

# テンプレート{#templates}

テンプレートは、次のような AEM の様々な場面で使用されます。

* [ページを作成する場合、テンプレートを選択します](#templates-pages)。このテンプレートは、新しいページのベースとして使用されます。テンプレートは、ページの構造、すべての初期コンテンツおよび使用可能な[コンポーネント](/help/sites-authoring/default-components.md)（デザインプロパティ）を定義します。

ここでは、次のテンプレートについて詳しく説明します。

* [ページテンプレート - 編集可能](/help/sites-developing/page-templates-editable.md)

## テンプレート - ページ {#templates-pages}

AEM には、ページを作成するための 2 つの基本的なタイプのテンプレートが用意されています。

>[!NOTE]
>
>[ページを作成](/help/sites-authoring/managing-pages.md#creating-a-new-page)する際にテンプレートを使用する場合、（ページの作成者にとって）見た目に違いはなく、またどのタイプのテンプレートが使用されているかはわかりません。

### 編集可能なテンプレート {#editable-templates}

AEM で開発を行う場合は、編集可能テンプレートを使用することをお勧めします。

編集可能テンプレートの利点は次のとおりです。

* 作成者によって[作成](/help/sites-authoring/templates.md#creating-a-new-template-template-author)および[編集](/help/sites-authoring/templates.md#editing-a-template-structure-template-author)できます。

* テンプレートを使用して作成されたページに、次の項目を定義できるようにするために導入されました。

   * 構造
   * 初期コンテンツ
   * コンテンツポリシー

* 新しいページが作成されると、ページとテンプレートの間に動的な接続が維持されます。つまり、テンプレート構造の変更は、そのテンプレートで作成されたすべてのページに反映されます。初期コンテンツの変更は反映されません。
* デザインプロパティを保持するには、テンプレートエディターから編集できるコンテンツポリシーを使用します（ページエディター内のデザインモードは使用しません）。
* `/conf` に保存されます。
* 詳しくは、[編集可能テンプレート](/help/sites-developing/page-templates-editable.md)を参照してください。

>[!NOTE]
>
>詳しくは、[編集可能なページテンプレートを使用した Experience Manager サイトの開発](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=ja)を参照してください。

### 静的テンプレート {#static-templates}

静的テンプレート：

* 開発者が定義および設定する必要があります。
* 多くのバージョンが使用できる AEM のオリジナルのテンプレートシステムです。
* 静的テンプレートは、作成するページと同じ構造を持ち、実際のコンテンツを持たないノードの階層です。
* ページを作成するためにコピーされ、その後は動的接続は存在しません。
* デザインプロパティを保持するには、[デザインモード](/help/sites-authoring/default-components-designmode.md)を使用します。
* `/apps` に保存されます

>[!NOTE]
>
>AEM 6.5 以降では、静的テンプレートの使用はベストプラクティスとは見なされていません。その代わりに編集可能テンプレートを使用してください。
>
>[AEM 最新化](modernization-tools.md)ツールは、静的テンプレートから編集可能テンプレートへの移行に役立ちます。

### 使用可能なテンプレート {#template-availability}

>[!CAUTION]
>
>AEM は、複数のプロパティをオファーして、**Sites** で許可されるテンプレートを制御します。ただし、組み合わせることで非常に複雑なルールになり、トラックや管理が困難になる可能性があります。
>
>したがって、アドビでは、次の項目を定義して、単純に開始することをお勧めします。
>
>* プロパティは `cq:allowedTemplates` のみ
>
>* サイトのルートにのみ
>
>例えば、We.Retail `/content/we-retail/jcr:content` を参照してください。
>
>プロパティ `allowedPaths`、`allowedParents`、`allowedChildren` をテンプレートに配置して、より高度なルールを定義することもできます。ただし、可能な場合、許可されるテンプレートをさらに制限する必要がある場合は、サイトのサブセクションでさらに `cq:allowedTemplates` プロパティを定義する方が&#x200B;*はるかに*&#x200B;簡単です。
>
>また、**ページプロパティ**&#x200B;の「**詳細**」タブで、作成者が `cq:allowedTemplates` プロパティを更新できるという利点もあります。その他のテンプレートプロパティは、（標準）UI を使用して更新することはできないので、変更するたびに、ルールとコードのデプロイメントを管理する開発者が必要になります。

サイト管理インターフェイスでページを作成する場合、使用可能なテンプレートのリストは、新しいページの場所と、各テンプレートで指定されている配置制限によって異なります。

次のプロパティは、新しいページをページ `P` の子として配置する場合に、テンプレート `T` を使用できるかどうかを決定します。これらの各プロパティは、0 個以上の正規表現を保持する複数値の文字列で、パスの照合に使用されます。

* `jcr:content` サブノードの `P` または `P` の上位ページの `cq:allowedTemplates` プロパティ。

* `T` の `allowedPaths` プロパティ。

* `T` の `allowedParents` プロパティ。

* `P` のテンプレートの `allowedChildren` プロパティ。

評価は次のように行われます。

* `P` で始まるページ階層を昇順にしているときに見つかった、最初の空でない `cq:allowedTemplates` プロパティは、`T` のパスと一致します。一致する値がない場合、`T` は拒否されます。

* `T` に空でない `allowedPaths` プロパティがあるものの、 `P` のパスと一致する値がない場合、`T` は拒否されます。

* 上記のプロパティの両方が空または存在しない場合、`P` と同じアプリケーションに属さない限り、`T` は拒否されます。`T` は、`T` のパスの 2 番目のレベルの名前が `P` のパスの 2 番目のレベルの名前と同じである場合に限り、`P` と同じアプリケーションに属します。例えば、テンプレート `/apps/geometrixx/templates/foo` は、ページ `/content/geometrixx` と同じアプリに属しています。

* `T` に空でない `allowedParents` プロパティがあるものの、 `P` のパスと一致する値がない場合、`T` は拒否されます。

* `P` のテンプレートに空でない `allowedChildren` プロパティがあるものの、`T` のパスと一致する値がない場合、`T` は拒否されます。

* その他すべての場合は、`T` は許可されます。

以下の図は、テンプレートの評価プロセスを示しています。

![chlimage_1-176](assets/chlimage_1-176.png)

#### 子ページで使用するテンプレートの制限 {#limiting-templates-used-in-child-pages}

特定のページの下に子ページを作成するために使用できるテンプレートを制限するには、ページの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用して、子ページとして許可するテンプレートのリストを指定します。例えば、`/apps/geometrixx/templates/contentpage` リストの各値は、許可されている子ページのテンプレートへの絶対パスである必要があります。

テンプレートの `jcr:content` ノードの `cq:allowedTemplates` プロパティを使用すると、このテンプレートを使用するすべての新規作成ページにこの設定を適用できます。

例えばテンプレート階層に対してさらに制約を追加する場合は、テンプレートの `allowedParents/allowedChildren` プロパティを使用できます。その後、テンプレート T から作成されたページが、テンプレート T から作成されたページと親子である必要があることを明示的に指定できます。
