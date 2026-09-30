---
title: ブランディングのための組織ロゴの変更
description: AEM Forms Workspace をブランド化するには、デフォルトのロゴをカスタマイズして組織のロゴを提供します。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 3aa4aca3-3c94-4936-ba9c-484bbb196256
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
source-wordcount: '116'
ht-degree: 100%
---
# ブランディングのための組織ロゴの変更 {#changing-the-organization-logo-for-branding}

組織のロゴは、AEM Forms Workspace の左上隅に表示されます。 ロゴを更新するには、[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md#generic-steps-for-html-workspace-customization)に従い、次の手順を実行します。

1. ロゴを作成してファイルに `NewWorkspace.png` と名前を付けます。 WebDAV クライアントを使用して、/apps/ws/images フォルダーに画像ファイルを配置します。

   >[!NOTE]
   >
   >ロゴ画像の推奨サイズは 218 ピクセル × 20 ピクセル です。

   >[!NOTE]
   >
   >詳しくは、[WebDAV アクセス](/help/sites-administering/webdav-access.md)を参照してください。

1. 次のスタイルを追加することによって、/apps/ws/css/newStyle.css にあるスタイルシートの新しいロゴ画像を参照します。

   ```css
   #logo {
   
          background: url(../images/NewWorkspace.png) no-repeat 14px 11px;
   
   }
   ```
