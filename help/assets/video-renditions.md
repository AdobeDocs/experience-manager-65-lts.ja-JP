---
title: ビデオレンディション
description: Adobe Experience Manager Assets を使用して、様々な形式（OGG、FLV など）のビデオアセット用のビデオレンディションを生成する方法について説明します。
contentOwner: rbrough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
solution: Experience Manager, Experience Manager Assets
feature: Video
role: User
exl-id: da33f43b-7375-46f1-a80f-c1891fd90312
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 100%

---

# ビデオレンディション {#video-renditions}

Adobe Experience Manager Assets では、様々な形式（OGG、FLV など）のビデオアセット用のビデオレンディションが生成されます。

Experience Manager Assets では、メディアアセットの静的レンディションと動的レンディション（DM エンコードされたレンディション）がサポートされています。

静的レンディションは、FFMPEG（システムパスにインストールされ、使用できるもの）を使用してネイティブに生成され、コンテンツリポジトリに保存されます。

DM エンコードされたレンディションは、プロキシサーバーに保存され、実行時に提供されます。

Experience Manager Assets では、クライアントサイドでこのようなレンディションの再生がサポートされています。

特定のビデオアセットのレンディションを表示するには、アセットのページを開いて、グローバルナビゲーションアイコンを選択します。次に、リストから「**[!UICONTROL レンディション]**」を選択します。

![chlimage_1-478](assets/chlimage_1-478.png)

ビデオレンディションのリストは、**[!UICONTROL レンディション]**&#x200B;パネルに表示されます。

![chlimage_1-479](assets/chlimage_1-479.png)

DM エンコードされたレンディションのプロキシサーバーを設定するには、[Dynamic Media クラウドサービスを設定します](config-dynamic.md)。

目的のパラメーターでビデオレンディションを生成するには、[対応するビデオプロファイルを作成](video-profiles.md)します。

プロキシサーバーを設定し、ビデオプロファイルを作成したら、このビデオプリセットを処理プロファイルに追加して、その処理プロファイルをフォルダーに適用することができます。

>[!NOTE]
>
>Microsoft® Internet Explorer 11 では、OGG および WAV ファイルのオーディオは再生できません。拡張子が OGG または WAV のアセットの詳細ページに、エラー `Invalid Source` が表示されます。
>
>MS® Edge および iPad では、OGG ファイルは再生されず、サポートされていない形式というエラーが発生します。
