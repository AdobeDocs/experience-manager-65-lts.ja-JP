---
title: 不在設定の指定
description: 不在機能を使用して、ユーザーが不在となり、AEM Forms によって割り当てられるタスクを実行できない日時を指定できます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: bf4fa6e4-25c7-46a8-9bae-4af7bfc14426
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 100%

---

# 不在設定の指定 {#configuring-out-of-office-settings}

ユーザーまたは管理者は不在機能を使用して、ユーザーが不在となり、AEM Forms によって割り当てられるタスクを実行できない日時を指定できます。あるユーザーが「不在」に設定されている場合、そのユーザーのタスクは 1 人以上の指定されたユーザーに割り当てられます。ユーザーは Workspace で「不在」設定を変更できます。ユーザーの代わりに、管理者が Forms ワークフローで設定を変更することもできます。

Workbench ユーザーは、プロセスの作成時に、不在設定が有効な場合にタスクをリダイレクトするかどうかを指定できます。

## ユーザーの不在情報の表示 {#view-a-user-s-out-of-office-information}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

1. 管理コンソールで、サービス／Forms ワークフロー／不在をクリックします。
1. 不在ページの上部付近にあるボックスで、次のいずれかを実行できます。

   **名前で検索**

   「名前で検索」オプションを選択します。ユーザーの名前またはその一部を入力して、「検索」をクリックします。このフィールドに何も入力しないで検索すると、Forms ワークフローによって全ユーザーのリストが返されます。

   **日付範囲で検索**

   「日付範囲で検索」オプションを選択します。検索結果を絞り込むために、開始日および終了日や、目的のタイムスタンプを指定します。「検索」をクリックします。

1. ユーザー名をクリックすると、そのユーザーの不在情報がユーザーリストの下に表示されます。

## ユーザーの不在ステータスを変更する {#change-a-user-s-out-of-office-status}

1. 「[ユーザーの不在情報の表示](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)」の説明に従って、ユーザーを検索します。
1. 変更するユーザーの名前をクリックします。
1. 「*ユーザー名*」の「現在の状態」リストから、「在席中」または「不在」のいずれかを選択します。
1. 「保存」をクリックします。

## ユーザー不在の日付範囲を追加する {#add-an-out-of-office-date-range-for-a-user}

1. 「[ユーザーの不在情報の表示](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)」の説明に従って、ユーザーを検索します。
1. 変更するユーザーの名前をクリックします。
1. 「日付範囲を追加」をクリックします。
1. 「開始時刻」と「終了時刻」に入力します。カレンダーアイコンをクリックすると、日付を選択することができます。終了時刻を指定しない場合、ユーザーは無期限に不在であると設定されます。
1. 「保存」をクリックします。

## 不在時のタスクにユーザーを割り当てる {#assign-a-user-for-out-of-office-tasks}

ユーザーが不在の間に、不在のユーザーに代わって新規タスクを実行する 1 人以上のユーザーを割り当てることができます。以下の設定を行うことができます。

* すべての新しいタスクを指定されたデフォルトユーザーに割り当てます。
* タスクを再割り当てしません。新しいタスクは不在のユーザーに割り当てられたままになります。
* ユーザーのタスクの大半を受け取るデフォルトユーザーを割り当てるが、特定のプロセスからのタスクを他のユーザーに再割り当てするか、不在のユーザーに割り当てられたままにするよう指定します。
* デフォルトユーザーは割り当てないが、特定のプロセスからの特定のタスクを特定のユーザーに割り当てます。

   1. 「[ユーザーの不在情報の表示](configuring-out-office-settings.md#view-a-user-s-out-of-office-information)」の説明に従って、ユーザーを検索します。
   1. 変更するユーザーの名前をクリックします。
   1. 「不在時のタスクのデフォルトユーザー」リストで、リストからユーザーを選択します。デフォルトユーザーが再割り当てされた項目を受け取らないようにする場合は、「割り当てません」を選択します。

      適切なユーザー名がリストに表示されない場合は、「ユーザーの検索」をクリックし、ユーザーの検索ダイアログボックスを使用してユーザーを検索します。リストから適切なユーザーを選択して、「ユーザーを選択」をクリックします。ユーザーの検索ダイアログボックスで「ユーザーのスケジュールを表示」をクリックして、選択したユーザーの不在スケジュールを確認することもできます。

   1. デフォルトユーザーに送信してはいけないプロセスがある場合は、「例外を追加」をクリックしてプロセスを選択し、リストから別のユーザーを選択します。「割り当てません」を選択して、タスクを不在のユーザーに割り当てたままにしておくこともできます。
   1. 「保存」をクリックします。
