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
source-git-commit: 598d6eecbdd3887c41a36a14daa215e2e8e6e09a
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 34%

---

# Adobe Experience Manager（AEM） 6.5 LTS へのアップグレード {#upgrading-to-aem}

>[!NOTE]
>AEM 6.5 LTS へのアップグレードは、最新の 6 つのサービスパックからサポートされています。

このセクションでは、AEM インストールからAEM 6.5 LTS へのアップグレードについて説明します。

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

Foundation layer は、Apache Sling、Felix、Jackrabbit Oakの最新のオープンソースバンドルを組み込んで、Java 17 をサポートするようになりました。 さらに、AEM 6.5 LTS uber-jar のパッケージが変更されました。 さらに、AEM 6.5 LTS からは、従来の機能がいくつか削除されています。 詳細については、「[ リリース ノート ](/help/release-notes/release-notes.md#whats-new-what-s-new)」および [ アップグレード後にアンインストールされる廃止されたバンドルの一覧 ](/help/sites-deploying/obsolete-bundles.md) を参照してください。

AEM 6.5 LTS は、機能の後方互換性に重点を置いており、アナライザーツールが付属しています。 開始時の複雑性の評価 [ アップグレードの計画 ](/help/sites-deploying/pattern-detector.md) については、[AEM Analyzer を使用したアップグレードの複雑性の評価 ](/help/sites-deploying/upgrade-planning.md) を参照してください。
