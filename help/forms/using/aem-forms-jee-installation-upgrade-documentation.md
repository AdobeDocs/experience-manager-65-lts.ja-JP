---
title: JEE上のAEM Formsのインストールとアップグレードのワークフロー
description: JEE上のAEM Forms 6.5 LTS （JBoss）のインストールとアップグレードのワークフローと、関連するPDFとその目的の一覧。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE,AEM Forms Upgrade
exl-id: 67a96376-412e-4065-b7af-fbb720a4720a
source-git-commit: f015c4fb30bbba2ec0de7290d37ee56e182d2ddc
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 3%

---

# JEE上のAEM Formsのインストールとアップグレードのワークフロー {#aem-forms-jee-installation-upgrade-documentation}

## 適用先 {#applies-to}

このドキュメントは、**AEM 6.5 LTS Forms**&#x200B;に適用されます。

次のワークフローと表を使用して、シナリオに適したガイドを選択します。 一部の文書はPDFとして公開されます。追加の文書は、使用可能になると時間の経過とともに追加される場合があります。

## インストールとアップグレードのワークフロー {#installation-upgrade-workflow}

1. [JEE上のAEM Formsでサポートされているプラットフォーム ](/help/forms/using/aem-forms-jee-supported-platforms.md)を確認し、システムが必要なソフトウェアとハードウェアの組み合わせを満たしていることを確認します。
2. **新しいインストール**&#x200B;を実行するか、**アップグレード**&#x200B;を実行するかを決定します。
3. 選択したパスの場合は、以下の手順に従います（一部のシナリオでは、複数のガイドが必要です）。

## インストール前とアップグレード前の手順 {#start-here}

| ガイド | 説明 |
| --- | --- |
| [JEE上のAEM Formsでサポートされているプラットフォーム ](/help/forms/using/aem-forms-jee-supported-platforms.md) | JEE上のAEM Formsでサポートされているソフトウェアとハードウェアの組み合わせを一覧表示します。 インストールまたはアップグレードを開始する前に前提条件を検証する場合に使用します。 |
| [AEM Forms のアーキテクチャとデプロイメントトポロジ](/help/forms/using/aem-forms-architecture-deployment.md) | 推奨されるアーキテクチャとデプロイメントトポロジについて説明します。これにより、お使いの環境に合ったアプローチ（シングルサーバーとクラスターの比較など）を選択できます。 |
| [AEM Forms インストール用の永続性タイプの選択](/help/forms/using/choosing-persistence-type-for-aem-forms.md) | 開始する前に、インストール トポロジに適した永続性タイプを選択できます。 |

## JBossでJEEにAdobe Experience Manager Forms（AEM Forms）をインストールするにはどうすればよいですか？ {#installing-aem-forms-jee-jboss}

### ターンキー {#install-jee-jboss-turnkey}

| ガイド | 説明 |
| --- | --- |
| [JBoss ターンキー（PDF）を使用したJEEでのAEM Forms 6.5 LTSのインストールとデプロイ ](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-turnkey.pdf) | JBossでの&#x200B;**新規ターンキーインストール**&#x200B;に使用します。 このドキュメントでは、JBoss ターンキー配布を使用してJEE上にAEM Formsをインストールおよびデプロイする手順について説明します。 |

### シングルサーバー（ターンキーなし） {#install-jee-jboss-single-server}

| ガイド | 説明 |
| --- | --- |
| [AEM Forms （Single Server） （PDF）のインストールの準備中](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-install-single-server.pdf) | **before**&#x200B;を&#x200B;**フレッシュな単一サーバー（ターンキー以外）インストール**&#x200B;として使用します。 このドキュメントでは、シングルサーバートポロジにJEE上にAEM Formsをインストールするための前提条件と環境の準備手順について説明します。 |
| [JEE for JBossでのAEM Formsのインストールとデプロイ（PDF） ](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-jboss.pdf) | JBoss上のJEE上のAEM Formsの&#x200B;**ステップバイステップのインストールとデプロイメント**&#x200B;に使用します（**非ターンキー**）。 シングルサーバーインストールの場合は、このガイドに従ってください&#x200B;**after** completing *Preparing to Install AEM Forms （Single Server）*. |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **fresh cluster installation**. Describes prerequisites and environment preparation steps for installing AEM Forms on JEE in a server cluster topology. *(Link will be added once the PDF is available.)* |
| [Configuring AEM Forms on JEE on JBoss Cluster (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/cluster-jboss.pdf) | Use when setting up and configuring a **JBoss cluster topology** for AEM Forms on JEE. |
-->

## JBossでJEE上のAdobe Experience Manager Forms（AEM Forms）をアップグレードするにはどうすればよいですか？ {#upgrading-aem-forms-jee-jboss}

### ターンキー {#upgrade-jee-jboss-turnkey}

| ガイド | 説明 |
| --- | --- |
| [JBoss Turnkey （PDF）用JEE上のAEM Forms 6.5 LTSへのアップグレード ](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-turnkey.pdf) | **ターンキーアップグレードに使用**。 このドキュメントでは、JEE JBoss上の既存のAEM Formsのターンキーインストールをアップグレードする手順を説明します。 |

### 単一のサーバー {#upgrade-jee-jboss-single-server}

| ガイド | 説明 |
| --- | --- |
| [AEM Forms （PDF）のアップグレードの準備中](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-upgrade.pdf) | **before**&#x200B;を&#x200B;**単一サーバーのアップグレード**&#x200B;として使用します。 AEM 6.5 LTS Formsにアップグレードする前に、環境を準備する方法について説明します。 これは、シングルサーバーインストールモードでJEE上のAEM Formsを実行している環境に適用されます。 |
| [JBoss向けJEE上のAEM Forms（PDF）へのアップグレード ](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-jboss.pdf) | **単一サーバー**&#x200B;のインストールモードでJBossの&#x200B;**ステップバイステップのアップグレード手順**&#x200B;に使用します。 このガイドに従って、**が&#x200B;*AEM Formsのアップグレードの準備中*を完了した後に**&#x200B;実行します。 |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **cluster upgrade**. Describes how to prepare the environment for a server cluster before upgrading to AEM 6.5 LTS Forms. It applies to environments running AEM Forms on JEE in a server cluster installation mode. *(Link will be added once the PDF is available.)* |
| Upgrading to AEM Forms on JEE for JBoss (Cluster) (PDF) (**TBD**) | Use for the **step-by-step upgrade procedure** on JBoss in a **clustered** installation mode. Follow this guide **after** completing *Preparing to Install AEM Forms (Server Cluster)*. *(Link will be added once the PDF is available.)* |
-->
