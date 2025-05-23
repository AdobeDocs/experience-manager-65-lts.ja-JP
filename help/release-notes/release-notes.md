---
title: Adobe Experience Manager 6.5 LTS の最新のリリースノート
description: Adobe Experience Manager 6.5 LTS の最新のリリース情報について説明します。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: abba652bb5d7eb9b5f902ce99c07f2186e313173
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 30%

---

# Adobe Experience Manager 6.5 LTS の最新のリリースノート {#release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] |
|---|---|
| バージョン | 6.5 LTS |
| 種類 | メジャーリリース |
| 一般公開日 | 2025年3月7日（PT） |

## 新機能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS は、[!DNL Adobe Experience Manager] 6.5 コードベースのアップグレードリリースです。 お客様向けの主要な修正、お客様向けの優先順位の高い機能強化、製品の安定性向上のための全般的なバグ修正が含まれています。 また、[!DNL Adobe Experience Manager] 6.5 の SP22 までのサービスパックリリースも含まれています。

次のリストはその概要です。詳細については以降のページを参照してください。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS のプラットフォームは、アップデートバージョンの OSGi ベースのフレームワーク（Apache Sling および Apache Felix）と Java™ コンテンツリポジトリの Apache Jackrabbit Oak 1.68.x 上に構築されています。

Eclipse Jetty 11.0.x は、Quickstart のサーブレットエンジンとして使用されます。

#### Java™ サポート  {#java-support}

* Java™ 17 および Java™ 21 のサポート。
* 最適なパフォーマンスを得るには、デフォルトの GC 値を他の値に置き換えてください。 詳しくは、[インストールとアップデート](/help/sites-deploying/custom-standalone-install.md)の節を参照してください。
* Oracleから公開されていない場合、Adobeは、AEM関連プロジェクトでお客様が使用するための Java™ 17 および Java™ 21 メンテナンスアップデートを配布します。

#### Uberjar のパッケージ {#uber-jar-packaging}

* AEM 6.5 LTS の Uberjar パッケージには、わずかな違いがあります。 詳しくは、[AEM Uber Jar のバージョンの更新 ](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version) を参照してください。

#### アップグレード {#upgrade}

* アップグレードの手順について詳しくは、[ アップグレードドキュメント ](/help/sites-deploying/upgrade.md) を参照してください。

## インストールとアップデート {#install-update}

設定要件について詳しくは、[インストール手順](/help/sites-deploying/custom-standalone-install.md)を参照してください。

手順について詳しくは、[ アップグレードドキュメント ](/help/sites-deploying/upgrade.md) を参照してください。

## サポートされているプラットフォーム {#supported-platforms}

サポートしているプラットフォーム（サポートレベルを含む）の一覧については、[AEM 6.5 LTS の技術要件 ](/help/sites-deploying/technical-requirements.md) を参照してください。

>[!NOTE]
>
>AEM 6.5 LTS で使用するバージョンとしては、Java™ 17/Java™ 21 をお勧めします。

## 廃止される機能および削除された機能 {#deprecated-and-removed-features}

Adobeは、製品の機能を継続的にレビューし、古い機能を最新化する、または古い機能に取って代わることで、お客様にとっての価値を向上させます。 これらの変更は、後方互換性に慎重に注意して行われます。

近い将来行われる Adobe Experience Manager（AEM）機能の削除や置換を通知するため、次のルールが適用されます。

1. 廃止の発表がまず行われます。廃止中は、機能はまだ使用可能ですが、それ以上の機能強化は行われません。
1. 廃止された機能の削除は、早ければ、次のメジャーリリースで行われます。削除の実際の目標期日は、後で発表される予定です。

このプロセスにより、機能が実際に削除されるまでに、廃止される機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

### 廃止される機能 {#deprecated-features}

ここでは、AEM 6.5 LTS でAdobeが廃止された機能の一覧を示します。 通常、Adobeは、将来のリリースで削除される前に機能を非推奨（廃止予定）にし、代わりの機能を提供します。


現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するように実装を変更するための計画を立てることをお勧めします。

| 領域 | 機能 | 代替手段 | バージョン（SP） |
|---|---|---|---|
| Sites | [SPA Editor](/help/sites-developing/spa-overview.md) | AEM でヘッドレスコンテンツの管理に推奨されるエディターは次のとおりです。<br>- ビジュアル編集用の[ユニバーサルエディター](/help/sites-developing/universal-editor/introduction.md)。<br>- フォームベース編集用の[コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-managing.md)。 | 6.5 LTS GA |

### 削除された機能 {#removed-features}

ここでは、AEM 6.5 LTS から削除された機能の一覧を示します。 以前のリリースでは、これらの機能は非推奨（廃止予定）とマークされていました。

| 領域 | 機能 | 代替手段 | バージョン（SP） |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic はサポートされていません。 | [AEM CIF](/help/commerce/cif/migration.md) に移行します。 | 6.5 LTS GA |
| ソリューション | ソーシャル / コミュニティはサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| Screens | Screensはサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| Assets | バンドルがソーシャルに依存しているので、`dam-pim` と `dam-rating` はサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| Assets | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` は削除されました。 | 追加された別の api `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` を使用します。 | 6.5 LTS GA |
| ポータル | AEM Portal Director はサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| Granite | バンドル `com.adobe.granite.socketio` は削除されました。 | 代替機能はありません。 | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer` はサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| Granite | `crx2oak` はサポートされていません。 | 関連するバージョンの [oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) を選択します。 | 6.5 LTS GA |
| アドビ | `com.adobe.cq.cq-searchpromote-integration` はサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| グアバ | すべての guava の依存関係がAEMで削除され、`com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` バンドルがAEMに含まれなくなりました。 | guava に依存している場合は、顧客が自分で guava を追加できます。また、guava コードを java コレクションやその他の代替品に置き換えることもできます。 | 6.5 LTS GA |
| We.Retail | We-retail サンプルサイトはサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| オープンソース | バ `oak-solr-osgi` ドルはサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| オープンソース | `org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom` および `org.apache.sling.atom.taglib` はサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| オープンソース | `org.apache.commons.io` パッケージが `org.apache.commons.commons-io` から書き出されるようになりました。 | 変更は不要です。 | 6.5 LTS GA |
| オープンソース | `javax.mail` パッケージを `com.sun.javax.mail` バンドルから書き出しています。 | 変更は不要です。 | 6.5 LTS GA |
| オープンソース | パッケ `org.apache.jackrabbit.api` ジが `org.apache.jackrabbit.oak-jackrabbit-api` バンドルから書き出されるようになりました。 | 変更は不要です。 | 6.5 LTS GA |
| オープンソース | `com.github.jknack.handlebars` はサポートされていません。 | 関連する [ バージョン ](https://mvnrepository.com/artifact/com.github.jknack/handlebars) を選択 | 6.5 LTS GA |

## 既知の問題 {#known-issues}

### AEM 6.5.21-6.5.23 およびAEM 6.5 LTS GA の JSP スクリプティングバンドルの問題**

AEM 6.5.21、6.5.22、6.5.23、およびAEM 6.5 LTS GA には、既知の問題を含む `org.apache.sling.scripting.jsp:2.6.0` バンドルが付属しています。 この問題は、通常、AEM インスタンスが多数の同時リクエストを処理する際に高負荷で発生します。

この問題が発生すると、`org.apache.sling.scripting.jsp:2.6.0` への参照と共に、次の例外のいずれかがエラーログに表示される場合があります。

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

このエラーが発生した場合は、AEM インスタンスを再起動するしかありません。

Adobeのカスタマーサポートに連絡し、このリリースノートを参照して解決してください。

### SSL のみの機能を使用したDispatcher接続の失敗 {#ssl-only-feature}

AEMのデプロイメントで SSL のみの機能を有効にする場合、Dispatcher インスタンスとAEM インスタンス間の接続に影響を与える既知の問題があります。 この機能を有効にすると、ヘルスチェックが失敗し、Dispatcher インスタンスとAEM インスタンス間の通信が中断される可能性があります。

**影響：**

* HTTP 500 応答コードを含むヘルスチェックエラー
* Dispatcher インスタンスとAEM インスタンス間のトラフィックの破損
* コンテンツがDispatcherを通じて適切に提供されない

**影響を受ける環境：**

* Dispatcher設定を使用したAEM デプロイメント
* SSL のみの機能が有効になっているシステム

**解決策：**
この問題が発生した場合は、Adobe カスタマーサポートにお問い合わせください。 この問題を解決するためのホットフィックス [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.0.zip) が利用可能です。 必要なホットフィックスが適用されるまで、SSL のみの機能を有効にしないでください。

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/ja/docs/customer-one/using/home)。

