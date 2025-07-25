---
title: 開発者モード
description: 開発者モードで開かれるサイドパネルのタブには、現在のページに関する開発者向けの情報が表示されます。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: b30bb90b-adca-4d3a-ae15-bede70e1c39a
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 99%

---

# 開発者モード{#developer-mode}

Adobe Experience Manager（AEM）でページを編集する場合は、開発者モードなど、複数の[モード](/help/sites-authoring/author-environment-tools.md#modestouchoptimizedui)が使用可能です。これで開かれるサイドパネルのタブには、現在のページに関する開発者向けの情報が表示されます。次の 3 つのタブがあります。

* **[コンポーネント](#components)**：構造およびパフォーマンスに関する情報を表示します。
* **[テスト](#tests)**：テストを実行し、結果を分析します。
* **[エラー](#errors)**：発生している問題が表示されます。

これらのタブで、開発者は以下を実行できます。

* 検出：ページが何から作成されているかを確認します。
* デバッグ：発生したエラーとその場所およびタイミングを特定して、問題の修正に役立てます。
* テスト：アプリケーションが期待どおりに動作するかを示します。

>[!CAUTION]
>
>開発者モード：
>
>* （ページの編集時に）タッチ操作対応 UI でのみ使用できます。
>* モバイルデバイスまたはデスクトップ上の小さいウィンドウでは、スペースの制約があるので使用できません。
>
>   * ウィンドウの幅が 1024 px 未満の場合は使用できません。
>* `administrators` グループに所属しているユーザーのみ使用できます。

>[!CAUTION]
>
>開発者モードは、nosamplecontent 実行モードを使用していない標準のオーサーインスタンスでのみ使用できます。
>
>必要に応じて、次のように設定して使用できます。
>
>* nosamplecontent 実行モードを使用しているオーサーインスタンス
>* パブリッシュインスタンス
>
>使用後は再度無効にする必要があります。

>[!NOTE]
>
>詳しくは以下を参照してください。
>
>* ヒントおよびツールの詳細については、ナレッジベースの記事「[AEM TouchUI の問題のトラブルシューティング](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-16935)」。
>* [AEM 6.0 の開発者モード](https://experienceleague.adobe.com/docs/events/experience-manager-gems-recordings/gems2014/aem-developer-mode.html?lang=ja)に関する AEM Gems セッション。
>

## 開発者モードを開く {#opening-developer-mode}

開発者モードは、ページエディターのサイドパネルとして実装されます。パネルを開くには、ページエディターのツールバーにあるモードセレクターから「**開発者**」を選択します。

![chlimage_1-11](assets/chlimage_1-11.png)

パネルは、次の 2 つのタブで構成されています。

* **[コンポーネント](/help/sites-developing/developer-mode.md#components)** - コンポーネントツリーが表示されます。これは、作成者向けの[コンテンツツリー](/help/sites-authoring/author-environment-tools.md#content-tree)に似ています。

* **[エラー](/help/sites-developing/developer-mode.md#errors)** - 問題が発生すると、各コンポーネントの詳細が表示されます。

### コンポーネント {#components}

![chlimage_1-12](assets/chlimage_1-12.png)

コンポーネントツリーが表示されます。次の機能があります。

* ページ上にレンダリングされるコンポーネントとテンプレートのチェーンの概要を示します（SLY、JSP など）。このツリーを展開して、階層内のコンテキストを表示できます。
* コンポーネントをレンダリングするためのサーバーサイドの計算時間を示します。
* ツリーを展開し、ツリー内の特定のコンポーネントを選択できます。コンポーネントを選択すると、次のようなコンポーネント詳細にアクセスできます。

   * リポジトリーパス
   * スクリプトへのリンク（CRXDE Lite でアクセス）

* 選択されたコンポーネント（コンテンツフローでは青い境界線で示されます）は、コンテンツツリーで強調表示されます（その逆も同様です）。

これは次の目的に役立ちます。

* コンポーネントごとのレンダリング時間を判断し、比較します。
* 階層を確認し、理解します。
* 時間がかかっているコンポーネントを把握することで、ページの読み込み時間について理解し、向上させます。

各コンポーネントエントリの表示例を以下に示します。

![chlimage_1-13](assets/chlimage_1-13.png)

* **詳細を表示**：以下の項目を表示するリストへのリンクです。

   * コンポーネントのレンダリングに使用されるすべてのコンポーネントスクリプト。
   * この特定のコンポーネントのリポジトリーコンテンツパス。

  ![chlimage_1-14](assets/chlimage_1-14.png)

* **スクリプトを編集**：次のことを実行するリンクです。

   * CRXDE Lite でコンポーネントスクリプトを開きます。

* コンポーネントエントリを展開（矢印の先端をクリック）すると、次の項目も表示されます。

   * 選択したコンポーネント内の階層。
   * 選択したコンポーネント単独でのレンダリング時間、そのコンポーネント内にネストされている個々のコンポーネントのレンダリング時間および両者の合計。

  ![chlimage_1-15](assets/chlimage_1-15.png)

>[!CAUTION]
>
>`/libs` の下にあるスクリプトを指すリンクもあります。ただし、これらのリンクは参照専用とし、`/libs` の下層にあるものは何も編集&#x200B;**しないでください**。変更しても無駄になる可能性があるからです。これは、このブランチは、アップグレードしたりホットフィックスや機能パックを適用したりするたびに変更される傾向にあるからです。必要な変更はすべて `/apps` 下で行います。詳しくは、[オーバーレイとオーバーライド](/help/sites-developing/overlays.md)を参照してください。

### エラー {#errors}

![chlimage_1-16](assets/chlimage_1-16.png)

**エラー**&#x200B;タブは常に（上図のように）何も表示されないのが理想ですが、問題が発生すると、コンポーネントごとに以下の詳細が表示されます。

* 警告とエラーの詳細および CRXDE Lite 内の適切なコードへの直接リンク（コンポーネントによってエラーログにエントリが作成された場合）
* 警告（コンポーネントによって管理セッションが開かれた場合）

例えば、未定義のメソッドが呼び出されたときは、その結果として発生したエラーが「**エラー**」タブに表示されます。

![chlimage_1-17](assets/chlimage_1-17.png)

エラーが発生すると、「コンポーネント」タブのツリーにあるコンポーネントエントリもインジケーターでマークされます。

### テスト {#tests}

>[!CAUTION]
>
>AEM 6.2 では、開発者モードのテスト機能がスタンドアロンのツールアプリケーションとして再実装されました。
>
>詳しくは、[UI のテスト](/help/sites-developing/hobbes.md)を参照してください。
