---
title: 包括的な検索
description: 包括的な検索で、より迅速にコンテンツを見つけます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 4c6d1d6a-c000-48cf-9d86-306245a3c10c
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 100%

---

# 検索{#searching}

AEM のオーサー環境は、リソースタイプに応じて、コンテンツを検索するための様々なメカニズムを提供します。

>[!NOTE]
>
>オーサー環境外では、[Query Builder](/help/sites-developing/querybuilder-api.md) や [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) など、他の検索メカニズムも使用できます。

## 検索の基本 {#search-basics}

検索は上部のツールバーから使用できます。

![検索](do-not-localize/chlimage_1-17.png)

検索レールでは、次の操作を実行できます。

* 特定のキーワード、パスまたはタグを検索する。
* リソース固有の条件（変更日、ページのステータス、ファイルサイズなど）に基づいてフィルタリングする。
* 上記の条件に基づいて、[保存した検索条件](#saved-searches)を定義して使用する。

>[!NOTE]
>
>検索レールが表示されていれば、ホットキー `/`（スラッシュ）を使用して検索を呼び出すこともできます。

## 検索とフィルター {#search-and-filter}

リソースを検索およびフィルターするには、次のようにします。

1. （ツールバーの虫眼鏡アイコンを使用して）**検索**&#x200B;を開き、検索語を入力します。候補が表示され、その中から選択できます。

   ![s-01](assets/s-01.png)

   デフォルトでは、検索結果は現在の場所（コンソールと関連するリソースタイプ）に限定されます。

   ![screen_shot_2018-03-23at101445](assets/screen_shot_2018-03-23at101445.png)

1. 必要に応じて、場所フィルターを削除（削除するフィルターで「**X**」を選択）し、すべてのコンソール／リソースタイプを検索できます。
1. 検索結果は、コンソールや関連するリソースタイプに基づいてグループ化されて表示されます。

   特定のリソースを選択してアクションをさらに実行するか、必要なリソースタイプ（「**すべてのサイトを表示**」など）を選択してドリルダウンできます。

   ![screen-shot_2019-03-05at101900](assets/screen-shot_2019-03-05at101900.png)

1. さらにドリルダウンするには、レール記号（左上）を選択して&#x200B;**フィルターおよびオプション**&#x200B;のサイドパネルを開きます。

   ![フィルターおよびオプション](do-not-localize/screen_shot_2018-03-23at101542.png)

   検索には、リソースタイプに応じて、検索／フィルター条件の定義済みの選択項目が表示されます。

   サイドパネルでは、次の要素を選択できます。

   * 保存済みの検索結果
   * 検索ディレクトリ
   * タグ
   * 検索基準（更新日、公開ステータス、LiveCopy ステータスなど）。

   >[!NOTE]
   >
   >検索条件は、次の場合に変わる可能性があります。
   >
   >
   >
   >    * 選択したリソースタイプによって。例えば、アセットとコミュニティの条件はわかりやすく細分化されています。
   >    * [検索フォーム](/help/sites-administering/search-forms.md)としてのインスタンスは（AEM 内の場所に合わせて）カスタマイズできます。
   >
   >

   ![screen-shot_2019-03-05at102509](assets/screen-shot_2019-03-05at102509.png)

1. 検索用語を追加することもできます。

   ![screen-shot_2019-03-05at102613](assets/screen-shot_2019-03-05at102613.png)

1. **検索**&#x200B;を閉じるには **X**（右上）を使用します。

>[!NOTE]
>
>検索結果で項目を選択すると、検索条件が保持されます。
>
>検索結果ページの項目を選択する際に、ブラウザーの戻るボタンを使用した後で検索ページに戻ると、検索条件が保持されます。

## 保存済みの検索結果 {#saved-searches}

様々なファセットで検索するだけでなく、特定の検索設定を保存して、後で取得して使用することもできます。

1. 検索条件を定義して、「**保存**」を選択します。

   ![screen-shot_2019-03-05at102613-1](assets/screen-shot_2019-03-05at102613-1.png)

1. 名前を割り当ててから、「**保存**」を使用して確認します。

   ![screen-shot_2019-03-05at102725](assets/screen-shot_2019-03-05at102725.png)

1. 保存済みの検索は、次回検索パネルにアクセスするときにセレクターで選択できます。

   ![screen-shot_2019-03-05at102927](assets/screen-shot_2019-03-05at102927.png)

1. 保存すると、次の操作を実行できます。

   * （保存済みの検索結果の名前に対して）**x** を使用して、新しいクエリを開始する（保存済みの検索結果自体は削除されません）。
   * **保存済みの検索を編集**&#x200B;し、検索条件を変更して、もう一度&#x200B;**保存**&#x200B;する。

保存済みの検索結果を変更するには、保存済みの検索結果を選択して、検索パネルの下部にある「**保存済みの検索を編集**」をクリックします。

![screen-shot_2019-03-05at103010](assets/screen-shot_2019-03-05at103010.png)
