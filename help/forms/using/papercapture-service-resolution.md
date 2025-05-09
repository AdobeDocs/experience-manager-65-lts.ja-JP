---
title: PaperCapture サービスが PDF に対して OCR（光学式文字認識）操作を実行できない場合の問題を解決するトラブルシューティング記事。
description: PaperCapture サービスが PDF に対して OCR（光学式文字認識）操作を実行できない問題を解決する手順について説明します。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: de3cd0ad-0b18-4d9a-8c6b-72cc16149cfc
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 100%

---

# PaperCapture サービスが PDF に対して OCR を実行できない

## 問題

AEM Forms サービスパック 6.5.21.0 へのアップグレード後、`PaperCapture` サービスが、PDF に対して OCR（光学文字認識）処理を実行できない。このサービスでは、PDF やログファイルの形式で出力を生成しません。

## 適用先

このソリューションは次の場合に適用されます。
* すべての（JBoss、WebLogic、WebSphere）JEE サーバー上の AEM Forms
* OSGi サーバー上の AEM Forms

## 解決策

1. ソフトウェア配布ポータルから[ホットフィックス](https://nam04.safelinks.protection.outlook.com/?url=https%3A%2F%2Fexperience.adobe.com%2F%23%2Fdownloads%2Fcontent%2Fsoftware-distribution%2Fen%2Faem.html%3Fpackage%3D%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq650%2Fhotfix%2FPaperCaptureSvc.zip&amp;data=05%7C02%7Cruchitas%40adobe.com%7Cf50f80aab6994875271a08dc91f2f137%7Cfa7b1b5a7b34438794aed2c178decee1%7C0%7C0%7C638545719814675925%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C0%7C%7C%7C&amp;sdata=9pTrMfiMD%2B5kQezxsZwTdOmaaktxURR99d7f6wHr%2FWQ%3D&amp;reserved=0)をダウンロードします。
1. ダウンロードしたフォルダーのコンテンツを抽出してコピーします。
1. 対応するアプリケーションサーバーの以下のパスに移動します。
   * **JBoss**：
     `..\Adobe\Adobe_Experience_Manager_Forms\jboss\standalone\svcnative\PaperCaptureSvc`
   * **WebLogic**：
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **WebSphere**：\
     `..\Adobe\Adobe_Experience_Manager_Forms\crx-repository\bedrock\svcnative\PaperCaptureSvc`
   * **OSGi の設定**：\
     `..\quickstart\crx-quickstart\bedrock\svcnative\PaperCaptureSvc`
1. AEM アプリケーションサーバーを停止します。
1. `PaperCaptureSvc` フォルダーの既存のコンテンツをコピーしたコンテンツに置き換えます。
1. AEM アプリケーションサーバーを再起動します。

   >[!NOTE]
   >
   > 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。
