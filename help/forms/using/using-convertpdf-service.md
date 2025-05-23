---
title: ConvertPDF サービス
description: Adobe Experience Manager Forms の ConvertPDF サービスを使用して、PDF ドキュメントを PostScript ファイルや画像ファイルに変換します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
feature: Document Services,Assembler
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 1f6263f5-e4fb-44c2-a1d2-6046e9d69a48
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 100%

---

# ConvertPDF サービス {#convertpdf-service}

## 概要 {#overview}

Convert PDF サービスは、PDF ドキュメントを PostScript ファイルまたは画像ファイル（JPEG、JPEG 2000、PNG および TIFF）に変換します。PDFドキュメントを PostScript に変換すると、PostScript プリンターでサーバーベースの無人印刷を行う場合に便利です。PDF ドキュメントをサポートしていないコンテンツ管理システムでドキュメントをアーカイブする場合、PDF ドキュメントをマルチページ TIFF ファイルに変換する方法が実用的です。

Convert PDF サービスを使用すると、次のタスクを実行できます。

* PDF ドキュメントを PostScript に変換します。PostScript に変換する際に、この変換操作を使用して、変換元のドキュメントと、PostScript レベル 2 と 3 のどちらに変換するかを指定できます。PostScript ファイルに変換する PDF ドキュメントは、非インタラクティブである必要があります。
* PDF ドキュメントを JPEG、JPEG 2000、PNG および TIFF 画像形式に変換します。これらの画像形式のいずれかに変換する場合は、変換操作を使用して、ソースドキュメントおよび画像オプションの仕様を指定できます。画像オプションには、画像変換形式、画像の解像度、色変換などの様々な設定があります。

## サービスのプロパティの設定 {#properties}

AEM コンソールで **AEMFD ConvertPDF サービス**&#x200B;を使用すると、このサービスのプロパティを設定できます。AEM コンソールのデフォルト URL は `https://[host]:'port'/system/console/configMgr` です。

## サービスの使用 {#using-the-service}

ConvertPDF サービスには次の 2 つの API があります。

* **[toPS](https://helpx.adobe.com/jp/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toPS)**：PDF ドキュメントを PostScript ファイルに変換します。

* **[toImage](https://helpx.adobe.com/jp/experience-manager/6-3/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage)**：PDF ドキュメントを画像ファイルに変換します。サポートされている画像形式は、JPEG、JPEG2000、PNG および TIFF です。

### JSP またはサーブレットでの toPS API の使用 {#using-tops-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToPSOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.PSLevel,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to PostScript

 Document inputPDF = new Document(documentPath);

 // options object to pass to toPS API
 ToPSOptionsSpec toPSOptions = new ToPSOptionsSpec();

 // mandatory option to pass, sets PostScript language
 toPSOptions.setPsLevel(PSLevel.LEVEL_3);

 // invoke toPS method to convert inputPDF to PostScript
 Document convertedPS = cpdfService.toPS(inputPDF, toPSOptions);

 // save converted PostScript file to disk
 convertedPS.copyToFile(new File("C:/temp/out.ps"));

%>
```

### JSP またはサーブレットでの toImage API の使用 {#using-toimage-api-with-a-jsp-or-servlets}

```jsp
<%@ page import="java.util.List, java.io.File,

                com.adobe.fd.cpdf.api.ConvertPdfService,
                com.adobe.fd.cpdf.api.ToImageOptionsSpec,
                com.adobe.fd.cpdf.api.enumeration.ImageConvertFormat,

                com.adobe.aemfd.docmanager.Document" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to ConvertPdfService OSGi service.
 // Within an OSGi bundle @Reference annotation
 // can be used to retrieve service reference

 ConvertPdfService cpdfService = sling.getService(ConvertPdfService.class);

 // path to input document in AEM repository
 // replace this with path to your document
 String documentPath = "/content/dam/formsanddocuments/ExpenseClaimFlat.pdf";

 // Create a Docmanager Document object for
 // the flat PDF file which needs to be converted
 // to image

 Document inputPDF = new Document(documentPath);

 // options object to pass to toImage API
 ToImageOptionsSpec toImageOptions = new ToImageOptionsSpec();

 // mandatory option to pass, image format
 toImageOptions.setImageConvertFormat(ImageConvertFormat.JPEG);

 // invoke toImage method to convert inputPDF to Image
 List<Document> convertedImages = cpdfService.toImage(inputPDF, toImageOptions);

 // save converted image files to disk
 for(int i=0;i<convertedImages.size();i++){
     Document pageImage = convertedImages.get(i);
     pageImage.copyToFile(new File("C:/temp/out_"+(i+1)+".jpeg"));
 }

%>
```

### AEM ワークフローでの ConvertPDF サービスの使用 {#using-convertpdf-service-with-aem-workflows}

ワークフローから ConvertPDF サービスを実行する方法は、JSP またはサーブレットから実行する方法と似ています。

唯一の相違点は、JSP またはサーブレットからこのサービスを実行する場合、ドキュメントが ResourceResolverHelper オブジェクトから ResourceResolver オブジェクトのインスタンスを自動で取得する点です。この自動メカニズムは、コードがワークフローから呼び出される場合は機能しません。ワークフローの場合、ResourceResolver オブジェクトのインスタンスを Document クラスのコンストラクタに明示的に渡します。続いて、Document オブジェクトは
渡された ResourceResolver オブジェクトを使用してリポジトリからコンテンツを読み込みます。

以下に示したサンプルワークフロープロセスでは、入力したドキュメントを PostScript ドキュメントに変換します。コードは ECMAScript で記述され、ドキュメントはワークフローペイロードとして渡されます。

```javascript
/*
 * Imports
 */
var ConvertPdfService = Packages.com.adobe.fd.cpdf.api.ConvertPdfService;
var ToPSOptionsSpec = Packages.com.adobe.fd.cpdf.api.ToPSOptionsSpec;
var PSLevel = Packages.com.adobe.fd.cpdf.api.enumeration.PSLevel;
var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to ConvertPdfService
var cpdfService = sling.getService(ConvertPdfService);

/*
 * workflow payload and path to it
 */
var payload = graniteWorkItem.getWorkflowData().getPayload();
var payload_path = payload.toString();

/* Create resource resolver using current session
 * this resource resolver needs to be passed to Document
 * object constructor when file is to be read from
 * crx repository.
 */

/* get ResourceResolverFactory service reference , used
 * to construct resource resolver
 */
var resourceResolverFactory = sling.getService(ResourceResolverFactory);

var authInfo = {
    "user.jcr.session":graniteWorkflowSession.getSession()
};

var resourceResolver = resourceResolverFactory.getResourceResolver(authInfo);

// Create Document object from payload_path
var inputDocument = new Document(payload_path, resourceResolver);

// options object to be passed to toPS operation
var toPSOptions = new ToPSOptionsSpec();

// Set PostScript Language Three
toPSOptions.setPsLevel(PSLevel.LEVEL_3);

// invoke toPS operation to convert inputDocument to PS
var convertedPS = cpdfService.toPS(inputDocument, toPSOptions);

// save converted PostScript file to disk
convertedPS.copyToFile(new File("C:/temp/out.ps"));
```
