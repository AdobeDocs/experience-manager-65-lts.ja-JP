---
title: Adobe Experience Manager 6.5 LTS の最新のリリースノート
description: Adobe Experience Manager 6.5 LTS の最新のリリースノートです。
source-git-commit: baa7e84c30117645d6a2e4ef8d8e182a9dd73321
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 40%

---


# Adobe Experience Manager 6.5 LTS の最新のリリースノート {#release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] |
|---|---|
| バージョン | 6.5 LTS |
| 種類 | メジャーリリース |
| 一般公開日 | 2025年3月7日（PT） |

## 新機能 {#what-s-new}

[!DNL Adobe Experience Manager] 6.5 LTS は、[!DNL Adobe Experience Manager] 6.5 コードベースのアップグレードリリースです。 新機能と強化された機能、お客様向けの重要な修正、お客様向けの優先順位の高い機能強化、製品の安定性向上のための全般的なバグ修正が加えられています。また、[!DNL Adobe Experience Manager] 6.5 の SP22 までのサービスパックリリースも含まれています。

次のリストはその概要です。詳細については以降のページを参照してください。

### [!DNL Experience Manager Foundation] {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS のプラットフォームは、アップデートバージョンの OSGi ベースのフレームワーク（Apache Sling および Apache Felix）と Java™ コンテンツリポジトリの Apache Jackrabbit Oak 1.68.0 上に構築されています。

Quickstart は、サーブレットエンジンとして Eclipse Jetty 11.0.x を使用します。

#### Java™ サポート  {#java-support}

* Java™ 17 のサポート。
* 最適なパフォーマンスを得るには、デフォルトの GC 値を他の値に置き換えてください。詳しくは、[インストールとアップデート](/help/sites-deploying/custom-standalone-install.md)の節を参照してください。
* Java™ 17 メンテナンスアップデートがAdobeから公開されない場合は、AEM関連プロジェクトで使用するお客様向けにOracleが配布します。

#### Java™ の開発 {#java-development}

* [Uberjar の 2 つのバージョン ](/help/sites-developing/ht-projects-maven.md#experience-manager-api-dependencies)、廃止予定としてマークされていないパブリックインターフェイスを使用した推奨バージョン、廃止予定としてマークされているインターフェイスのみを含むバージョンがリリースされました。

#### アップグレード {#upgrade}

* アップグレードの手順について詳しくは、[ アップグレードドキュメント ](/help/sites-deploying/upgrade.md) を参照してください。

#### リポジトリ {#repository}

* Adobe Experience Manager 6.5 LTS の基盤は、アップデートバージョンの OSGi ベースのフレームワーク（Apache Sling および Apache Felix）と Java™ コンテンツリポジトリの Apache Jackrabbit Oak 1.68.0 上に構築されています。

## インストールとアップデート {#install-update}

設定要件について詳しくは、[インストール手順](/help/sites-deploying/custom-standalone-install.md)を参照してください。

手順について詳しくは、[アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。

## サポートされているプラットフォーム {#supported-platforms}

サポートしているプラットフォーム（サポートレベルを含む）の一覧については、[AEM 6.5 LTS の技術要件 ](/help/sites-deploying/technical-requirements.md) を参照してください。

>[!NOTE]
>
>AEM 6.5 LTS で使用するバージョンとしては、Java™ 17 をお勧めします。


## 廃止される機能および削除された機能 {#deprecated-and-removed-features}

アドビでは、製品の機能を絶えず評価して、常に後方互換性を慎重に考慮しながら、古い機能を作成し直したり、より近代的な機能に置き換えて、お客様にとっての全体的な価値を向上させています。

近い将来行われる Adobe Experience Manager（AEM）機能の削除や置換を通知するため、次のルールが適用されます。

1. 廃止の発表がまず行われます。廃止中は、機能はまだ使用可能ですが、それ以上の機能強化は行われません。
1. 廃止された機能の削除は、早ければ、次のメジャーリリースで行われます。実際の削除予定日は後日通知されます。

このプロセスにより、機能が実際に削除されるまでに、廃止される機能の新しいバージョンまたは後継機能にお客様が実装を合わせるためのリリースサイクルが少なくとも 1 回あります。

### 廃止される機能 {#deprecated-features}

ここでは、AEM 6.5 LTS で非推奨（廃止予定）となった機能の一覧を示します。 通常、将来のリリースで削除される予定の機能はまず廃止予定に設定され、代替手段が提供されます。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するように実装を変更するための計画を立てることをお勧めします。

| 領域 | 機能 | 代替手段 | バージョン（SP） |
|---|---|---|---|
| Sites | [SPA Editor](/help/sites-developing/spa-overview.md) | AEM でヘッドレスコンテンツの管理に推奨されるエディターは次のとおりです。<br>- ビジュアル編集用の[ユニバーサルエディター](/help/sites-developing/universal-editor/introduction.md)。<br>- フォームベース編集用の[コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-managing.md)。 | 6.5 LTS GA |

### 削除された機能 {#removed-features}

ここでは、AEM 6.5 LTS から削除された機能の一覧を示します。 以前のリリースでは、これらの機能は非推奨（廃止予定）とマークされていました。

| 領域 | 機能 | 代替手段 | バージョン（SP） |
|--- |--- |--- |--- |
| Commerce | AEM CIF Classic はサポートされていません。 | [AEM CIF](/help/commerce/cif/migration.md) に移行してください。 | 6.5 LTS GA |
| ソリューション | ソーシャル / コミュニティはサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| Screens | Screensはサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| アセット | バンドルがソーシャルに依存しているので、`dam-pim` と `dam-rating` はサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| アセット | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` は削除されました。 | 追加された別の api `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` を使用します。 | 6.5 LTS GA |
| Granite | バンドル `com.adobe.granite.socketio` は削除されました。 | 代替機能はありません。 | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer` はサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| グアバ | すべての guava の依存関係がAEMで削除され、`com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` バンドルがAEMに含まれなくなりました。 | guava に依存している場合は、顧客が自分で guava を追加できます。また、guava コードを java コレクションやその他の代替品に置き換えることもできます。 | 6.5 LTS GA |
| We.Retail | We-retail サンプルサイトはサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| オープンソース | バ `oak-solr-osgi` ドルはサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| オープンソース | `org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom` および `org.apache.sling.atom.taglib` はサポートされていません。 | 代替機能はありません。 | 6.5 LTS GA |
| オープンソース | `org.apache.commons.io packages` を `org.apache.commons.commons-io` から書き出すようになりました。 | 変更は不要です。 | 6.5 LTS GA |
| オープンソース | `javax.mail` パッケージを `com.sun.javax.mail` バンドルから書き出しています。 | 変更は不要です。 | 6.5 LTS GA |
| オープンソース | パッケ `org.apache.jackrabbit.api` ジが `org.apache.jackrabbit.oak-jackrabbit-api` バンドルから書き出されるようになりました。 | 変更は不要です。 | 6.5 LTS GA |

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/ja/docs/customer-one/using/home)。
