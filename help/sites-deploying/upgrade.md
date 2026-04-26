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
exl-id: ebc34847-dc3d-41ed-b0d6-f004c3debcd9
source-git-commit: f015c4fb30bbba2ec0de7290d37ee56e182d2ddc
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 27%

---

# Adobe Experience Manager（AEM） 6.5 LTSへのアップグレード {#upgrading-to-aem}

>[!NOTE]
>AEM 6.5 LTSへのアップグレードは、サポートされているすべての6.5 サービスパックで利用できます。

>[!NOTE]
>
>技術的な観点から、AEM 6.5 LTSからAEM 6.5 LTS サービスパックへのアップグレードプロセスは、[のシームレスなインプレースアップグレード ](/help/sites-deploying/in-place-upgrade.md)となるように設計されています。 このプロセスでは、通常、リリースノートに明記されていない限り、顧客からのコードの変更は必要ありません。

この節では、AEM インストールをAEM 6.5 LTSにアップグレードする方法について説明します。

<!--
Alexandru: drafting for now 

* [Planning Your Upgrade](/help/sites-deploying/upgrade-planning.md)
* [Assessing the Upgrade Complexity with Pattern Detector](/help/sites-deploying/pattern-detector.md)
* [Backward Compatibility in AEM 6.5](/help/sites-deploying/backward-compatibility.md)
-->

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

基盤レイヤーでJava 17とJava 21がサポートされるようになり、Apache Sling、Felix、Jackrabbit Oakの最新のオープンソースバンドルが組み込まれています。 さらに、AEM 6.5 LTS uber-jarのパッケージが変更されました。 さらに、AEM 6.5 LTSから一部のレガシー機能が削除されました。 詳しくは、[ リリースノート ](/help/release-notes/release-notes.md#whats-new-what-s-new)および[ アップグレード後にアンインストールされた古いバンドルの一覧](/help/sites-deploying/obsolete-bundles.md)を参照してください

AEM 6.5 LTSは、機能の下位互換性に重点を置いており、アナライザーツールが付属しています。 アップグレードの計画[を開始する際の複雑性の評価については、[AEM Analyzerを使用したアップグレードの複雑性の評価](/help/sites-deploying/aem-analyzer.md)を参照してください](/help/sites-deploying/upgrade-planning.md)。
