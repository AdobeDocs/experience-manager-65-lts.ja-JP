---
title: 管理コンソール実行時の考慮事項
description: このドキュメントでは、管理コンソール実行時のいくつかの考慮事項について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: bdd884c4-ae12-4827-8251-01033cbc0185
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 100%

---

# 管理コンソール実行時の考慮事項 {#considerations-when-running-administrationconsole}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

管理コンソールの実行時には、以下のことを考慮してください。

* URL `https://[hostname]:'port'/adminui`を指定して管理コンソールにアクセスする場合、指定するホスト名にアンダースコア文字を含めることはできません。アンダースコア文字を含めると、管理コンソールの一部の領域へのリンクが正しく機能しない場合があります。
* 日本語の OS 上の Windows エクスプローラーで管理コンソールを実行すると、次の問題が発生することがあります。

   * リンクをクリックすると、予期されるリンクではなく、ログインページに戻る。
   * リンクをクリックすると、権限エラーが表示される。

  ベストプラクティスとしては、リンクが失敗しないようにするために、Mozilla Firefox などの別のブラウザーから管理コンソールを実行してください。

* 管理コンソールで検索を実行するときは、バックスラッシュ文字（）を使用しないでください。
