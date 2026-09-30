---
title: プロセスデータの削除
description: 長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎて、結果的に AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。 プロセスデータを削除する方法を確認してください。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 53ce63a3-704a-4da6-b652-362a436f05a7
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
source-wordcount: '207'
ht-degree: 100%
---
# プロセスデータの削除 {#purging-process-data}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

長期間有効なプロセスの呼び出し時に生成されるプロセスデータが大きくなりすぎて、結果的に AEM Forms のパフォーマンスが低下し、不要なディスク領域が使用される可能性があります。 レコードが不要になったら、プロセスデータを削除することをお勧めします。 AEM Forms には、プロセスデータを削除するいくつかの方法が用意されています。

* 管理コンソールを使用して、長期間有効なプロセスに関連する古いレコードを一度に削除したり、定期的に自動で削除するようにスケジュールしたりできます （[ジョブマネージャーのデータベースからの古いレコードの削除](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)を参照）。
* AEM Forms の Java API および web サービス API を使用して、長期間有効なプロセスに関連するプロセスデータをプログラムで削除できます。 （[AEM Forms によるプログラミング](https://www.adobe.com/go/learn_aemforms_programming_63_jp)の「プロセスデータの削除」を参照）。
* プロセス名および他のパラメーターに基づいてプロセスを削除するには、プロセス削除ツールを使用します。 詳しくは、*[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt にあるプロセス削除ツールの ReadMe ファイルを参照してください。
