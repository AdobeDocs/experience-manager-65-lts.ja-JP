---
title: Adobe Experience Manager 6.5 へのアップグレード
description: 古い Adobe Experience Manager（AEM）のインストールを AEM 6.5 にアップグレードするための基礎について説明します。
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: f66bb283e5c2a746821839269e112be8c2714ba7
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 29%

---

# Adobe Experience Manager（AEM） 6.5 LTS へのアップグレード {#upgrading-to-aem}

>[!NOTE]
>AEM 6.5 LTS へのアップグレードは、最新の 6 つのサービスパックからサポートされています。

この節では、AEM 6.5 への AEM インストール環境のアップグレードについて説明します。

<!-- Alexandru: drafting for now 

* [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md)
* [Assessing the Upgrade Complexity with Pattern Detector](/help/sites-deploying/pattern-detector.md)
* [Backward Compatibility in AEM 6.5](/help/sites-deploying/backward-compatibility.md)
  This was drafted before: * [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->

<!--
* [Upgrade Procedure](/help/sites-deploying/upgrade-procedure.md)
* [Upgrading Code and Customizations](/help/sites-deploying/upgrading-code-and-customizations.md)
* [Pre-Upgrade Maintenance Tasks](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [Performing an In-Place Upgrade](/help/sites-deploying/in-place-upgrade.md)
* [Post Upgrade Checks and Troubleshooting](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [Sustainable Upgrades](/help/sites-deploying/sustainable-upgrades.md)
* [Lazy Content Migration](/help/sites-deploying/lazy-content-migration.md)

-->

この手順に出てくる AEM インスタンスをわかりやすく区別するために、以下のように呼ぶことにします。

* アップグレード元の AEM インスタンスを「ソース」インスタンスと呼びます&#x200B;*。*
* アップグレード先のインスタンスを「ターゲット」インスタンスと呼びます&#x200B;*。*

## 変更点 {#what-has-changed}

### 更新 {#updates}

以下に、AEM の最近のいくつかのリリースでの注目すべき主な変更点を示します。

1. 基盤レイヤーは、Java 17 （Apache Sling、Apache Felix、Apache Jackrabbit Oakのバンドルのオープンソースレイヤーで構成）をサポートするようにアップグレードされました

1. AEM 6.5 LTS jar パッケージで Jarkarta サーブレット API 仕様 5 がサポートされるようになり、war パッケージを Jakarta サーブレット API 仕様 5/6 を実装するサーブレットコンテナにデプロイできるようになりました

1. AEM 6.5 LTS uber-jar のパッケージが変更されました。 詳しくは、[ コードとカスタマイズのアップグレード ](/help/sites-deploying/upgrading-code-and-customizations.md) を参照してください。

### 従来の機能/アーティファクトの削除 {#removed-legacy-features-artifacts}

次の従来のソリューションは、AEM 6.5 LTS から削除されました。 詳しくは、TBD：リリースノートへのリンクおよび [ アップグレード後にアンインストールされる廃止されたバンドルのリスト ](/help/sites-deploying/obsolete-bundles.md) を参照してください。

1. Social
1. Commerce
1. Screens
1. We-retail
1. Search と Promote の統合

**削除されたアーティファクト**

1. CRX-explorer
1. Crx2oak
1. Google guava （セキュリティの脆弱性により削除）
1. Abdera-parser （セキュリティの脆弱性により削除）
1. jdom （`org.apache.servicemix.bundles.jdom`） （セキュリティの脆弱性により削除されました）
1. `com.github.jknack.handlebars` （セキュリティの脆弱性により削除されました）

AEM 6.5 LTS は、機能の後方互換性に重点を置いており、アナライザーツールが付属しています。 アップグレードの計画を開始する際の複雑性の評価については、[AEM Analyzer を使用したアップグレードの複雑性の評価 ](/help/sites-deploying/pattern-detector.md) を参照してください。 その他の変更点について詳しくは、こちらの完全なリリースノートを参照してください。 未定：AEM 6.5 LTS のリリースノートへのリンク