---
title: フォームをテンプレートとして保存
description: ここでは、繰り返し使うデータが入力されたフォームからテンプレートを作成する方法について説明します。
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 5e5ce783-8d0c-421c-b938-7020215682a0
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 100%

---

# フォームをテンプレートとして保存 {#save-forms-as-templates}

フォームに入力する際に、複数のフィールドへ繰り返し同じ値を入力しなければならない場面に遭遇することがあります。そのような場合は、同じ値が必要な複数のフィールドに適切な値を入力し、そのフォームまたはドラフトをテンプレートとして保存することができます。これにより、テンプレートのインスタンスを作成するたびに、指定のフィールドがテンプレートで指定した値で事前入力された状態になります。これは、フォームを入力する時間と手間を省くのに役立ちます。

次の手順を実行して、テンプレートを作成します。

1. フォームを開き、使用するたびに値がほぼ同一になるフィールドを選択するか入力します。フォームを入力する際に通常追加するテンプレートを使用して、添付ファイルを追加できます。
1. 「**テンプレートとして保存**」![save_as_template](assets/save_as_template.png) アイコンを選択します。テンプレートの名前を入力するためのダイアログボックスが表示されます。
1. テンプレートの名前を指定し、「**保存**」を選択します。テンプレートフォルダーにテンプレートが表示されます。

   同じ名前のテンプレートが既に存在する場合は、テンプレートの上書きを確認するダイアログボックスが表示されます。既存のテンプレートを新しいテンプレートで置き換えるには、「**続行**」を選択します。別の名前でテンプレートを保存するには、「**キャンセル**」を選択します。

これで、保存したテンプレートを開くことができます。テンプレートを開くたびに新しいフォームまたはタスクが作成され、フォームには保存されたデータとオプションが表示されます。テンプレートを使用して、事前入力データの編集、添付ファイルの追加、ドラフトとしての保存、タスクの送信またはこのテンプレートを使用した別のテンプレートの作成を行うことができます。テンプレートはモバイルデバイスのみに保存され、Adobe Experience Manager Forms サーバーとは同期されません。

不要になったテンプレートを削除することもできます。テンプレートを削除するには、テンプレートフォルダーに移動し、省略記号を選択して「**テンプレートを削除**」を選択します。

>[!NOTE]
>
>テンプレートはローカルで保存され、サーバーとは同期されません。アプリケーションのローカルデータを削除すると、テンプレートも削除されます。
