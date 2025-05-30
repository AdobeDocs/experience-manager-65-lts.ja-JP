---
title: エンドポイントの追加、有効化、変更または削除
description: エンドポイントの追加、有効化、変更または削除方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 14264788-a05a-4a8d-b485-33ae1caac094
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 100%

---

# エンドポイントの追加、有効化、変更または削除 {#adding-enabling-modifying-or-removing-endpoints}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

## エンドポイントのサービスへの追加 {#add-an-endpoint-to-a-service}

エンドポイントは、サービスのみに追加できます。エンドポイントは単独では存在できず、サービスに関連付ける必要があります。

>[!NOTE]
>
>エンドポイントを追加するときは、一意の名前を使用することをお勧めします。

1. 管理コンソールで、サービス／アプリケーションおよびサービス／サービスの管理をクリックします。
1. サービスの管理ページで、設定するサービスをクリックします。
1. 「エンドポイント」タブにあるリストで、追加するエンドポイントの種類を選択し、「追加」をクリックします。
1. エンドポイントの種類に応じて、その他のエンドポイント設定を指定します。

[監視フォルダーエンドポイントの設定](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[メールエンドポイントの設定](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[タスクマネージャーエンドポイントの設定](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[リモートエンドポイントの設定](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. 「追加」をクリックします。

## エンドポイントの有効化または無効化 {#enable-or-disable-an-endpoint}

デフォルトで、新しいエンドポイントは自動的に有効になります。ただし、エンドポイントを手動で無効にした場合は、有効にしない限りエンドポイントは動作しません。

サービスに関する問題が発生している場合は、関連するエンドポイントを無効にすると、問題をトラブルシューティングしやすくなります。また、システムの定期保守やサービスのアップグレードを行うときも、エンドポイントを無効にする必要があります。

1. 管理コンソールで、サービス／アプリケーションおよびサービス／エンドポイントの管理をクリックします。
1. エンドポイントの管理ページで、有効または無効にするエンドポイントのチェックボックスをオンにして、「有効にする」または「無効にする」をクリックします。

## エンドポイントの変更 {#modify-an-endpoint}

>[!NOTE]
>
>管理コンソールを使用してエンドポイント設定に加えた変更は、アプリケーションのデザイン時コピーには反映されません。アプリケーションを再デプロイすると、管理コンソールを使用してそのエンドポイントに加えた変更はすべて失われます。

1. 管理コンソールで、サービス／アプリケーションおよびサービス／エンドポイントの管理をクリックします。
1. エンドポイントの管理ページで、変更するエンドポイントをクリックします。
1. エンドポイントの更新ページで、エンドポイントの名前、説明および設定を変更します。

   >[!NOTE]
   >
   >名前や説明には「&lt;」を含めないでください。含めると、Workspace に表示される名前や説明の一部が削除されます。

1. 変更を保存するには、「更新」をクリックします。

このタスクは、サービスの管理ページから、サービスを選択して「エンドポイント」タブをクリックすることで実行することもできます。

## エンドポイントの削除 {#remove-an-endpoint}

1. 管理コンソールで、サービス／アプリケーションおよびサービス／エンドポイントの管理をクリックします。
1. エンドポイントの管理ページで、削除するエンドポイントのチェックボックスをオンにして、「削除」をクリックします。エンドポイントが表示されなくなります。
