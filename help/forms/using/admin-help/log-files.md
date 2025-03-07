---
title: ログファイル
description: 実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録され、そのログファイルは任意のテキストエディターで開くことができます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ff4dce07-725e-4750-9e95-4261b50580bd
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 100%

---

# ログファイル {#log-files}

実行時や起動時のエラーなどのイベントは、アプリケーションサーバーのログファイルに記録されます。アプリケーションサーバーへのデプロイ中に問題が発生した場合には、ログファイルを参照して問題を見つけることができます。ログファイルは、テキストエディターを使用して開くことができます。

（JBoss）次のログファイルは `[appserver root]/server/'server'/log` ディレクトリにあります。

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

（WebLogic）ドメインログファイルは `[appserverdomain]` ディレクトリにあり、サーバーログファイルは `[appserverdomain]/servers/[appserver name]/logs` ディレクトリにあります。

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

（WebSphere）次のログファイルは `[appserver root]/profiles/default/logs/[appserver name]` ディレクトリにあります。

* SystemErr.log
* SystemOut.log
* StartServer.log
