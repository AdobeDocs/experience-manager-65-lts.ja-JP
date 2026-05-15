---
title: よくある質問（FAQ）
description: AEM 6.5 LTS に関するよくある質問です。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: d18c9dc3-fdcc-4558-b9b6-ecf1ce61048a
source-git-commit: 004a3859c06e7c219e7919ac5920a9bc179ede43
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 91%

---

# AEM 6.5 LTS に関するよくある質問（FAQ） {#faq}

このページは、AEM 6.5 LTS に関するよくある質問への回答を目的としています。

## アドビが AEM の 6.5 LTS をリリースしたのはなぜですか？

アドビでは、提供するアプリケーションのセキュリティと安定性に引き続き全力で取り組んでいます。 AEM 6.5 長期サポートは、AEM 6.5 の今後のアップデートの基盤となります。 特に、AEM 6.5 LTS には、Oracle Java 17 および Java 21 のサポートが含まれており、AEM の新機能とイノベーションを受け取る AEM 分岐となります。

## オンプレミスのお客様は、AEM 6.5 LTS にアップグレードしないとどうなりますか？

AEM 6.5 LTS には、Oracle Java 17 および Java 21 のサポートを含む、重要なセキュリティと安定性のアップデートが含まれています。 組織は6.5 LTSへのアップグレードを計画することをお勧めします。 Adobeは、2027年2月28日まで引き続きAEM 6.5をサポートします。 詳細については、[&#x200B; ロードマップ &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap#aem65)を確認してください。

## AEM 6.5 LTS にアップグレードすると、既存のカスタマイズや統合は影響を受けますか？

AEM 6.5 LTS は、後方互換性を維持することを目的としていますが、一部の従来の機能とアーティファクトは削除されています。
[リリースノート](/help/release-notes/release-notes.md#deprecated-and-removed-features)を確認し、[AEM アナライザーツール](/help/sites-deploying/aem-analyzer.md)を使用して、カスタマイズと統合に対する影響を評価することが重要です。

## AEM 6.5 LTS にスムーズに移行するにはどうすればよいですか？

スムーズな移行を行うには、次の操作をお勧めします。

* [リリースノート](/help/release-notes/release-notes.md)とドキュメントを徹底的に確認します。
* [AEM アナライザーツール](/help/sites-deploying/aem-analyzer.md)を使用して、アップグレードの複雑さを評価します。
* アップグレードプロセスに十分な時間とリソースを計画して割り当てます。
* ガイダンスとサポートを取得するために、アドビのサポートおよびイネーブルメントセッションに参加します。

## AEM 6.5 LTS サービスパックとは何ですか？

AEM 6.5 LTS サービスパックとは、初回リリース以降に AEM 6.5 LTS に行われたすべての修正と改善を含む累積的なアップデートです。 AEM インスタンスが最新の機能とセキュリティパッチで最新の状態になるように、最新のサービスパックを適用することをお勧めします。

## 現在 AEM 6.5 を使用していますが、AEM 6.5 LTS GA リリースにアップグレードせずに、AEM 6.5 LTS サービスパックに直接アップグレードできますか？

はい、AEM 6.5 から任意の AEM 6.5 LTS サービスパックに直接アップグレードできます。 [リリースノート](/help/release-notes/release-notes.md)と [AEM 6.5 LTS へのアップグレード](/help/sites-deploying/upgrade.md)の節を確認することをお勧めします。

## 現在 AEM 6.5 LTS GA を使用していますが、AEM 6.5 LTS サービスパックにアップグレードするには、コードを変更する必要はありますか？

いいえ、AEM 6.5 LTS から AEM 6.5 LTS サービスパックにアップグレードするためにコードを変更する必要はありません。 ただし、サービスパックを実稼動インスタンスに適用する前に、[リリースノート](/help/release-notes/release-notes.md)を確認し、ステージング環境でカスタマイズと統合をテストすることを常にお勧めします。

## 新しい AEM 6.5 LTS 設定で最初から開始する必要がありますが、AEM 6.5 LTS サービスパックから直接開始できますか？

はい、AEM 6.5 LTS GA ビルドを設定せずに、新しい AEM 6.5 LTS サービスパックを直接設定できます。 詳しくは、[リリースノート](/help/release-notes/release-notes.md)と[カスタムスタンドアロンインストール](/help/sites-deploying/custom-standalone-install.md)の節を参照することをお勧めします。
