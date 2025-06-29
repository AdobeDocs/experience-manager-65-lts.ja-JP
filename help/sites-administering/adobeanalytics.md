---
title: Adobe Analytics との統合
description: Adobe Experience Manager（AEM）と Adobe Analytics を統合する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: 4f7e1794-af5a-45a2-8dc6-80029c47caeb
source-git-commit: 929a2175449a371ecf81226fedb98a0c5c6d7166
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 100%

---

# Adobe Analytics との統合{#integrating-with-adobe-analytics}

Adobe Analytics と AEM の統合により、web ページのアクティビティを追跡できます。

* Adobe Analytics 設定により、AEM で Adobe Analytics を認証できます。
* Adobe Analytics レポートスイートに送信されたデータはフレームワークで特定されます。

データには、次のようなページおよびユーザーデータが含まれます。

* AEM コンポーネントで収集されるデータ
* リンククリック数
* ビデオ使用量情報
* Adobe Analytics から訪問されるページの数

統合の設定に役立つ情報は、次のページにあります。

* [Adobe Analytics への接続とフレームワークの作成](/help/sites-administering/adobeanalytics-connect.md)
* [Adobe Analytics のリンクトラッキングの設定](/help/sites-administering/adobeanalytics-link.md)
* [コンポーネントデータと Adobe Analytics プロパティとのマッピング](/help/sites-administering/adobeanalytics-mapping.md)
* [Adobe Analytics のビデオトラッキングの設定](/help/sites-administering/adobeanalytics-video.md)
* [Adobe Classifications](/help/sites-administering/adobeanalytics-classifications.md)

また、[オプトインウィザード](/help/sites-administering/opt-in.md)を使用して簡単に統合を実行できます。

>[!NOTE]
>
>方法については、[DTM を使用した AEM と Adobe Target および Adobe Analytics の統合](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html?lang=ja)も参照してください。

## その他の情報 {#further-information}

次のページを参照してください。

* ユーザーデータを収集するコンポーネントの開発と Adobe Analytics フレームワークのカスタマイズに関する情報については、[Adobe Analytics 統合の拡張](/help/sites-developing/extending-analytics.md)を参照してください。

>[!NOTE]
>
>Adobe Analytics をカスタムプロキシ設定で使用している場合、（例えば、Web コンソールで）**Apache HTTP Client** プロキシ設定に必要な [2 つの OSGi バンドルを設定](/help/sites-deploying/configuring-osgi.md)する必要があります。AEM の一部の機能では 3.x API を使用し、他の機能では 4.x API を使用するので、両方とも必要です。設定：
>
>* **Day Commons HTTP Client 3.1**（3.x API を設定）。
>  >  例：[https://localhost:4502/system/console/configMgr/com.day.commons.httpclient](https://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>
>* **Apache HTTP コンポーネントプロキシ設定**（4.x API を設定）。
>  >  例：[https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](https://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>
