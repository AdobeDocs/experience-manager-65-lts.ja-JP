---
title: User Management
description: User Management では、SAML を使用して、AEM Forms モジュールと Netegrity SiteMinder で保護されたアプリケーションとの間で SSO を有効にできます。 このドキュメントでは、User Management について詳しく説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 5a87e340-053b-4b72-99a0-df14d7bf304c
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
source-wordcount: '493'
ht-degree: 100%
---
# User Management {#user-management}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

User Management では、Security Assertion Markup Language（SAML）を使用して、AEM Forms モジュールと Netegrity SiteMinder で保護されたアプリケーションとの間でシングルサインオン（SSO）を有効にできます。 SSO を実装すると、AEM Forms のユーザーログインページは不要になります。ユーザーが会社のポータルで既に認証されている場合は表示されません。

DB2 のデータベースおよびディレクトリ同期のパフォーマンスを向上させる方法については、[IBM DB2 データベース：定期保守のコマンドの実行](/help/forms/using/admin-help/ibm-db2-database-running-commands.md#ibm-db2-database-running-commands-for-regular-maintenance)を参照してください。

## SSL 対応の LDAP サーバーを対象とした User Management の設定 {#configuring-user-management-for-an-ssl-enabled-ldap-server}

SSL 対応の LDAP サーバーがある場合は、それと連携するように User Management を設定します （[SSL 対応の LDAP サーバーを対象とした User Management の設定](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server)を参照）。

## Document Security で使用するユーザー権限の設定 {#setting-user-privileges-for-use-with-document-security}

ユーザーおよびグループを作成するための適切な権限を持つ管理者ユーザーを作成します。 AEM Forms 環境に Document Security が含まれている場合は、招待ユーザーおよびローカルユーザーを管理する権限を、これらのユーザーの管理者となるユーザーに付与します。 また、管理コンソールのユーザーの役割を割り当てて、ユーザーに管理コンソールへのアクセス権を付与します （[役割の作成および設定](/help/forms/using/admin-help/creating-configuring-roles.md#creating-and-configuring-roles)を参照）。

選択したドメインのユーザーおよびグループを、ポリシーユーザーの検索中に表示するには、上級管理者またはポリシーセット管理者が、作成したポリシーセットごとに表示されるユーザーとグループのリストに対して、ドメイン（User Management で作成）を選択して追加する必要があります。

表示されるユーザーとグループのリストは、ポリシーセットコーディネーターに対して表示され、ポリシーに追加するユーザーまたはグループを選択する際にエンドユーザーが参照できるドメインを制限するために使用されます。 このタスクを実行しない場合、ポリシーセットコーディネーターに対して、ポリシーに追加するユーザーまたはグループが表示されません。 ポリシーセットコーディネーターは、特定のポリシーセットに複数存在する可能性があります。

>[!NOTE]
>
>ポリシーを作成するには、ドメインの作成を済ませておく必要があります。

### 表示されるユーザーおよびグループを設定 {#set-visible-users-and-groups}

AEM Forms 環境と Document Security をインストールして設定した後に、User Management で適切なドメインをすべて設定します。

1. 管理コンソールで、サービス／Document Security／ポリシーをクリックし、「ポリシーセット」タブをクリックします。
1. 「グローバルポリシーセット」を選択し、「表示されるユーザーとグループ」タブをクリックします。
1. 「ドメインを追加」をクリックし、必要に応じて既存のドメインを追加します。
1. サービス／Document Security／設定／マイポリシーに移動し、「表示されるユーザーとグループ」タブをクリックします。
1. 「ドメインを追加」をクリックし、必要に応じて既存のドメインを追加します。

## 管理者ユーザーの制限 {#administrator-user-restrictions}

特定の種類の管理者権限を持つユーザーは、セキュリティ上の理由から、Workspace のエンドユーザー web ページにアクセスできません。 これらの web ページはファイアウォールの外部に存在することがあるので、管理レベルのタスクを許可するとセキュリティ上のリスクが生じる可能性があります。 のエンドユーザー Web ページにアクセスできるのは、Workspace 管理者または Workspace ユーザーの権限を持つユーザーだけです。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。
