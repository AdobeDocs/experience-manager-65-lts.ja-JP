---
title: フォルダーのアセットとコレクションのレビュー
description: フォルダー内またはコレクション内のアセットに対してレビューワークフローを設定し、それをレビュー担当者またはクリエイティブパートナーと共有してフィードバックを得ることができます。
contentOwner: AG
feature: Collaboration, Collections
role: User
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 9d921487-89a7-4271-bdce-67ae539e5d85
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 100%

---

# フォルダーのアセットとコレクションのレビュー {#review-folder-assets-and-collections}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=ja) |
| AEM 6.5 | この記事 |

フォルダー内またはコレクション内のアセットに対してレビューワークフローを設定し、それをレビュー担当者またはクリエイティブパートナーと共有してフィードバックを得ることができます。

[!DNL Adobe Experience Manager Assets] では、フォルダー内またはコレクション内のアセットに対してアドホックレビューワークフローを設定し、レビュー担当者またはクリエイティブパートナーと共有してフィードバックを得ることができます。

レビューワークフローをプロジェクトと関連付けることも、独立したレビュータスクを作成することもできます。

ユーザーがアセットを共有した後で、レビュー担当者がアセットを承認または拒否できます。ワークフローの様々なステージで、様々なタスクの完了に関する通知が対象の受信者に送信されます。例えば、ユーザーがフォルダーまたはコレクションを共有すると、レビュー担当者は、フォルダーまたはコレクションがレビューのために共有されたという通知を受け取ります。

レビュー担当者がレビューを終了（アセットを承認または拒否）すると、ユーザーはレビューが完了したという通知を受け取ります。

## フォルダー用レビュータスクの作成 {#creating-a-review-task-for-folders}

1. [!DNL Assets] ユーザーインターフェイスで、レビュータスクを作成するフォルダーを選択します。
1. ツールバーの「**[!UICONTROL レビュータスクを作成]** ![レビュータスクを作成](assets/do-not-localize/create-review-task.png)」をクリックすると、**[!UICONTROL レビュータスク]**&#x200B;のページが表示されます。ツールバーにオプションが表示されていない場合は、「**[!UICONTROL その他]**」をクリックしてオプションを選択します。

1. （オプション）**[!UICONTROL プロジェクト]**&#x200B;リストから、レビュータスクを関連付けるプロジェクトを選択します。デフォルトでは、「**[!UICONTROL なし]**」オプションが選択されています。レビュータスクにプロジェクトを関連付けない場合は、この選択を保持します。

   >[!NOTE]
   >
   >エディターレベルの権限（またはそれ以上）のあるプロジェクトのみが「**[!UICONTROL プロジェクト]**」リストに表示されます。

1. レビュータスクの名前を入力し、「**[!UICONTROL 割り当て先]**」リストから承認者を選択します。

   >[!NOTE]
   >
   >選択されたプロジェクトのメンバーまたはグループが、承認者として「**[!UICONTROL 割り当て先]**」リストに表示されます。

1. レビュータスクの説明、タスクの優先順位および期限を入力します。

   ![task_details](assets/task_details.png)

1. 「詳細」タブで、URI の作成に使用されるラベルを入力します。

   ![review_name](assets/review_name.png)

1. 「**[!UICONTROL 送信]**」をクリックし、次に「**[!UICONTROL 完了]**」をクリックして確認メッセージを閉じます。新しいタスクに関する通知が承認者に送信されます。
1. 承認者として [!DNL Assets] にログインし、[!DNL Assets] の UI に移動します。アセットを承認するには、「**[!UICONTROL 通知]**」をクリックし、リストからレビュータスクを選択します。

   ![Assets の通知](assets/aemAssetsNotification.png)

1. **[!UICONTROL レビュータスク]**&#x200B;ページでレビュータスクの詳細を確認し、「**[!UICONTROL レビュー]**」をクリックします。
1. **[!UICONTROL レビュータスク]**&#x200B;ページでアセットを選択し、必要に応じて&#x200B;**[!UICONTROL 「承認」または「却下」]**&#x200B;をクリックして、承認または却下します。

   ![review_task](assets/review_task.png)

1. ツールバーの「**[!UICONTROL 完了]**」をクリックします。ダイアログでコメントを入力し、「**[!UICONTROL 完了]**」をクリックして確定します。
1. [!DNL Assets] ユーザーインターフェイスに移動し、フォルダーを開きます。カード表示とリスト表示に、アセットの承認状況アイコンが表示されます。

   **カードビュー**

   ![カードビューに表示されるレビューのステータス](assets/chlimage_1-404.png)

   **リスト表示**

   ![リスト表示に表示されるレビューのステータス](assets/review_status_listview.png)

## コレクション用レビュータスクの作成 {#creating-a-review-task-for-collections}

1. コレクションページで、レビュータスクを作成するコレクションを選択します。
1. ツールバーの「**[!UICONTROL レビュータスクを作成]** ![レビュータスクを作成](assets/do-not-localize/create-review-task.png)」をクリックすると、**[!UICONTROL レビュータスク]**&#x200B;のページが表示されます。ツールバーにオプションが表示されていない場合は、「**[!UICONTROL その他]**」をクリックしてオプションを選択します。

1. （オプション）**[!UICONTROL プロジェクト]**&#x200B;リストから、レビュータスクを関連付けるプロジェクトを選択します。デフォルトでは、「**[!UICONTROL なし]**」オプションが選択されています。レビュータスクにプロジェクトを関連付けない場合は、この選択を保持します。

   >[!NOTE]
   >
   >エディターレベルの権限（またはそれ以上）のあるプロジェクトのみが「**[!UICONTROL プロジェクト]**」リストに表示されます。

1. レビュータスクの名前を入力し、「**[!UICONTROL 割り当て先]**」リストから承認者を選択します。

   >[!NOTE]
   >
   >選択されたプロジェクトのメンバーまたはグループが、承認者として「**[!UICONTROL 割り当て先]**」リストに表示されます。

1. レビュータスクの説明、タスクの優先順位および期限を入力します。

   ![task_details-collection](assets/task_details-collection.png)

1. 「**[!UICONTROL 送信]**」をクリックし、次に「**[!UICONTROL 完了]**」をクリックして確認メッセージを閉じます。新しいタスクに関する通知が承認者に送信されます。
1. 承認者として [!DNL Assets] にログインし、[!DNL Assets] のコンソールに移動します。アセットを承認するには、「**[!UICONTROL 通知]**」をクリックし、リストからレビュータスクを選択します。
1. **[!UICONTROL レビュータスク]**&#x200B;ページでレビュータスクの詳細を確認し、「**[!UICONTROL レビュー]**」をクリックします。
1. コレクションのすべてのアセットがレビューページに表示されます。アセットを選択し、必要に応じて&#x200B;**[!UICONTROL 「承認」または「却下」]**&#x200B;をクリックして、アセットを承認または却下します。

   ![review_task_collection](assets/review_task_collection.png)

1. ツールバーの「**[!UICONTROL 完了]**」をクリックします。ダイアログでコメントを入力し、「**[!UICONTROL 完了]**」をクリックして確定します。
1. コレクションコンソールに移動して、コレクションを開きます。アセットの承認ステータスアイコンは、カード表示とリスト表示の両方に表示されます。

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *図：カードビュー*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *図：リスト表示*
