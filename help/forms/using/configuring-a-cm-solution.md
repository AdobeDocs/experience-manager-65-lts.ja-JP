---
title: Correspondence Management Solution の設定
description: AEM Forms 環境で Correspondence Management Solution を設定する方法について説明します。
topic-tags: correspondence-management
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: da668935-9d16-49e1-8e7a-772fc4040c1d
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 100%

---

# Correspondence Management Solution の設定 {#configuring-a-correspondence-management-solution}

## VersionRestoreManagerImpl のオーサーインスタンス URL の定義 {#defining-author-instance-url-for-versionrestoremanagerimpl}

オーサーインスタンスバージョンのリストアのオーサーインスタンス URL を定義するには、次の手順を実行します。

1. *https://:&lt;PublishHost>:&lt;PublishPort>/lc/system/console/configMgr* に移動します。OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. 「**[!UICONTROL com.adobe.livecycle.content.activate.impl.VersionRestoreManagerImpl.name]**」設定の横にある「**[!UICONTROL 編集]**」アイコンをクリックします。
1. 「**[!UICONTROL VersionRestoreManager Author URL]**」フィールドで、オーサーインスタンス VersionRestoreManager の URL を指定します。

   **URL 文字列**:

   `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.VersionRestoreManager`

   >[!NOTE]
   >
   >ロードバランサーの前に複数のオーサーインスタンス（クラスター化）がある場合は、「**[!UICONTROL VersionRestoreManager Author URL]**」フィールドにその URL を指定します。

1. 「**[!UICONTROL 保存]**」をクリックします。

## ActivationManagerImpl（パブリックインスタンス Activation Manager）のパブリッシュインスタンス URL の定義 {#defining-the-publish-instance-url-for-activationmanagerimpl-public-instance-activation-manager}

パブリックインスタンス Activation Manager のパブリッシュインスタンス URL を定義するには、次の手順を実行します。

1. *https://:&lt;authorHost>:&lt;authorPort>/lc/system/console/configMgr* に移動します。OSGi Management Console のユーザー資格情報を使ってログインします。デフォルトの資格情報は、admin/admin です。
1. **[!UICONTROL com.adobe.livecycle.content.activate.impl.ActivationManagerImpl.name]** 設定の横にある&#x200B;**[!UICONTROL 編集]**&#x200B;アイコンをクリックします。
1. 「**[!UICONTROL ActivationManager Publish URL]**」フィールドで、パブリッシュインスタンス Activation Manager にアクセスする URL を指定します。次の URL を指定できます。

   * **ロードバランサー URL（推奨）**：パブリッシュファーム（複数の非クラスターパブリッシュインスタンス）の前にロードバランサーとして機能する web サーバーを持っている場合は、そのロードバランサーの URL を指定します。
   * **パブリッシュインスタンス URL**：単一のパブリッシュインスタンスのみを持っている場合、あるいは何らかの制限によってパブリッシュファーム前段の web サーバーにオーサー環境からアクセスできない場合、任意のパブリッシュインスタンス URL を指定します。指定したパブリッシュインスタンスがダウンした場合は、フォールバックメカニズムが機能してオーサー側で処理します。
   * **URL 文字列**：

     `https://<hostname>:<port>:/libs/fd/fdm/content/crud/lc.content.remote.activate.activationManager`

1. 「**[!UICONTROL 保存]**」をクリックします。

Correspondence Management の設定方法について詳しくは、[Correspondence Management 設定プロパティ](https://helpx.adobe.com/jp/aem-forms/6-2/cm-configuration-properties.html)を参照してください。
