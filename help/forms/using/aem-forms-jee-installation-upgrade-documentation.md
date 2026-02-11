---
title: JEE 上のAEM Formsのインストールおよびアップグレードワークフロー
description: AEM Forms 6.5 LTS on JEE （JBoss）のインストールおよびアップグレードワークフローと、関連する PDF とその目的の一覧。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: AEM Forms on JEE,AEM Forms Upgrade
exl-id: 6d8c0e24-7f08-4e66-bb12-2cf1cfe1d5d3
source-git-commit: fb9f6ef794da7f3b242e9e81a6c2505692c16cd8
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 3%

---


# JEE 上のAEM Formsのインストールおよびアップグレードワークフロー {#aem-forms-jee-installation-upgrade-documentation}

## 適用先 {#applies-to}

このドキュメントは、**AEM 6.5 LTS Forms** に適用されます。

次のワークフローと表を使用して、シナリオに合った正しいガイドを選択します。 一部のドキュメントは PDF として公開されます。ドキュメントは利用可能になるにつれて追加される場合があります。

## インストールとアップグレードのワークフロー {#installation-upgrade-workflow}

1. [JEE 上のAEM Formsでサポートされているプラットフォーム &#x200B;](/help/forms/using/aem-forms-jee-supported-platforms.md) を確認し、システムが必要なソフトウェアとハードウェアの組み合わせを満たしていることを確認します。
2. **新規インストール** と **アップグレード** のどちらを実行しているかを判断します。
3. 選択したパスについては、以下に説明する順序に従います（シナリオによっては、複数のガイドが必要な場合があります）。

## インストール前およびアップグレード前の手順 {#start-here}

| ガイド | 説明 |
| --- | --- |
| [JEE 上のAEM Formsでサポートされるプラットフォーム &#x200B;](/help/forms/using/aem-forms-jee-supported-platforms.md) | JEE 上のAEM Formsでサポートされるソフトウェアとハードウェアの組み合わせを示します。 インストールまたはアップグレードを開始する前に、前提条件を検証するために使用します。 |
| [AEM Forms のアーキテクチャとデプロイメントトポロジ](/help/forms/using/aem-forms-architecture-deployment.md) | 推奨されるアーキテクチャとデプロイメントトポロジについて説明し、環境に合ったアプローチ（例えば、単一サーバーとクラスター）を選択できるようにします。 |
| [AEM Forms インストールの永続性タイプの選択 &#x200B;](/help/forms/using/choosing-persistence-type-for-aem-forms.md) | 開始する前に、インストールトポロジに適した永続性タイプを選択するのに役立ちます。 |

## Adobe Experience Manager Forms（AEM Forms） on JEE を JBoss にインストールするにはどうすればよいですか？ {#installing-aem-forms-jee-jboss}

### ターンキー {#install-jee-jboss-turnkey}

| ガイド | 説明 |
| --- | --- |
| [JEE 上におけるAEM Forms 6.5 LTS のインストールおよびデプロイ（JBoss Turnkey （PDF）を使用） &#x200B;](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-turnkey.pdf) | JBoss での **新規の自動インストール** に使用します。 このドキュメントでは、JBoss 自動ディストリビューションを使用して、JEE 上にAEM Formsをインストールおよびデプロイする手順を説明します。 |

### シングルサーバー（自動インストールなし） {#install-jee-jboss-single-server}

| ガイド | 説明 |
| --- | --- |
| [AEM Formsのインストールの準備（シングルサーバー）（PDF） &#x200B;](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-install-single-server.pdf) | **新規のシングルサーバー（自動インストール以外）のインストール** の前 **&#x200B;**&#x200B;を使用します。 このドキュメントでは、シングルサーバートポロジで JEE 上のAEM Formsをインストールするための前提条件と環境の準備手順を示します。 |
| [JEE 上のAEM Formsのインストールおよびデプロイ（JBoss （PDF）版） &#x200B;](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/install-jboss.pdf) | を使用して、JBoss 上の JEE 上のAEM Formsの **インストールとデプロイメント** 手順を追って実行 **きます（自動インストールは行われません**）。 シングルサーバーのインストールの場合は、このガイド **後** の手順 *AEM Formsのインストールの準備（シングルサーバー）* に従ってください。 |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **fresh cluster installation**. Describes prerequisites and environment preparation steps for installing AEM Forms on JEE in a server cluster topology. *(Link will be added once the PDF is available.)* |
| [Configuring AEM Forms on JEE on JBoss Cluster (PDF)](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/cluster-jboss.pdf) | Use when setting up and configuring a **JBoss cluster topology** for AEM Forms on JEE. |
-->

## JBoss で JEE 上のAdobe Experience Manager Forms（AEM Forms）をアップグレードするにはどうすればよいですか？ {#upgrading-aem-forms-jee-jboss}

### ターンキー {#upgrade-jee-jboss-turnkey}

| ガイド | 説明 |
| --- | --- |
| [JEE 上のAEM Forms 6.5 LTS への自動アップグレード（JBoss 版）（PDF） &#x200B;](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-turnkey.pdf) | **自動アップグレード** にを使用します。 このドキュメントでは、JEE 上の既存のAEM Forms JBoss 自動インストールをアップグレードする手順を説明します。 |

### シングルサーバー {#upgrade-jee-jboss-single-server}

| ガイド | 説明 |
| --- | --- |
| [AEM Formsへのアップグレードの準備（PDF） &#x200B;](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/prepare-upgrade.pdf) | **前** の **シングルサーバーアップグレード** を使用します。 AEM 6.5 LTS Formsにアップグレードする前に環境を準備する方法について説明します。 これは、シングルサーバーインストールモードで JEE 上のAEM Formsを実行している環境に適用されます。 |
| [JEE 上のAEM Formsへのアップグレード（JBoss 版）（PDF） &#x200B;](https://helpx.adobe.com/content/dam/help/en/experience-manager/65LTS/forms/upgrade-jboss.pdf) | **シングルサーバー** インストールモードの JBoss での **ステップバイステップのアップグレード手順** に使用します。 このガイド **事後** に従って、*AEM Formsのアップグレードの準備* を完了します。 |

<!--
| Preparing to Install AEM Forms (Server Cluster) (PDF) (**TBD**) | Use **before** a **cluster upgrade**. Describes how to prepare the environment for a server cluster before upgrading to AEM 6.5 LTS Forms. It applies to environments running AEM Forms on JEE in a server cluster installation mode. *(Link will be added once the PDF is available.)* |
| Upgrading to AEM Forms on JEE for JBoss (Cluster) (PDF) (**TBD**) | Use for the **step-by-step upgrade procedure** on JBoss in a **clustered** installation mode. Follow this guide **after** completing *Preparing to Install AEM Forms (Server Cluster)*. *(Link will be added once the PDF is available.)* | -->

