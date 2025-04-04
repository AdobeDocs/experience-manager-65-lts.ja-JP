---
title: ページコンテンツの編集
description: コンテンツの追加は、ページにドラッグ可能なコンポーネントを使用して行います。コンポーネントはその後、そのまま編集したり、移動や削除をおこなったりすることができます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: be81e33d-8e37-4a57-bcc1-78e968c64641
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1829'
ht-degree: 100%

---

# ページのコンテンツの編集{#editing-page-content}

ページが作成されたら（新規またはローンチまたはライブコピーの一部として）、コンテンツを編集して、必要な更新を行うことができます。

コンテンツは、ページにドラッグ可能な[コンポーネント](/help/sites-classic-ui-authoring/classic-page-author-default-components.md)（コンテンツのタイプに適したもの）を使用して追加できます。コンポーネントはその後、そのまま編集したり、移動や削除をおこなったりすることができます。

>[!NOTE]
>
>[適切なアクセス権](/help/sites-administering/security.md)と、ページ編集（コンポーネントの追加、編集または削除、注釈、ロック解除など）のための[権限](/help/sites-administering/security.md#permissions)を持つアカウントが必要です。
>
>問題が発生した場合は、システム管理者にお問い合わせください。

## サイドキック {#sidekick}

サイドキックは、ページのオーサリングを行う際の重要なツールです。ページのオーサリング中はフローティングされるので、常に表示されます。

次のような複数のタブとアイコンを利用できます。

* コンポーネント
* ページ
* 情報
* バージョン管理
* ワークフロー
* モード
* 基礎モード
* ClientContext
* web サイト

![chlimage_1-71](assets/chlimage_1-71.png)

これらのタブやアイコンから、次のような幅広い機能にアクセスできます。

* [コンポーネントの選択](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#sidekick)
* [参照の表示](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#showing-references)
* [監査ログへのアクセス](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#audit-log)
* [モードの切り替え](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)
* バージョンの[作成](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#creating-a-new-version)、[復元](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#restoring-a-page-version-from-sidekick)および[比較](/help/sites-classic-ui-authoring/classic-page-author-work-with-versions.md#comparing-with-a-previous-version)

* ページの[公開](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#publishing-a-page)、[非公開](/help/sites-classic-ui-authoring/classic-page-author-publish-pages.md#unpublishing-a-page)

* [ページプロパティの編集 ](/help/sites-classic-ui-authoring/classic-page-author-edit-page-properties.md)

* [基礎モード](classic-feature-scaffolding.md)

* [クライアントコンテキスト](/help/sites-administering/client-context.md)

## コンポーネントの挿入 {#inserting-a-component}

### コンポーネントの挿入 {#inserting-a-component-1}

ページを開いたら、コンテンツの追加を開始できます。コンテンツの追加を行うには、コンポーネント（「段落」とも呼ばれる）を追加します。

新しいコンポーネントを挿入するには：

1. 挿入する段落のタイプを選択するには、次のようないくつかの方法があります。

   * 「**コンポーネントまたはアセットをここにドラッグします**」というラベルが付いた領域をダブルクリックします。**新規コンポーネントを挿入**&#x200B;ツールバーが開きます。コンポーネントを選択して、「**OK**」をクリックします。

   * サイドキックと呼ばれるフローティングツールバーからコンポーネントをドラッグして、新しい段落を挿入します。
   * 既存の段落を右クリックして、「**新規**」を選択します。新規コンポーネントを挿入ツールバーが開きます。コンポーネントを選択して、「**OK**」をクリックします。

   ![screen_shot_2012-02-15at115605am](assets/screen_shot_2012-02-15at115605am.png)

1. サイドキックと&#x200B;**新規コンポーネントを挿入**&#x200B;ツールバーの両方に、使用可能なコンポーネント（段落タイプ）のリストが表示されます。これらの段落タイプは様々なセクション（「一般」、「列」など）に分類され、必要に応じて展開できます。

   表示されるオプションは、実稼働環境によって異なります。コンポーネントについて詳しくは、[デフォルトコンポーネント](/help/sites-classic-ui-authoring/classic-page-author-default-components.md)を参照してください。

1. ページに必要なコンポーネントを挿入します。次に、段落をダブルクリックすると、段落を設定してコンテンツを追加できるウィンドウが開きます。

### コンテンツファインダーを使用したコンポーネントの挿入 {#inserting-a-component-using-the-content-finder}

[コンテンツファインダー](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder)からアセットをドラッグして、ページに新しいコンポーネントを追加することもできます。この操作により、アセットを含んだ適切なタイプのコンポーネントが自動的に作成されます。

これは次のアセットタイプに有効です（一部はページや段落システムに依存します）。

| アセットタイプ | 結果のコンポーネントのタイプ |
|---|---|
| 画像 | 画像 |
| ドキュメント | ダウンロード |
| 製品 | 製品 |
| ビデオ | Flash |

>[!NOTE]
>
>この動作は使用しているインストール環境に応じて設定できます。詳しくは、[アセットをドラッグするとコンポーネントインスタンスが作成されるように段落システムを設定する](/help/sites-developing/developing-components.md#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance)を参照してください。

前述のいずれかのアセットタイプをドラッグしてコンポーネントを作成するには：

1. ページが&#x200B;[**編集**&#x200B;モード](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#page-modes)であることを確認します。
1. [コンテンツファインダー](/help/sites-classic-ui-authoring/classic-page-author-env-tools.md#the-content-finder)を開きます。
1. 必要なアセットを必要な位置にドラッグします。コンポーネントの配置先が[コンポーネントプレースホルダー](#componentplaceholder)に表示されます。

   選択したアセットを格納した、アセットタイプに適したコンポーネントが必要な場所に作成されます。

1. 必要に応じて、コンポーネントを[編集](#editmovecopypastedelete)します。

## コンポーネント（コンテンツとプロパティ）の編集 {#editing-a-component-content-and-properties}

既存の段落を編集するには、次のいずれかの操作を実行します。

* 段落を&#x200B;**ダブルクリック**&#x200B;して開きます。段落を作成したときと同じウィンドウと、既存のコンテンツが表示されます。変更を行い、「**OK**」をクリックします。

* 段落を&#x200B;**右クリック**&#x200B;して、「**編集**」をクリックします。

* 段落を 2 回&#x200B;**クリック**（ゆっくりダブルクリック）して、インプレース編集モードを開始します。ページ上のテキストを、ダイアログウィンドウ内ではなく直接編集できます。このモードでは、ページ最上部にツールバーが表示されます。変更を行うと、その内容は自動的に保存されます。

## コンポーネントの移動 {#moving-a-component}

段落を移動するには：

>[!NOTE]
>
>[切り取りと貼り付け](#cut-copy-paste-a-component)を使用して、コンポーネントを移動することもできます。

1. 移動する段落を選択します。

   ![screen_shot_2012-02-15at115855am](assets/screen_shot_2012-02-15at115855am.png)

1. 段落を新しい場所にドラッグします。段落を移動できる場所が緑のチェックマークで示されます。目的の場所にドロップします。
1. 段落が移動されます。

   ![screen_shot_2012-02-15at120030pm](assets/screen_shot_2012-02-15at120030pm.png)

## コンポーネントの削除 {#deleting-a-component}

段落を削除するには：

1. 段落を選択し、**右クリック**&#x200B;します。

   ![screen_shot_2012-02-15at120220pm](assets/screen_shot_2012-02-15at120220pm.png)

1. メニューから「**削除**」を選択します。段落の削除を確認するメッセージが AEM WCM に表示されます。削除の操作を元に戻すことはできません。
1. 「**OK**」をクリックします。

>[!NOTE]
>
>[グローバル編集ツールバーを表示するためのユーザープロパティ](/help/sites-classic-ui-authoring/author-env-user-props.md)を設定している場合、表示される「**コピー**」、「**切り取り**」、「**貼り付け**」、「**削除**」の各ボタンを使用して、段落に対する特定の操作を実行できます。
>
>様々な[キーボードショートカット](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)も利用できます。

## コンポーネントの切り取り／コピー／貼り付け {#cut-copy-paste-a-component}

[コンポーネントを削除](#deleting-a-component)するときと同様に、コンテキストメニューを使用してコンポーネントのコピー、切り取り、貼り付けを行うことができます。

>[!NOTE]
>
>[グローバル編集ツールバーを表示するためのユーザープロパティ](/help/sites-classic-ui-authoring/author-env-user-props.md)を設定している場合、表示される「**コピー**」、「**切り取り**」、「**貼り付け**」、「**削除**」の各ボタンを使用して、段落に対する特定の操作を実行できます。
>
>様々な[キーボードショートカット](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)も利用できます。

>[!NOTE]
>
>コンテンツの切り取り、コピーおよび貼り付けは、同じページ内でのみサポートされています。

## 継承されたコンポーネント {#inherited-components}

継承されたコンポーネントは、次のような様々なシナリオによって生成されます。

* [マルチサイト管理](/help/sites-administering/msm.md)。[基礎モード](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md#scaffolding-with-msm-inheritance)と組み合わせて使用されます。

* [ローンチ](/help/sites-classic-ui-authoring/classic-launches.md)（ライブコピーをベースとしている場合）
* 特定のコンポーネント（Geometrixx 内の継承された段落システムなど）

継承はキャンセル（その後再度有効化）できます。コンポーネントによって、次の場所から操作できます。

1. **ライブコピー**

   コンポーネントがライブコピーまたはローンチに含まれる場合は、南京錠アイコンで示されます。この南京錠アイコンをクリックして継承をキャンセルできます。

   * 南京錠アイコンは、コンポーネントの選択時に、次のように表示されます。

   ![chlimage_1-72](assets/chlimage_1-72.png)

   * また、次に示すように、南京錠アイコンはコンポーネントのダイアログにも表示されます。

   ![chlimage_1-73](assets/chlimage_1-73.png)

1. **継承された段落システム**

   設定ダイアログです。例えば、Geometrixx 内の「継承された段落システム」と同様です。

   ![chlimage_1-74](assets/chlimage_1-74.png)

## 注釈の追加 {#adding-annotations}

[注釈](/help/sites-classic-ui-authoring/classic-page-author-annotations.md)を使用すると、他の作成者がコンテンツに関するフィードバックを提供できます。注釈は、レビューや検証の目的でよく使用されます。

## ページのプレビュー {#previewing-pages}

ページのプレビューに重要な 2 つのアイコンがサイドキックの下部にあります。

![7 つのアイコンが横並びで表示されたサイドキックの下枠。行の先頭にある 2 つのアイコン（編集アイコンとプレビューモードアイコン）は、それぞれ鉛筆記号と虫眼鏡記号で示されます。](do-not-localize/chlimage_1-5.png)

* 鉛筆のアイコンは、現在のモードが編集モードであり、コンテンツを追加、変更、移動または削除できることを示します。

  ![鉛筆記号で示される編集アイコン。](do-not-localize/chlimage_1-6.png)

* 虫眼鏡アイコンを使用すると、プレビューモードを選択できます。プレビューモードでは、ページが公開環境と同じ形式で表示されます（ページの更新が必要になる場合もあります）。

  ![虫眼鏡記号で示されるプレビューモードアイコン。](do-not-localize/chlimage_1-7.png)

  プレビューモードでは、サイドキックが縮小されます。下向き矢印アイコンをクリックすると、編集モードに戻ります。

  ![AEM というタイトルと、タイトルの右側に下矢印記号で示された編集モードアイコンが表示されているバー。](do-not-localize/chlimage_1-8.png)

## 検索と置換 {#find-replace}

同じフレーズを大規模に編集する場合、「**[検索して置換](/help/sites-classic-ui-authoring/author-env-search.md#find-and-replace)**」メニューオプションを使用すると、web サイトのセクション内で文字列のインスタンスを複数検索して置換できます。

## ページのロック {#locking-a-page}

AEM では、他のユーザーによるコンテンツの変更を防ぐためにページをロックできます。ページのロックは、1 つの特定のページで大量の編集作業を行う場合や、短期間ページを凍結する必要がある場合に便利です。

>[!CAUTION]
>
>ページをロックしたユーザー（または管理者権限を持つアカウント）しかそのページをロック解除できないので、ページのロック機能は慎重に使用してください。

ページをロックするには：

1. 「**Web サイト**」タブで、ロックするページを選択します。
1. ページをダブルクリックして、編集用に開きます。
1. サイドキックの「**ページ**」タブで、「**ページをロック**」を選択します。

   ![screen_shot_2012-02-08at15750pm](assets/screen_shot_2012-02-08at15750pm.png)

   他のユーザーに対してページがロックされているというメッセージが表示されます。さらに、**Web サイト**&#x200B;コンソール右側のパネルに、AEM WCM はページをロック済みとして表示し、ページをロックしたユーザーが示されます。

   ![screen_shot_2012-02-08at20657pm](assets/screen_shot_2012-02-08at20657pm.png)

## ページのロック解除 {#unlocking-a-page}

ページのロックを解除するには：

1. 「**Web サイト**」タブで、ロックを解除するページを選択します。
1. ページをダブルクリックして開きます。
1. サイドキックの「**ページ**」タブで、「**ページのロックを解除**」を選択します。

## ページ編集の取り消しとやり直し {#undoing-and-redoing-page-edits}

ページのコンテンツフレームにフォーカスがあるときに、次のキーボードショートカットを使用します。

* 取り消し：Ctrl + Z（Windows）または Cmd + Z（Mac）
* やり直し：Ctrl + Y（Windows）または Cmd + Y（Mac）

1 つまたは複数の段落の削除、追加、再配置の取り消しまたはやり直しを実行すると、影響を受ける段落が点滅します（デフォルトの動作）。

>[!NOTE]
>
>ページ編集の取り消しとやり直しで実行できることについて詳しくは、[ページ編集の取り消しとやり直し - 理論](#undoing-and-redoing-page-edits-the-theory)を参照してください。

## ページ編集の取り消しとやり直し - 理論 {#undoing-and-redoing-page-edits-the-theory}

>[!NOTE]
>
>システム管理者は、インスタンスの要件に応じて、[取り消しとやり直し機能の様々な側面を設定](/help/sites-administering/config-undo.md)できます。

AEM では、ユーザーが実行するアクションの履歴と、それらのアクションを実行した順序が保存されます。そのため、複数のアクションの取り消しは、ユーザーが実行した順序で行われます。その後、やり直しを使用して、1 つ以上のアクションを再適用できます。

コンテンツページ上の要素が選択されている場合、取り消しおよびやり直しコマンドは、選択されている項目（テキストコンポーネントなど）に適用されます。

取り消しおよびやり直しコマンドの動作は、他のソフトウェアプログラムの動作と同様です。コンテンツに関する決定を行いながら、これらのコマンドを使用して web ページの直近の状態に戻すことができます。例えば、テキスト段落をページ上の別の場所に移動した場合に、取り消しコマンドを使用して、その段落を元の場所に戻すことができます。その後、段落を再度移動することに決めた場合は、やり直しコマンドを使用します。

>[!NOTE]
>
>以下の操作を実行できます。
>
>* 取り消しを使用してからページの編集を行っていない限り、アクションをやり直すことができます。
>* 最大 20 回の編集アクションを取り消すことができます（デフォルト設定）。
>* 様々な[キーボードショートカット](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md)を利用して取り消しとやり直しを行うこともできます。
>

取り消しおよびやり直しは、次のようなページの変更に対して使用できます。

* 段落の追加、編集、削除および移動
* 段落コンテンツのインプレース編集
* ページ内部での項目のコピー、カットおよび貼り付け
* ページ間での項目のコピー、カットおよび貼り付け
* ファイルおよび画像の追加、削除および変更
* 注釈およびスケッチの追加、削除および変更
* 基礎モードに対する変更
* 参照の追加と削除
* コンポーネントダイアログボックスでのプロパティ値の変更

フォームコンポーネントがレンダリングするフォームフィールドは、ページのオーサリング中に指定された値を持つことにはなりません。そのため、取り消しおよびやり直しコマンドは、それらのタイプのコンポーネントの値に対して行った変更には影響を与えません。例えば、ドロップダウンリスト内の値の選択を取り消すことはできません。

>[!NOTE]
>
>ファイルと画像に対する変更の取り消しとやり直しには、特別な権限が必要になります。また、ファイルと画像に対する変更の取り消し履歴は、少なくとも数時間保管されます。この時間を経過すると、変更の取り消しは保証されません。管理者は、権限を付与したり、デフォルトの 10 時間を変更したりすることができます。
