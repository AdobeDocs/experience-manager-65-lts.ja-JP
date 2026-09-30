---
title: Adobe コンテンツパッケージ Maven プラグイン
description: コンテンツパッケージ Maven プラグインを使用した AEM アプリケーションのデプロイについて説明します
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: 99cc79c0-3f31-4389-a21f-b58a70805b30
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
source-wordcount: '176'
ht-degree: 56%
---
# Adobe Content Package Maven plug-in {#adobe-content-package-maven-plugin}

パッケージデプロイメントおよび管理タスクを Maven プロジェクトに組み込むには、Adobe コンテンツパッケージ Maven プラグインを使用します。

Adobe Content Package Maven プラグインは、構築されたパッケージをAEMにデプロイし、AEM Package Managerで通常実行するタスクを自動化します。

>[!TIP]
>
>次の項目も参照してください。
>
>* AEM アプリケーションのデプロイ方法について詳しくは、AEM as a Cloud Service ドキュメントの [Adobe コンテンツパッケージ Maven プラグイン](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developer-tools/maven-plugin#developer-tools)に関する記事を参照してください。
>* 最新のAEM プロジェクトの構成方法については、AEM as a Cloud Service ドキュメントの[AEM プロジェクト構造](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure)記事を参照してください。
>* アーキタイプを使用して新しい AEM プロジェクトを開始する方法については、[AEM プロジェクトのアーキタイプ](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/developing/archetype/overview)のドキュメントを参照してください。
>
>3 つのドキュメントはすべて AEM 6.5 に適用されます。
