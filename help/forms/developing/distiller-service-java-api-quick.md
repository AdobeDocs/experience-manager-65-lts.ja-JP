---
title: Distiller サービス Java™ API クイックスタート（SOAP）
description: Distiller サービスで PostScript、EPS、PRN の各ファイルを PDF に変換する方法を説明します。この方法は、大量の印刷物から電子ドキュメントへの変換に一般的に採用されます。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
hide: true
hidefromtoc: true
exl-id: f38c6b8d-1870-4ff1-b08c-f65bd77bc5d0
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 100%

---

# Distiller サービス Java™ API クイックスタート（SOAP） {#distiller-service-java-api-quickstart-soap}

Distiller® サービスで Java™ API クイックスタート（SOAP）を使用できます。

[クイックスタート（SOAP モード）：Java を使用した PostScript ファイルの PDF ドキュメントへの変換](distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

AEM Forms の操作は、AEM Forms で厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

>[!NOTE]
>
>「AEM Forms によるプログラミング」にあるクイックスタートは、JBoss® Application Server と Microsoft® Windows オペレーティングシステムにデプロイされる Forms サーバーに基づいています。ただし、UNIX® などの別のオペレーティングシステムを使用している場合は、Windows 固有のパスを該当するオペレーティングシステムでサポートされているパスに置き換えます。同様に、別の J2EE アプリケーションサーバーを使用している場合は、有効な接続プロパティを必ず指定してください。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）。

## クイックスタート（SOAP モード）：Java™ API を使用した PostScript ファイルの PDF ドキュメントへの変換 {#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api}

次のコードの例では、*Loan.ps* という名前の PostScript ファイルを *Loan.pdf* という名前の PDF ファイルに変換します（[PostScript を PDF ドキュメントに変換する](/help/forms/developing/converting-postscript-pdf-documents.md#converting-postscript-to-pdf-documents)を参照してください）。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-distiller-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */

 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.distiller.client.DistillerServiceClient;

 public class JavaAPICreatePDFSoap {

     public static void main(String[] args)
     {
         try
         {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

         // Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);

         DistillerServiceClient disClient = new DistillerServiceClient(factory );

         // Get a PS file document to convert to a PDF document and populate a com.adobe.idp.Document object
         String inputFileName = "C:\\Adobe\Loan.ps";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);

         //Set run-time options
         String adobePDFSettings = "Standard";
          String securitySettings = "No Security";

          //Convert a PS  file into a PDF file
         CreatePDFResult result = new CreatePDFResult();
         result = disClient.createPDF(
                 inDoc,
                 inputFileName,
                      adobePDFSettings,
                 securitySettings,
                 null,
                 null
             );

          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();

          //Save the PDF file
         createdDocument.copyToFile(new File("C:\\Adobe\Loan.pdf"));
         }
         catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```
