---
title: アカウントロックの設定
description: 「アカウントロックを有効にする」オプションを使用して、認証エラーが連続して指定の回数発生した後で、ユーザーアカウントをロックします。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: e78860dc-9375-465c-b1fa-2a4827ca8dce
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
source-wordcount: '210'
ht-degree: 100%
---
# アカウントロックの設定 {#configure-account-locking-settings}


>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

ドメインを追加する場合、アカウントロックを有効にするかどうかを指定します。 「アカウントロックを有効にする」オプションを選択すると、認証エラーが連続して指定の回数発生した後で、ユーザーアカウントがロックされます。 指定した時間が経過した後、ユーザーは認証をもう一度試行することができます。 この機能により、ユーザーが様々な秘密鍵証明書の組み合わせを使用してシステムにアクセスしようとすることを防ぎます。

ドメインの管理ページの設定を使用して、認証エラーの最大数およびアカウントがロックされている時間を指定できます。 これらの設定は、アカウントロックが有効になっているすべてのドメインに適用されます。

1. 管理コンソールで、**[!UICONTROL 設定／User Management／ドメインの管理]**&#x200B;をクリックします。
1. 「連続する認証エラーの最大回数」ボックスに、アカウントがロックされるまで連続して何回ログインの失敗が許可されるか、その回数を入力します。 デフォルト値は 20 です。
1. 「アカウントのロック解除までの時間（分）」ボックスに、ユーザーアカウントがロックされている時間（分）を入力します。 指定した時間（分）が経過すると、ユーザーはもう一度ログインを試行できます。 デフォルト値は 30 です。
1. 「**[!UICONTROL 保存]**」をクリックします。
