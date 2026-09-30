---
title: Acrobat Reader DC Extensions で使用するタイムアウト値の設定
description: Acrobat Reader DC Extensions で使用するタイムアウト値の設定方法について説明します。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: c2f96686-15e3-4d92-acfe-f971c5849de4
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 100%
---
# Acrobat Reader DC Extensions で使用するタイムアウト値の設定  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

Acrobat Reader DC Extensions で多数の PDF ファイルを処理している場合は、以下のタイムアウト値を適切に設定して、ジョブがタイムアウトして失敗するのを防ぎます。

**ドキュメント破棄タイムアウト：**

この値は管理コンソールで設定できます。 設定／コアシステム設定／設定をクリックし、デフォルトのドキュメント破棄タイムアウトの値を指定します。

**User Manager AEM Forms のタイムアウト：**&#x200B;この値を設定するには、config.xml ファイルを編集してください。 管理コンソールで、設定／ユーザー管理／設定／設定ファイルのインポートとエクスポートをクリックし、「エクスポート」をクリックします。 エクスポートされた config.xml ファイルを開き、次の行を編集します。

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

config.xml ファイルを保存し、再び管理コンソールに読み込みます。

**アプリケーションサーバーセッションタイムアウト：**&#x200B;この値は、アプリケーションサーバーで設定できます。 詳しくは、アプリケーションサーバーに付属するマニュアルを参照してください。
