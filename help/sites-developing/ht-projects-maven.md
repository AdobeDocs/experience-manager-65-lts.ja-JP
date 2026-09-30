---
title: Apache Maven を使用して AEM プロジェクトをビルドする方法
description: このドキュメントでは、Apache Mavenに基づいてAEM プロジェクトを設定する方法について説明します。
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: ddc629ac-cf76-4608-9e9b-c8bd3e89da3c
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 46%
---
# Apache Mavenを使用したAEM プロジェクトの構築方法 {#how-to-build-aem-projects-using-apache-maven}

AEM 6.5は、パッケージ管理とプロジェクト構造に関する最新のベストプラクティスに従っています。 オンプレミスとAMSの両方の実装に、最新のAEM プロジェクトアーキタイプを使用します。

>[!TIP]
>
>詳しくは、次を参照してください。
>
>* 最新のAEM プロジェクトの構成方法については、AEM as a Cloud Service ドキュメントの[AEM プロジェクト構造](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure)記事を参照してください。
>* アーキタイプを使用して新しい AEM プロジェクトを開始する方法について詳しくは、[AEM プロジェクトのアーキタイプ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/developing/archetype/overview)に関するドキュメントを参照してください。
>* AEM アプリケーションのデプロイ方法について詳しくは、AEM as a Cloud Service ドキュメントの [Adobe コンテンツパッケージ Maven プラグイン](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developer-tools/maven-plugin#developer-tools)に関する記事を参照してください。
>
>3 つのドキュメントはすべて AEM 6.5 に適用されます。
