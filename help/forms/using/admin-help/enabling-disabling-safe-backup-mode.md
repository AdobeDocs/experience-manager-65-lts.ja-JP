---
title: セーフバックアップモードの有効化と無効化
description: バックアップ設定ページでは、AEM Forms をセーフバックアップモードで操作できるので、データベースとグローバルドキュメントストレージ（GDS）ディレクトリを確実にバックアップできます。セーフバックアップモードを有効化および無効化する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 34381caa-154e-479c-b475-7b3549909e9a
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 100%

---

# セーフバックアップモードの有効化と無効化 {#enabling-and-disabling-safe-backup-mode}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

バックアップ設定ページでは、AEM Forms をセーフバックアップモードで操作できるので、データベースとグローバルドキュメントストレージ（GDS）ディレクトリを確実にバックアップできます。

セーフバックアップモードになっている場合でも、AEM Forms は正常に稼動します。ただし、ファイルは GDS ディレクトリから削除されません。

>[!NOTE]
>
>このオプションを設定しても、システムのバックアップは実行されません。このオプションでは、バックアップを行うようにシステムが準備されます。

## セーフバックアップモードの有効化 {#enable-safe-backup-mode}

1. 管理コンソールで、設定／コアシステム設定／バックアップ設定をクリックします。
1. バックアップ設定ページで、「セーフバックアップモードで稼動する」を選択して「OK」をクリックします。

>[!NOTE]
>
>システムが既にセーフバックアップモードで稼動している場合は、「OK」をクリックしても新しい予約は作成されません。

## セーフバックアップモードの無効化 {#disable-safe-backup-mode}

1. 管理コンソールで、設定／コアシステム設定／バックアップ設定をクリックします。
1. バックアップ設定ページで、「セーフバックアップモードで稼動する」の選択を解除して「OK」をクリックします。
