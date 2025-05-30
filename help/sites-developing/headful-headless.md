---
title: AEMにおけるヘッドフルとヘッドレス
description: AEM プロジェクトはヘッドフルモデルでもヘッドレスモデルで実装できますが、二者択一ではありません。AEM は、1 つのプロジェクトで両方のモデルのメリットを活用できる柔軟性を備えています。
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
exl-id: ba7f8ad9-807b-48d9-a4eb-da0a60d2494a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 100%

---

# AEM におけるヘッドフルとヘッドレス {#headful-headless}

Adobe Experience Manager プロジェクトはヘッドフルモデルでもヘッドレスモデルで実装できますが、二者択一ではありません。AEM は、1 つのプロジェクトで両方のモデルのメリットを活用できる柔軟性を備えています。このドキュメントでは、各モデルの概要と SPA 統合のレベルについて説明します。

## 概要 {#overview}

AEM には、コンテンツの作成と配信を 1 つのプラットフォームで管理するための強力なツールが用意されています。それは、従来の「ヘッドフル」コンテンツ管理モデルです。このモデルでは、コンテンツ作成者と開発者が同じプラットフォームで作業して、コンテンツ利用者にエクスペリエンスを提供します。

また、AEM をコンテンツの管理だけに使用することもでき、その場合はコンテンツの表示と配信を別のプラットフォームで管理できます。これは「ヘッドレス」コンテンツ管理モデルです。このモデルでは、コンテンツ作成者と開発者が様々なプラットフォームで作業して、コンテンツ利用者にエクスペリエンスを提供します。

しかし、これはバイナリ選択である必要はありません。AEM にはこれまでにはない柔軟性があるので、プロジェクトに両方のモデルのメリットを活用できます。

![AEM 実装モデル](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

ヘッドフルモデルまたはフルスタックモデルでは、コンテンツは AEM リポジトリで管理され、Java、HTL などに基づく AEM コンポーネントを使用して、ユーザーエクスペリエンス用にコンテンツをレンダリングします。このモデルでは、コンテンツの作成、スタイル設定、表示、配信がすべて AEM で行われます。

ヘッドレスモデルでは、コンテンツは AEM リポジトリで管理されますが、REST や GraphQL などの API を使用して別のシステムに配信されて、ユーザーエクスペリエンス用にレンダリングされます。このモデルでは、コンテンツは AEM で作成されますが、コンテンツのスタイル設定、表示、配信はすべて別のプラットフォームで行われます。

AEM がヘッドレスで配信するコンテンツの宛先は、多くの場合、単一ページアプリケーション（SPA）です。ただし、これらの SPA は完全に AEM の外部にある必要はありません。AEM では、SPA をどの程度 AEM に統合するかを決定できます。例を見てみましょう。

## Web ショップの例 {#web-shop-example}

会社の既存の Web ショップが SPA として存在するとします。その中に製品の詳細や画像がすべて含まれています。この状況で、プロモーションサイト、ブログ、キャンペーンコンテンツなどのマーケティング活動を強化するために AEM を導入します。これら 2 つをどのように統合すればよいでしょうか。AEM を使用すると、次のような幅広い選択肢があります。

* **両システムを独立して運用する。**
* **GraphQL を使用して AEM の限られたコンテンツを Web ショップに提供する。**&#x200B;コンテンツは作成者が AEM で作成できますが、表示は Web ショップ SPA でのみ可能です。
* **Web ショップ SPA を AEM に組み込む。**&#x200B;コンテンツは作成者が AEM で作成でき、AEM で Web ショップのコンテキストで表示できますが、操作はできません。
* **Web ショップ SPA を AEM に組み込み、編集可能ポイントを有効にする。**&#x200B;コンテンツは作成者が AEM で作成でき、AEM で Web ショップのコンテキストで表示できます。作成者は AEM 内で Web ショップ SPA のコンテンツを限定的に操作できます。
* **Web ショップ SPA を AEM に組み込み、ゾーン全体を編集可能にする。**&#x200B;コンテンツは作成者が AEM で作成でき、AEM で Web ショップのコンテキストで表示できます。作成者は AEM 内で Web ショップ SPA のコンテンツを限定的に操作できます。

次の節では、これらの統合レベルについて詳しく説明します。

>[!NOTE]
>
>もちろん、Web ショップ SPA を完全機能の AEM SPA として再実装することもできます（[AEM SPA Editor フレームワークを使用](/help/sites-developing/spa-walkthrough.md)既に AEM があり、web ショップまたは他の SPA を作成する場合はこの方法をお勧めしますが、このドキュメントの範囲には含まれません。

## SPA 統合レベル {#integration-levels}

SPA 統合は AEM の 4 つのレベルに分かれます。

* **レベル 0：統合なし**
   * SPA と AEM は別々に存在し、情報交換はありません。
   * コンテンツは、2 つの別個のシステムで独立に作成、管理、配信されます。
* **レベル 1：コンテンツフラグメント統合**
   * AEM で[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)を使用して、SPA 用の限られたコンテンツを作成および管理します。
   * SPA は、AEM の [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) を通じてこのコンテンツを取得します。
   * 一部のコンテンツは AEM で管理され、一部は外部システムで管理されます。
   * コンテンツは SPA でのみ表示できます。
* **レベル 2：SPA を AEM に埋め込む**
   * AEM で[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)を使用して、SPA 用のコンテンツを作成および管理します。
   * SPA は、AEM の [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) を通じてこのコンテンツを取得します。
   * 一部のコンテンツは AEM で管理され、一部は外部システムで管理されます。
   * コンテンツは AEM 内でインコンテクストで表示できます。
   * 限られたコンテンツを AEM 内で編集できます。
* **レベル 3：SPA を AEM に埋め込んで完全に有効にする**
   * AEM で[コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md)を使用して、SPA 用のコンテンツを作成および管理します。
   * SPA は、AEM の [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) を通じてこのコンテンツを取得します。
   * コンテンツは AEM 内でインコンテクストで表示できます。
   * ほとんどのコンテンツを AEM 内で編集できます。

レベル 1 は典型的なヘッドレス実装の例です。ただし、コンテンツ作成者は SPA 内でインコンテクストでのみコンテンツを表示できます。AEM はオーサリングツールにすぎません。

レベル 2 とレベル 3 では AEM のメリットと柔軟性が明白になる一方、SPA のメリットも維持されます。コンテンツ作成者は AEM でコンテンツを作成できますが、AEM 内でインコンテクストでコンテンツを表示できます。SPA は、AEM でオーサリングできるようになりますが、引き続き SPA として配信できます。

## 統合レベルの実装 {#implementing}

選択する統合レベルに応じて、使用可能な様々なツールが AEM に用意されています。各レベルは、前に使用したツールに基づいて構築されます。以下のリストは、関連するリソースへのリンクです。

* **レベル 1：**&#x200B;コンテンツフラグメントと [AEM ヘッドレスフレームワーク](/help/sites-developing/headless/introduction.md)を使用して、AEM コンテンツを SPA に配信できます。
* **レベル 2：**&#x200B;レベル 1 に加えて、
   * [RemotePage コンポーネント](/help/sites-developing/spa-remote-page.md)を使用して、外部 SPA を AEM に埋め込み、AEM コンテンツをインコンテクストで表示できます。
   * SPA の特定のポイントで [AEM での限られた編集を可能にする](/help/sites-developing/spa-edit-external.md)こともできます。
* **レベル 3：** レベル 2 に加えて、
   * SPA のゾーン全体で、AEM での包括的な編集を可能にすることができます。
