---
title: Web ページでのページトラッカーと埋め込みコードの使用
description: ページトラッカーコードと埋め込み JavaScript コードを web サイトコードに組み込んで、Adobe Analytics でアセットの使用状況データを収集できるようにする方法について説明します。
contentOwner: AG
role: Architect, Admin
feature: Asset Reports
solution: Experience Manager, Experience Manager Assets
exl-id: bf8b2e51-60f8-423e-8ed6-167d71d6ec94
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 100%

---

# Web ページでのページトラッカーと埋め込みコードの使用 {#using-page-tracker-and-embed-code-in-web-pages}

ページトラッカーは、サードパーティの web サイトコードに組み込む JavaScript コードです。このコードを使用して、Adobe Analytics がそれらの web サイトでの [!DNL Adobe Experience Manager Assets] の使用状況データを取得できます。

アセット固有のイベント（クリック数など）を取得するには、サードパーティの web サイトコードに埋め込みコードも含めます。

次のサンプルコードは、ページトラッカーコードと埋め込みコードの両方を含む web ページです。

```html
<!DOCTYPE html>
<html>
    <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in milliseconds
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","xxxx","xxx","list1","eVar3","event8","event7");
            </script>

    </head>

    <body>

                                <img
            src="https://10.41.52.147:4502/xxxx/content/dam/test/abc.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
                <img
                    src="http://localhost/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
</html>
```

## ページトラッカーコードの追加 {#adding-page-tracker-code}

ページトラッカーコードは Web サイトコードのヘッダーセクションに追加します。次のコードスニペットは、サンプル web ページに組み込まれたページトラッカーコードです。

```xml
 <head>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/sitecatalyst/appmeasurement.js"></script>
            <script type="text/javascript" src="http://localhost:4502/xxxx/etc.clientlibs/dam/clientlibs/foundation/assetinsights/pagetracker.js"></script>
            <script type="text/javascript">
                                assetAnalytics.attrTrackable = 'trackable';
                assetAnalytics.defaultTrackable = false;
                assetAnalytics.attrAssetID = 'aem-asset-id';
                assetAnalytics.assetImpressionPollInterval = 200; // interval in millis
                assetAnalytics.charsLimitForGET = 2000; // bytes
                assetAnalytics.dispatcher.init("assetstesting","abc.net","bee","list1","eVar3","event8","event7");
            </script>

 </head>
```

## 埋め込みコードの追加 {#add-embed-code}

埋め込みコードは Web サイトコードの本文に追加します。次のコードスニペットは、サンプル Web ページに組み込まれた埋め込みコードです。

```xml
<body>

      <img
            src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
            data-aem-asset-id="aaid:a386f2cd78234becb66bd11575f9452d"
            data-trackable=true
            onload=assetAnalytics.core.assetLoaded(this)>

        <a
            href="https://www.adobe.com"

            onclick="assetAnalytics.core.assetClicked(this);return false">
           <img
                    src="http://localhost:4502/xxxx/content/dam/test/xyz.jpg"
                    data-aem-asset-id="aaid:7fa01fce0ebe40268cd6dcf07e2d9cb1"
                    data-trackable=true
                    onload=assetAnalytics.core.assetLoaded(this)>
        </a>

    </body>
```
