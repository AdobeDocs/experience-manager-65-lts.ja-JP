---
title: DB2&reg; データベース：毎週プロセスを実行
description: AEM Forms DB2® データベースのパフォーマンスを向上させる方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: e8cf9e73-345c-4dea-8361-b678c1a3cd1b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 95%

---

# DB2® データベース：週単位のプロセス実行{#db-database-running-a-process-weekly}

ご使用の AEM Forms DB2® データベースの動作が遅くなり始めたら、週単位で以下のプロセスを実行することで、パフォーマンスが向上します。

1. DB2® コントロールセンターを起動します。

   （Windows）スタート／すべてのプログラム／IBM® DB2®／General Administration Tools／Control Center を選択します。

   （Linux® および UNIX®）コマンドプロンプトから、`db2jcc` コマンドを入力します。

1. DB2® コントロールセンターのオブジェクトツリーで、「すべてのデータベース」をクリックします。
1. AEM Forms 用に作成したデータベースを選択して、表フォルダーをクリックします。
1. コンテンツパネル内のデータベーステーブルをすべて選択し、それらを右クリックして「実行統計」をクリックします。
1. Statistics／Index Statistics に移動します。
1. 「Collect Statistics For All Indexes」を選択し、「Collect Statistics For Indexes With Extended Detailed Statistics」を選択して、「OK」をクリックします。

プロセスが完了すると、メッセージが表示されます。メッセージを閉じます。
