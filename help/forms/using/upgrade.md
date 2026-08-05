---
title: AEM 6.5 LTS Formsへのアップグレード
description: AEM 6.3 FormsおよびAEM 6.4 FormsからAEM 6.5 LTS Formsへの直接アップグレードを実行できます。
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade
exl-id: 93126750-4645-4084-a21b-5362e3cc08a9
source-git-commit: b93457f543c22c893edd01259af19399e2548b72
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 24%

---

# AEM 6.5 Forms LTSへのアップグレード {#upgrade-to-aem-forms}

## 適用先 {#applies-to}

このドキュメントは、**AEM 6.5 LTS Forms**&#x200B;に適用されます。

AEM as a Cloud Serviceのドキュメントについては、[Cloud Service上のAEM Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=ja)を参照してください。


AEM 6.5 LTS Formsには、フォームと通信を使用した作成、管理、ユーザーエクスペリエンスを合理化する、いくつかの新機能と機能強化が含まれています。 AEM 6.5 LTSのすべての新機能と機能強化について詳しくは、[新機能の概要ドキュメント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-65-lts/content/release-notes/release-notes)を参照してください。

既存のLiveCycleまたはAEM Forms インストールをアップグレードすると、既存のデータ、プロセス、アセットを維持しながら、AEM 6.5 LTS Formsで提供される新しい機能と機能強化を取得できます。 アップグレード時には、メタデータとプロセスの状態も保持されます。 アップグレードを開始するためのアップグレードパスを選択できます。

### OSGi上のAEM Forms LTS

次の図は、OSGi上のAEM Forms LTSで使用可能なアップグレードパスを示しています。

![OSGi アップグレードフロー](/help/forms/using/assets/updated-img-forms-upgrade-lts.png)

次の場所から直接アップグレードを実行できます。

* AEM 6.5.17.0からAEM Forms 6.5 LTS
* AEM 6.5.18.0からAEM Forms 6.5 LTS
* AEM 6.5.19.0からAEM Forms 6.5 LTS
* AEM 6.5.20.0からAEM Forms 6.5 LTS
* AEM 6.5.21.0からAEM Forms 6.5 LTS
* AEM 6.5.22.0からAEM Forms 6.5 LTS
* AEM 6.5.23.0からAEM Forms 6.5 LTS

### JEE上のAEM Forms LTS

次の図は、JEE上のAEM Forms LTSで使用可能なアップグレードパスを示しています。

![JEE アップグレード 6.5](do-not-localize/jee-upgrade-6-5.svg)

次の場所から直接アップグレードを実行できます。

* JEE上のAEM 6.5.23.0 Forms

#### JEE上のAdobe Experience Manager Forms（AEM Forms）をアップグレードするにはどうすればよいですか？ {#how-do-i-upgrade-aem-forms-on-jee}

ステップバイステップ形式のアップグレード PDF （JBoss ターンキー、シングルサーバー、クラスター）については、[JEE上のAEM Formsのインストールとアップグレードのワークフロー](/help/forms/using/aem-forms-jee-installation-upgrade-documentation.md)を参照してください。


<!--
AEM 6.5.18.0 Forms on JEE provides two types of installers: [Full installer](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) and [Patch installer](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja).

**Full installer**: You can use the full installer to set up fresh AEM Forms instances or perform upgrades from AEM 6.5.x.x Forms on JEE to AEM 6.5.18.0 Forms on JEE.

**Patch installer**: Patch installer is for customers already using AEM 6.5.x.x versions. You can use the patch installer to upgrade to the latest version of AEM Forms.

The following image depicts senarios for using full and patch installer.

![Full Installer and Patch Installer](/help/forms/using/assets/full-and-patch-installer.png) 

Refer to the [AEM 6.5 Forms Service Pack installation instructions](https://experienceleague.adobe.com/docs/experience-manager-65-lts/release-notes/aem-forms-current-service-pack-installation-instructions.html) article to install the latest Service Pack for JEE environment.

-->

<!--

[Work in Progress]

Migration involves moving only assets (PDF, XDP, images, adaptive forms, correspondence management assets) from one server to another - processes (LCA), settings, configurations, and a few other pieces of metadata are not migrated. Perform the following steps to migrate to AEM 6.3 Forms:

1. Set up a fresh environment of [AEM 6.3 Forms](https://adobe.com/go/learn_aemforms_documentation_63_jp).
2. Move XDP or other compatible assets to the freshly set instance. For detailed instructions, see [Importing and exporting assets to AEM Forms](../../forms/using/import-export-forms-templates.md). [import templates](../../forms/using/import-export-forms-templates.md)
3. Build the required services, if any.

   For example, if you are using AEM Forms on JEE Document Services, changes are required in the code to use document services available in AEM Forms on OSGi.

4. Perform post-installation activities:

    * **Run Migration Utility**

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM Software Distribution. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.

      
      -->
