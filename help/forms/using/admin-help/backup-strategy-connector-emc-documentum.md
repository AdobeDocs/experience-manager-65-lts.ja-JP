---
title: Connector for EMC Documentum&reg; ユーザーのバックアップ戦略
description: Connector for EMC Documentum&reg; ユーザーのバックアップ戦略を作成する方法を確認します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
exl-id: 019e1a9b-c26c-429f-8153-fceeb85f7096
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
source-wordcount: '155'
ht-degree: 85%
---
# Connector for EMC Documentum® ユーザー向けのバックアップ方法 {#backup-strategy-for-connector-for-emc-documentum-users}

Connector for EMC Documentum® をインストールしている場合は、この章の手順に加えて、バックアップおよび回復方法に、ECM システムのインストールされたコンピューターのバックアップ（または回復）処理が含まれている必要があります （ECM Documentum® のドキュメントを参照）。

ECM リポジトリを使用して以下のタスクを実行し、AEM Forms 環境をバックアップします。

* このドキュメントで説明されている手順に従って、AEM Forms をバックアップします。
* [EMC Documentum® Content Server のバックアップ](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#back-up-the-emc-documentum-content-server)の手順に従って、ECM Documentum® システムをバックアップします。

ECM リポジトリを使用して以下のタスクを実行し、AEM Forms 環境を復元します。

* [EMC Documentum® Content Server の復元](/help/forms/using/admin-help/backing-recovering-emc-documentum-repository.md#restore-the-emc-documentum-content-server)の手順に従って、各 ECM システムを復元します。
* このドキュメントで説明されている手順に従って、AEM Forms を復元します。
