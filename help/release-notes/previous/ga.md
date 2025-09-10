---
title: ' [!DNL Adobe Experience Manager]  6.5 LTS のリリースノート'
description: Adobe Experience Manager 6.5 LTS の最新のリリース情報について説明します。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: dfda31ac-765b-401d-98d0-c19f0de22aab
source-git-commit: eda8fc347ee8c68c1022495cbe8d48175c819be3
workflow-type: ht
source-wordcount: '1068'
ht-degree: 100%

---

# Adobe Experience Manager 6.5 LTS の最新リリースノート {#release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] |
|---|---|
| バージョン | 6.5 LTS |
| 種類 | メジャーリリース |
| 一般提供 | 2025年3月7日（PT） |

## 新機能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 は、[!DNL Adobe Experience Manager] 6.4 コードベースに対するアップグレードリリースです。お客様向けの重要な修正、お客様向けの優先順位の高い機能強化、製品の安定性向上のための全般的なバグ修正が加えられています。また、[!DNL Adobe Experience Manager] 6.5 の SP22 までのサービスパックリリースも含まれています。

次のリストはその概要です。詳細については以降のページを参照してください。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS のプラットフォームは、アップデートバージョンの OSGi ベースのフレームワーク（Apache Sling および Apache Felix）と Java™ コンテンツリポジトリの Apache Jackrabbit Oak 1.68.x 上に構築されています。

クイックスタートのサーブレットエンジンとして Eclipse Jetty 11.0.x が使用されます。

#### Java™ サポート  {#java-support}

* Java™ 17 および Java™ 21 のサポート。
* 最適なパフォーマンスを得るには、デフォルトの GC 値を他の値に置き換えてください。詳しくは、[インストールとアップデート](/help/sites-deploying/custom-standalone-install.md)の節を参照してください。
* アドビでは、Oracle から公開されていない場合、AEM 関連プロジェクトで顧客が使用できるように Java™ 17 および Java™ 21 のメンテナンスアップデートを配布します。

#### Uberjar パッケージ {#uber-jar-packaging}

* AEM 6.5 LTS の Uberjar パッケージには、わずかな違いがあります。詳しくは、[AEM Uber Jar バージョンの更新](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)を参照してください。

#### アップグレード {#upgrade}

* アップグレードの手順について詳しくは、 [アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。

## インストールとアップデート {#install-update}

設定要件について詳しくは、[インストール手順](/help/sites-deploying/custom-standalone-install.md)を参照してください。

手順について詳しくは、[アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。

>[!NOTE]
>
> AEM 6.5 LTS の新規インストールの場合、インデックス定義を個別にインストールする必要があります。 詳しくは、[このページ](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)を参照してください。

## サポートされているプラットフォーム {#supported-platforms}

サポートしているプラットフォーム（サポートレベルを含む）の完全な一覧表は、[AEM 6.5 LTS の技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

>[!NOTE]
>
>AEM 6.5 LTS で使用するバージョンとしては、Java™ 17／Java™ 21 をお勧めします。

## 廃止される機能および削除された機能 {#deprecated-and-removed-features}

アドビでは、古い機能を最新化または置き換えることで顧客価値を向上させるために、製品の機能を継続的にレビューしています。これらの変更は、後方互換性に細心の注意を払って行われます。

近い将来行われる Adobe Experience Manager（AEM）機能の削除や置換を通知するため、次のルールが適用されます。

1. 廃止の発表がまず行われます。廃止中は、機能はまだ使用可能ですが、それ以上の機能強化は行われません。
1. 廃止された機能の削除は、早ければ、次のメジャーリリースで行われます。実際の削除予定日は、後日発表される予定です。

このプロセスにより、機能が実際に削除されるまでに、廃止される機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

### 廃止される機能 {#deprecated-features}

この節では、AEM 6.5 LTS で廃止される機能の一覧を示します。通常、アドビでは今後のリリースで機能を削除する前に機能を非推奨（廃止予定）にし、代替手段を提供します。


現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するように実装を変更するための計画を立てることをお勧めします。

| 領域 | 機能 | 代替手段 | バージョン（SP） |
|---|---|---|---|
| Sites | [SPA Editor](/help/sites-developing/spa-overview.md) | AEM でヘッドレスコンテンツの管理に推奨されるエディターは次のとおりです。<br>- ビジュアル編集用の[ユニバーサルエディター](/help/sites-developing/universal-editor/introduction.md)。<br>- フォームベース編集用の[コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-managing.md)。 | 6.5 LTS GA |

### 削除された機能 {#removed-features}

この節では、AEM 6.5 LTS から削除された機能の一覧を示します。以前のリリースでは、これらの機能は非推奨（廃止予定）としてマークされていました。

| 領域 | 機能 | 代替手段 | バージョン（SP） |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic はサポートされていません。 | [AEM CIF](/help/commerce/cif/migration.md) に移行します。 | 6.5 LTS GA |
| ソリューション | ソーシャル／コミュニティはサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Screens | Screens はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Assets | バンドルはソーシャルに依存しているので、`dam-pim` と `dam-rating` はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Assets | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` は削除されました。 | 追加された代替 API `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` を使用します。 | 6.5 LTS GA |
| ポータル | AEM Portal Director はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Granite | バンドル `com.adobe.granite.socketio` は削除されました。 | 代替手段はありません。 | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer` はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Granite | `crx2oak` はサポートされていません。 | [Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) の関連バージョンを選択します | 6.5 LTS GA |
| Adobe | `com.adobe.cq.cq-searchpromote-integration` はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Guava | AEM では、すべての guava 依存関係が削除されたので、`com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` バンドルは AEM の一部ではなくなりました。 | 顧客は、guava に依存している場合は独自に guava を追加したり、可能であれば guava コードを java コレクションまたはその他の代替手段に置き換えたりすることができます。 | 6.5 LTS GA |
| `We.Retail` | `We-retail` サンプルサイトはサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| オープンソース | `oak-solr-osgi` バンドルはサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| オープンソース | `org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom`、`org.apache.sling.atom.taglib` はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| オープンソース | `org.apache.commons.io` パッケージが `org.apache.commons.commons-io` から書き出されるようになりました。 | 変更は必要ありません。 | 6.5 LTS GA |
| オープンソース | `javax.mail` パッケージが `com.sun.javax.mail` バンドルから書き出されています。 | 変更は必要ありません。 | 6.5 LTS GA |
| オープンソース | `org.apache.jackrabbit.api` パッケージが `org.apache.jackrabbit.oak-jackrabbit-api` バンドルから書き出されるようになりました。 | 変更は必要ありません。 | 6.5 LTS GA |
| オープンソース | `com.github.jknack.handlebars` はサポートされていません | 関連[バージョン](https://mvnrepository.com/artifact/com.github.jknack/handlebars)を選択します | 6.5 LTS GA |

## 既知の問題 {#known-issues}

### AEM 6.5.21～6.5.23 および AEM 6.5 LTS GA の JSP スクリプトバンドルの問題

AEM 6.5.21、6.5.22、6.5.23 および AEM 6.5 LTS GA には、既知の問題を含む `org.apache.sling.scripting.jsp:2.6.0` バンドルが付属しています。この問題は、通常、AEM インスタンスが多数の同時リクエストを処理する際の高負荷時に発生します。

この問題が発生すると、`org.apache.sling.scripting.jsp:2.6.0` への参照と共に、次の例外のいずれかがエラーログに表示される場合があります。

* `java.io.IOException: classFile.delete() failed`
* `java.io.IOException: tmpFile.renameTo(classFile) failed`
* `java.lang.ArrayIndexOutOfBoundsException: Index 0 out of bounds for length 0`
* `java.io.FileNotFoundException`

この問題を解決するためのホットフィックス [cq-6.5.lts.0-hotfix-NPR-42640](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-NPR-42640-1.2.zip) が使用可能です。

### SSL のみの機能を使用した Dispatcher 接続の失敗 {#ssl-only-feature}

AEM デプロイメントで SSL のみの機能を有効にすると、Dispatcher インスタンスと AEM インスタンス間の接続に影響を与える既知の問題があります。 この機能を有効にすると、ヘルスチェックが失敗し、Dispatcher インスタンスと AEM インスタンス間の通信が中断される場合があります。この問題は、お客様が `https + IP` 経由で Dispatcher から AEM インスタンスに接続しようとした場合に特に発生します。これは、SNI（Server Name Indication）検証の問題に関連しています。

**影響：**

* HTTP 400 応答コードを使用したヘルスチェックの失敗
* Dispatcher インスタンスとAEM インスタンス間のトラフィックの破損
* Dispatcher 経由でコンテンツを適切に配信できない
* Dispatcher 設定で IP アドレスを指定して HTTPS を使用した際の接続の失敗
* HTTPS + IP 経由で接続した際の HTTP 400「無効な SNI」エラー

**影響を受ける環境：**

* Dispatcher 設定を使用した AEM デプロイメント
* SSL のみの機能が有効になっているシステム
* AEM インスタンスへの `https + IP` 接続方法を使用した Dispatcher 設定

**解決策：**
この問題が発生した場合は、アドビカスタマーサポートにお問い合わせください。この問題を解決するためのホットフィックス [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) が使用可能です。必要なホットフィックスを適用するまで、SSL のみの機能を有効にしないでください。

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/ja/docs/customer-one/using/home)。
