---
title: Acrobat Reader DC Extensions で使用するタイムアウト値の設定
description: Acrobat Reader DC Extensions で使用するタイムアウト値の設定方法について説明します。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: eded255b54ff83f60f73cece8824c778d3a87680
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 100%

---

# Acrobat Reader DC Extensions で使用するタイムアウト値の設定  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Acrobat Reader DC Extensions で多数の PDF ファイルを処理している場合は、以下のタイムアウト値を適切に設定して、ジョブがタイムアウトして失敗するのを防ぎます。

**ドキュメント破棄タイムアウト：**

この値は管理コンソールで設定できます。設定／コアシステム設定／設定をクリックし、デフォルトのドキュメント破棄タイムアウトの値を指定します。

**User Manager AEM Forms のタイムアウト：**&#x200B;この値を設定するには、config.xml ファイルを編集してください。管理コンソールで、設定／ユーザー管理／設定／設定ファイルのインポートとエクスポートをクリックし、「エクスポート」をクリックします。エクスポートされた config.xml ファイルを開き、次の行を編集します。

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

config.xml ファイルを保存し、再び管理コンソールに読み込みます。

**アプリケーションサーバーセッションタイムアウト：**&#x200B;この値は、アプリケーションサーバーで設定できます。詳しくは、アプリケーションサーバーに付属するマニュアルを参照してください。
