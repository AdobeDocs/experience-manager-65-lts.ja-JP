---
title: 互換性パッケージ
description: 互換性パッケージをAEM Forms 6.5 LTS にインストールすると、AEM Forms 6.5 以前のバージョンの Correspondence Management アセットと、非推奨のアダプティブフォームテンプレートおよびページが使用できるようになります
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 3a529a82-e2fd-423c-96c1-a5accc87775e
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 54%

---

# 互換性パッケージ{#compatibility-package}

## 概要 {#overview}

インタラクティブ通信は、AEM Forms 6.5 LTS でカスタマーコミュニケーションを構築するためのデフォルトの方法です。インタラクティブ通信の使用をお勧めします。 AEM Forms 6.5 LTS で引き続きレターを使用するには、最新の [AEMFD 互換性パッケージ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) をインストールする必要があります。

AEMFD 互換パッケージを使用すると [AEM Forms 6.5 LTS でAEM Forms 6.5.22.0、6.4、6.3、6.2 の次のアセットを使用 &#x200B;](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms) できます。

* ドキュメントフラグメント
* レター
* データディクショナリ
* アダプティブフォームの非推奨（廃止予定）になったテンプレートおよびページ

詳細については、[互換性パッケージをインストールすることにより AEM Forms 6.5 と互換性を持つようになったアセット](../../forms/using/compatibility-package.md#assetsmadecompatible)を参照してください。

## AEM Forms 6.5 LTS でAEM Forms 6.5、6.4、6.3 および 6.2 アセットのサポートを追加 {#add-support-for-aem-forms-and-assets-in-aem-forms-6.5.lts}

アップグレードを実行した後、AEMFD 互換性パッケージをインストールしてアセットに 6.5 との互換性を持たせるには、以下を実行します。

[AEM 互換性パッケージ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)が事前にインストールされていることを確認します。

1. 最新のAEM 6.5 LTS[&#x200B; 互換性パッケージ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases) をインストールします。

   パッケージのアップロードおよびインストールについて詳しくは、[パッケージの操作方法](/help/sites-administering/package-manager.md)を参照してください。

1. ログの状態が安定したら、サーバーを再起動します。
1. アセットに 6.5 LTS との互換性を持たせるには、移行ユーティリティを使用します。

   >[!NOTE]
   >
   > `Ctrl + C` コマンドを使用してSDKを再起動することをお勧めします。 Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

   詳しくは、[移行ユーティリティ](../../forms/using/migration-utility.md)を参照してください。

## 互換性パッケージをインストールすることによりAEM Forms 6.5 LTS と互換性を持つようになったAssets {#assetsmadecompatible}

互換性パッケージをインストールすると、次のアセットとテンプレートにAEM Forms 6.5 LTS との互換性を持たせることができます。

* AEM 6.4 以前の Correspondence Management アセット:

   * [レター](../../forms/using/create-letter.md)
   * [データディクショナリ](/help/forms/using/data-dictionary.md)
   * ドキュメントフラグメント

* アダプティブフォームの非推奨になったテンプレート:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* アダプティブフォームの非推奨になったページ

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment
