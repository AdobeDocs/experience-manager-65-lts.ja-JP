---
title: Web ページに Dynamic Media ビデオ、画像ビューア、またはディメンショナルビューアを埋め込む
description: Web ページに Dynamic Media ビデオ、画像、または 3D 画像を埋め込む方法を説明します。
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Viewers
role: User, Admin
solution: Experience Manager, Experience Manager Assets
exl-id: b98729d3-111a-446b-915a-ca85b3cd75f0
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 100%

---

# Web ページに Dynamic Media ビデオ、画像ビューア、またはディメンショナルビューアを埋め込む {#embedding-the-video-or-image-viewer-on-a-web-page}

Web ページに埋め込んでビデオを再生したりアセットを表示したりする場合は、**[!UICONTROL 埋め込みコード]**&#x200B;機能を使用します。埋め込みコードをクリップボードにコピーして、Web ページに貼り付けることができます。**[!UICONTROL 埋め込みコード]**&#x200B;ダイアログボックスでは、コードの編集はできません。

Adobe Experience Manager を WCM として使用&#x200B;*していない*&#x200B;場合に限り、URL の埋め込みを実行します。Experience Manager を WCM として使用している場合は、[ページに直接アセットを追加します。](adding-dynamic-media-assets-to-pages.md)

[Web アプリケーションに URL をリンクする](linking-urls-to-yourwebapplication.md)を参照してください。

[レスポンシブサイトに最適化された画像の配信](responsive-site.md)を参照してください。

>[!NOTE]
>
>埋め込みコードは、選択したアセットを公開するまではコピーできません。また、ビューアプリセットまたは画像プリセットを公開する必要もあります。
>
>[アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。
>
>[ビューアプリセットを公開する](managing-viewer-presets.md#publishing-viewer-presets)を参照してください。
>
>[画像プリセットを公開する](managing-image-presets.md#publishing-image-presets)を参照してください。

**Web ページに Dynamic Media ビデオ、画像ビューア、またはディメンショナルビューアを埋め込む：**

1. 埋め込みコードをコピーする&#x200B;*公開済み*&#x200B;のビデオまたは画像アセットに移動します。

   埋め込みコードを使用するには、その&#x200B;*前に*&#x200B;アセットを&#x200B;*公開*&#x200B;しておく必要があります。また、ビューアプリセットまたは画像プリセットを公開する必要もあります。

   [アセットの公開](publishing-dynamicmedia-assets.md)を参照してください。

   [ビューアプリセットを公開する](managing-viewer-presets.md#publishing-viewer-presets)を参照してください。

   [画像プリセットを公開する](managing-image-presets.md#publishing-image-presets)を参照してください。

1. 左側のパネルでドロップダウンメニューを選択して、「**[!UICONTROL ビューア]**」を選択します。
1. 左側のレールで、ビューアプリセット名を選択します。ビューアプリセットがアセットに適用されます。
1. 「**[!UICONTROL 埋め込む]**」を選択します。
1. **[!UICONTROL 埋め込みコード]**&#x200B;ダイアログボックスで、コード全体をクリップボードにコピーしてから、「**[!UICONTROL 閉じる]**」を選択します。
1. 埋め込みコードを Web ページに貼り付けます。

## HTTP/2 を使用した Dynamic Media アセットの配信 {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 は、ブラウザーとサーバーの通信方法を改善する、新しく更新された web プロトコルです。情報の転送を高速化し、必要な処理能力を削減します。Dynamic Media アセットの配信は HTTP/2 を使用して行うことができ、応答時間と読み込み時間を短縮できます。

Dynamic Media アカウントでの HTTP/2 の使用方法について詳しくは、[コンテンツの HTTP/2 配信](http2.md)を参照してください。
