---
title: ソリューション統合
description: Adobe Experience Manager（AEM）と他のアドビサービスやサードパーティのサービスとの統合ついて詳しく説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: ac7f2ea1-4e0c-44da-8d1d-d65c65d817cb
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 243139ec-8e41-5296-a287-31343ab1bc0f
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 81%
---
# ソリューション統合{#solutions-integration}

* [Adobe Experience Cloud との統合](/help/sites-administering/marketing-cloud.md)
* [サードパーティのサービスとの統合](/help/sites-administering/third-party-services.md)
* [Analytics と外部プロバイダー](/help/sites-administering/external-providers.md)
* [スマートタグの理解、適用、キュレーション](/help/assets/enhanced-smart-tags.md)

AEM と他のアドビサービスまたはサードパーティのサービスの統合については、次の情報を参照してください。

>[!NOTE]
>
>統合でカスタムプロキシ設定を使用している場合、AEM には 3.x API を使用する機能と 4.x API を使用する機能があるので、両方の HTTP クライアントプロキシを設定する必要があります。
>
>* 3.xは[http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)で設定されています
>* 4.xは[http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)で設定されています
>
