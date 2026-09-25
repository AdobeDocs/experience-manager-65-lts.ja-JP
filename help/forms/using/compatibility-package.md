---
title: 互換性パッケージ
description: AEM Forms 6.5 LTSに互換性パッケージをインストールすると、AEM Forms 6.5以前のバージョンおよび非推奨のアダプティブフォームのテンプレートとページからCorrespondence Management アセットを使用できます
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 3a529a82-e2fd-423c-96c1-a5accc87775e
source-git-commit: 2e0cbe62754866d31de69547f9af1f2f63930f2c
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 59%
---
# 互換性パッケージ{#compatibility-package}

## 概要 {#overview}

インタラクティブ通信は、AEM Forms 6.5 LTSでお客様との通信を作成する際にデフォルトで推奨される方法です。 AEM Forms 6.5 LTSで引き続き文字を使用するには、最新の[AEMFD互換性パッケージ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)をインストールする必要があります。

AEMFD互換性パッケージでは、AEM Forms 6.5 LTS[&#128279;](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)でAEM Forms 6.5.22.0、6.4、6.3、6.2の次のアセットを使用することもできます

* ドキュメントフラグメント
* レター
* データディクショナリ
* アダプティブフォームの非推奨（廃止予定）になったテンプレートおよびページ

詳細については、[互換性パッケージをインストールすることにより AEM Forms 6.5 と互換性を持つようになったアセット](../../forms/using/compatibility-package.md#assetsmadecompatible)を参照してください。

## AEM Forms 6.5 LTSでのAEM Forms 6.5、6.4、6.3および6.2 アセットのサポートの追加 {#add-support-for-aem-forms-and-assets-in-aem-forms-6.5.lts}

アップグレードを実行した後、AEMFD 互換性パッケージをインストールしてアセットに 6.5 との互換性を持たせるには、以下を実行します。

[AEM 互換性パッケージ](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)が事前にインストールされていることを確認します。

1. 最新のAEM 6.5 LTS [互換性パッケージ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)をインストールします。

   パッケージのアップロードおよびインストールについて詳しくは、[パッケージの操作方法](/help/sites-administering/package-manager.md)を参照してください。

1. ログの状態が安定したら、サーバーを再起動します。
1. アセットを6.5 LTSと互換性を持たせるには、移行ユーティリティを使用します。

   >[!NOTE]
   >
   > SDKを再起動するには、`Ctrl + C` コマンドを使用することをお勧めします。 Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

   詳しくは、[移行ユーティリティ](../../forms/using/migration-utility.md)を参照してください。

## Assetsは、互換性パッケージをインストールすることで、AEM Forms 6.5 LTSと互換性を持つようになりました {#assetsmadecompatible}

互換性パッケージをインストールすることで、次のアセットとテンプレートをAEM Forms 6.5 LTSと互換性のあるものにすることができます。

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
