---
title: グラフィックレンダリング用のフォントの追加
description: AEM では、コンテンツから動的に取得したテキストを組み込んだグラフィックを生成できます
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 5ceaa9f0-aba1-40a3-97ef-f5ade0c2a54a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 100%

---

# グラフィックレンダリング用のフォントの追加{#adding-fonts-for-graphic-rendering}

AEM では、コンテンツから動的に取得したテキストを組み込んだグラフィックを生成できます

その際に、独自のフォントを読み込んで使用することもできます。

現時点で、Java プラットフォームのすべての実装で [TrueType](https://ja.wikipedia.org/wiki/TrueType) フォントがサポートされています。

1. CRXDE Lite を開き、次の場所にあるプロジェクトアプリケーションフォルダーに移動します。

   `/apps/<your-project>/`

1. `/apps/<your-project>/` の下に、新しいノードを作成します。

   * **名前**：`fonts`
   * **型**：`sling:Folder`

   すべての変更を保存します。

1. WebDAV などを使用して、フォントファイルをこのフォルダー内にコピーします。

   >[!NOTE]
   >
   >リポジトリ内のフォントファイルのサフィックスは、`*.ttf` または `*.TTF` である必要があります。

1. [Day Commons GFX Font Helper](/help/sites-deploying/osgi-configuration-settings.md) の [OSGi 設定](/help/sites-deploying/configuring-osgi.md)を更新します。フォントフォルダーへのパスを追加します（例：`/apps/<your-project>/fonts`）。

1. CRXDE Lite に戻ります。読み込んだフォントの名前を含むフォルダー内に、`.fontlist`ノードが表示されます。

   これらのフォントは、今後 Java API で使用できます。

Java API でのフォントの使用方法について詳しくは、[Java API の Font クラスに関するドキュメント](https://docs.oracle.com/javase/6/docs/api/java/awt/Font.html)を参照してください。
