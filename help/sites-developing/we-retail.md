---
title: We.Retail 参照実装
description: We.Retail は参照実装の技術プレビューであり、AEM を使用したオンラインプレゼンスを設定する際に推奨される方法を示しています
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 71a49353-5273-46ee-a1ff-5bbfe5b6b0b4
source-git-commit: c0bf6864bb344e582c4f88371c892d401ce2827c
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 56%

---

# `We.Retail` リファレンス実装{#we-retail-reference-implementation}

## はじめに {#introduction}

`We.Retail` のページは、Adobe Experience Managerを使用したオンラインプレゼンスの設定方法の推奨事項を示すリファレンス実装とサンプルコンテンツです。

`We.Retail` サイトでは、HTL、レスポンシブレイアウト、編集可能なテンプレート、コアコンポーネントなど、最新のAdobe Experience Manager（AEM）テクノロジーを使用しています。

これは小売業界について示していますが、サイトの設定方法は任意の業界に適用でき、商品カタログおよび買い物かご機能のみが小売特有です。

## 機能 {#features}

AEMの標準的な参照実装として、`We.Retail` ではAEMの最も強力な機能のいくつかを紹介します。

| **機能** | **説明** | **興味がある場合** |
|---|---|---|
| [グローバル化されたサイト構造](/help/sites-administering/tc-bp.md) | `We.Retail` には、国固有のサイトにライブコピーされるプライマリ言語ページが含まれます。 | [試してみる](/help/sites-developing/we-retail-globalized-site-structure.md) |
| [レスポンシブレイアウト](/help/sites-authoring/responsive-layout.md) | すべてのページには、画面やデバイスのサイズに動的に適応するレスポンシブレイアウトが採用されています。 | [試してみる](/help/sites-developing/we-retail-responsive-layout.md) |
| [編集可能テンプレート](/help/sites-developing/page-templates-editable.md) | すべてのページが編集可能テンプレートに基づいており、開発者以外のユーザーがテンプレートを変更したり、カスタマイズしたりできます。 | [試してみる](/help/sites-developing/we-retail-editable-templates.md) |
| [HTML テンプレート言語](https://experienceleague.adobe.com/ja/docs/experience-manager-htl/content/overview) | すべてのコンポーネントが HTL に基づいています。 |  |
| [コアコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/introduction) | すべてのコンポーネントが新しいコアコンポーネントに基づいており、使いやすく、設定変更も手早く行えます。 | [試してみる](/help/sites-developing/we-retail-core-components.md) |
| [コンテンツフラグメント](/help/assets/content-fragments/content-fragments.md) | `We.Retail` エクスペリエンスの節では、コンテンツフラグメントを利用したコンテンツの再利用機能を紹介します。 | [試してみる](/help/sites-developing/we-retail-content-fragments.md) |
| [エクスペリエンスフラグメント](/help/sites-authoring/experience-fragments.md) | エクスペリエンスフラグメントは、ページ内で参照できるコンテンツおよびレイアウトを含む 1 つ以上のコンポーネントのグループです。 | [試してみる](/help/sites-developing/we-retail-experience-fragments.md) |

## 今すぐ始める {#getting-started}

`We.Retail` サイトは、AEMのサンプルコンテンツとして提供されます。 使用するには、[通常どおりに AEM を起動する](/help/sites-deploying/deploy.md#getting-started)だけです。このとき、サンプルコンテンツが無効になっていないことを確認してください。

>[!CAUTION]
>
>`We.Retail` を実稼動インスタンスにインストールしないでください。 実稼動インスタンスは、`nosamplecontent` [実行モード](/help/sites-deploying/configure-runmodes.md)で開始する必要があります。

>[!CAUTION]
>
>`We.Retail` サイトは最新のAEM テクノロジーに基づいているので、[ クラシック UI オーサリング ](/help/sites-classic-ui-authoring/classic-page-author-first-steps.md) をサポートしていません。

### 最新バージョン {#latest-version}

`We.Retail` はAEM リリースと共に配布されますが、リリース後にコンテンツおよびその機能が更新される可能性があります。 そのため、[GitHub から最新リリースをダウンロード ](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases) した後、AEM インスタンスにパッケージとして [ アップロード ](/help/sites-administering/package-manager.md#uploading-packages-from-your-file-system) および [ インストール ](/help/sites-administering/package-manager.md#installing-packages) することができます。

### 最初の手順 {#first-steps}

1. AEMが起動（またはインストール）され `We.Retail` と、サイトコン **`We.Retail`** ールは [Sites コンソール ](/help/sites-authoring/basic-handling.md#global-navigation) で使用できるようになります。
1. 例えば、次のページを開くことができ、そのページは後述の[付録](#appendix)のように表示されます。

   `https://<server name>:<port number>/editor.html/content/we-retail/language-masters/en.html`

## `We.Retail` とGeometrixx {#we-retail-geometrixx}

以前のバージョンの AEM では、サンプルコンテンツとして Geometrixx とその多くの実例が提供されてきました。バージョン 6.3 以降、`We.Retail` はAEMに付属するサンプルコンテンツであり、新しい標準のリファレンス実装として機能します。

この `We.Retail` サイトは技術的により堅牢で、最新のAEM テクノロジを活用して柔軟性と拡張性を高めると同時に、最新の機能を紹介しています。

### 機能の比較 {#feature-comparison}

次の表に、Geometrixxと比較して `We.Retail` で利用できる主な機能の概要を示します。

* **使用可能**&#x200B;は、サンプルコンテンツに機能の例が含まれていることを意味します。
* **使用できません** は、サンプルコンテンツには機能例がないものの、機能は引き続き使用できる可能性があることを意味します。


| **機能** | **`We.Retail`** | **Geometrixx** |
|---|---|---|
| グローバル化されたサイト構造 | プライマリ言語ページは、国固有のサイトにライブコピーされます | 使用不可 |
| コンテンツフラグメント | 使用可 | 使用不可 |
| エクスペリエンスフラグメント | 使用可 | 使用不可 |
| レスポンシブレイアウト | すべてのページ | Geometrixx Media のみ |
| 編集可能なテンプレート | すべてのページ | 使用不可 |
| HTL | すべてのコンポーネント | 限定的 |
| ターゲティング | すべてのページ | Geometrixx Outdoors のみ |
| 原稿 | 使用不可 | 使用可 |
| カルーセルビューア、ダウンロード、グラフのコンポーネント | 使用不可 | 使用可 |
| 列の制御 | レイアウトコンテナに置き換えられる | 使用可 |
| Forms | 使用不可 | 使用可 |
| Campaign | メールのサンプルはない | 使用可 |

>[!NOTE]
>
>このリストは、完全を期していますが、あらゆる機能を網羅しているわけではありません。

## コントリビューション {#contribute}

`We.Retail` サイトはオープンソースプロジェクトとしてリリースされ、ソースコードの最新バージョンは GitHub からダウンロードできます。

GitHub のコード

このページのコードは GitHub にあります。

* [GitHub の aem-sample-we-retail プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail)
* プロジェクトを [ZIP ファイル](https://codeload.github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/zip/refs/heads/master)としてダウンロードします

最新のリリースは、インストール可能なパッケージとして[直接ダウンロード](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases/tag/we.retail.reactor-4.0.0)することもできます。

問題が発生した場合は、[GitHub の Issues](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/issues) に記入します。

自由にフォークするか、[プルリクエスト](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/pulls)によって貢献してください。

## プレビュー {#preview}

`We.Retail` のようこそページのプレビュー：

![screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32](assets/screencapture-localhost-4502-editor-html-content-we-retail-us-en-html-2018-08-17-14_33_32.png)
