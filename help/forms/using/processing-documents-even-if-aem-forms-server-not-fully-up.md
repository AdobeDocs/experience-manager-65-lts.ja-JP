---
title: AEM Forms サーバーは、すべてのサービスが起動して実行される前でもドキュメントの処理を開始します。
description: AEM Forms サーバーは、JEE サーバーおよび OSGi サーバー上ですべてのサービスが起動して実行される前でも、ドキュメントの処理を開始します。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 22dd8daa-b8c6-4e7d-bca3-3958a79fb4b5
source-git-commit: 402b42d8ce5539739205a85d99bcb035d382a036
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# AEM Forms サーバーは、すべてのサービスが起動して実行される前でもドキュメントの処理を開始します。{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## 問題 {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

AEM Forms サーバーが完全に起動し、すべてのアプリケーションが起動して実行される前に、AEM Forms サーバーはドキュメントの処理を開始します。


## 適用先 {#applies-to}

このソリューションは、JEE サーバー上の AEM Forms と OSGi サーバー上の AEM Forms に適用されます。

## 解決策 {#solution}

この問題を解決するには、サーバーの起動時に引数 `Dcom.adobe.livecycle.dsc.deferServiceStart=true` を[バッチファイル](/help/sites-deploying/command-line-start-and-stop.md#windows-platform-start-bat-script-example)に追加します。
