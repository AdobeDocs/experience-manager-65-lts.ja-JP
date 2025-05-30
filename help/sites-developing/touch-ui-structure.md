---
title: Adobe Experience Manager タッチ操作対応 UI の構造
description: Adobe Experience Manager に実装されているタッチ操作向け UI には、基盤となる原則があり、いくつかの主要な要素で構成されています
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 1fcf6de4-30b5-46cb-9c1d-109a160d5030
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 100%

---

# Adobe Experience Manager タッチ操作対応 UI の構造{#structure-of-the-aem-touch-enabled-ui}

AEM タッチ操作対応 UI には、基盤となる原則があり、いくつかの主要な要素で構成されています。

## コンソール {#consoles}

### 基本レイアウトとサイズ変更 {#basic-layout-and-resizing}

UI はモバイルデバイスとデスクトップデバイスの両方に対応します。アドビでは、2 つのスタイルを作成するのではなく、すべての画面とデバイスで機能する 1 つのスタイルを使用することにしました。

すべてのモジュールで同じ基本レイアウトを使用すると、AEM では次のような表示になります。

![chlimage_1-142](assets/chlimage_1-142.png)

レイアウトはレスポンシブデザインスタイルに従っており、使用するデバイスやウィンドウのサイズに収まるように自動で調整されます。

例えば、解像度が 1024 px 未満（モバイルデバイスなど）になると、それに応じて表示が調整されます。

![chlimage_1-143](assets/chlimage_1-143.png)

### Header Bar {#header-bar}

![chlimage_1-144](assets/chlimage_1-144.png)

ヘッダーバーにはグローバル要素が表示されます。

* ロゴおよび現在使用している特定の製品またはソリューション（AEM の場合は、グローバルナビゲーションへのリンクにもなります）
* 検索
* ヘルプリソースにアクセスするためのアイコン
* その他のソリューションにアクセスするためのアイコン
* ユーザー対応が必要なアラートまたはインボックス項目のインジケーター（またはそれらへのアクセス）
* ユーザーのプロファイル管理へのリンクになっているユーザーアイコン

### ツールバー {#toolbar}

現在の場所に応じて変わり、下のページのビューやアセットの制御に関連したツールが表示されます。ツールバーは製品固有ですが、要素には若干共通性があります。

どの場所でも、ツールバーには現在実行可能なアクションが表示されます。

![chlimage_1-145](assets/chlimage_1-145.png)

また、現在リソースが選択されているかどうかによっても異なります。

![chlimage_1-146](assets/chlimage_1-146.png)

### 左レール {#left-rail}

左レールは、必要に応じて表示／非表示を切り替えることができます。

* **タイムライン**
* **参照**
* **フィルター**

デフォルトは、**コンテンツのみ**&#x200B;です（パネルは非表示）。

![chlimage_1-147](assets/chlimage_1-147.png)

## ページオーサリング {#page-authoring}

ページをオーサリングする場合、構造化された領域は次のようになります。

### コンテンツフレーム {#content-frame}

ページコンテンツがコンテンツフレームでレンダリングされます。コンテンツフレームはエディターから独立しており、CSS や JavaScript による競合が発生しないようにします。

コンテンツフレームは、ウィンドウの右側セクションの、ツールバーの下に表示されます。

![chlimage_1-148](assets/chlimage_1-148.png)

### エディターフレーム {#editor-frame}

エディターフレームによって編集機能が実現されます。

エディターフレームは、すべてのページオーサリング要素のためのコンテナ（抽象）です。コンテンツフレームの上にあり、以下が含まれます&#x200B;*。*

* 上部のツールバー
* サイドパネル
* すべてのオーバーレイ
* その他のページオーサリング要素（コンポーネントツールバーなど）

![chlimage_1-149](assets/chlimage_1-149.png)

### サイドパネル {#side-panel}

アセットとコンポーネントを選択できる 2 つのデフォルトタブが含まれています。ここからドラッグしてページにドロップできます。

サイドパネルはデフォルトでは非表示です。選択すると、左側に表示されるか、横にスライドしてウィンドウ全体を覆います（モバイルデバイスのように、ウィンドウサイズが幅 1024 px 未満の場合）。

![chlimage_1-150](assets/chlimage_1-150.png)

### サイドパネル - アセット {#side-panel-assets}

「アセット」タブでは、一連のアセットから選択できます。特定の用語でフィルタリングしたり、グループを選択することもできます。

![chlimage_1-151](assets/chlimage_1-151.png)

### サイドパネル - アセットグループ {#side-panel-asset-groups}

「アセット」タブにはドロップダウンがあり、特定のアセットグループを選択できます。

![chlimage_1-152](assets/chlimage_1-152.png)

### サイドパネル - コンポーネント {#side-panel-components}

「コンポーネント」タブでは、一連のコンポーネントから選択できます。特定の用語でフィルタリングしたり、グループを選択することもできます。

![chlimage_1-153](assets/chlimage_1-153.png)

### オーバーレイ {#overlays}

コンテンツフレームをオーバーレイし、コンポーネントおよびそのコンテンツとの（透過的な）インタラクション方法を実現するために、[レイヤー](#layer)によって使用されます。

オーバーレイは、エディターフレーム内に（他のすべてのページオーサリング要素と共に）ありますが、実際はコンテンツフレームの適切なコンポーネントにオーバーレイします。

![chlimage_1-154](assets/chlimage_1-154.png)

### レイヤー {#layer}

レイヤーは、独立した機能バンドルであり、アクティベートすると次のことが可能です。

* ページを別のビューで表示
* ページの操作やインタラクションが可能

レイヤーを使用すると、個々のコンポーネントに特定のアクションが提供されるのではなく、ページ全体に高度な機能が提供されます。

AEM には、編集、プレビュー、注釈など、ページオーサリング用のレイヤーがいくつか実装済みです。

>[!NOTE]
>
>レイヤーは、ユーザーのページコンテンツの表示や操作に影響を与える強力な概念です。独自のレイヤーを開発する場合は、レイヤーを終了する際にクリーンアップするようにしてください。

### レイヤースイッチャー {#layer-switcher}

レイヤースイッチャーを使用して、使用するレイヤーを選択できます。閉じた場合は、現在使用中のレイヤーを示します。

レイヤースイッチャーは、ツールバー（ウィンドウ上部、エディターフレーム内）からドロップダウンとして使用できます。

![chlimage_1-155](assets/chlimage_1-155.png)

### コンポーネントツールバー {#component-toolbar}

コンポーネントの各インスタンスは、（1 回クリックするか、ゆっくりしたダブルクリックで）クリックするとツールバーを表示します。ツールバーには、ページ上のコンポーネントインスタンス（編集可能）で使用できる特定のアクション（コピー、ペースト、エディターを開くなど）が含まれます。

表示可能なスペースによって、コンポーネントツールバーは、適切なコンポーネントの右上または右下の隅に配置されます。

![chlimage_1-156](assets/chlimage_1-156.png)

## その他の情報 {#further-information}

タッチ操作対応 UI に関する概念について詳しくは、[AEM タッチ操作対応 UI の概念](/help/sites-developing/touch-ui-concepts.md)の記事を参照してください。

技術情報について詳しくは、タッチ操作対応ページエディター用の [JS ドキュメントセット](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html)を参照してください。
