---
title: 必要なテスト環境の種類
description: テストの一部として考慮する必要がある環境はいくつかあります
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: f74fbf2b-62bb-4fac-9ecb-5ace90ba0275
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 100%

---

# 必要なテスト環境の種類{#which-test-environments-will-be-needed}

テストする設定を定義するには、次の点を考慮する必要があります。

**開発** — 単体テスト、特定の統合テストの場合。

**テスト** – ほとんどのテストの場合。

**ライブ** — 最終的なパフォーマンステストとストレステスト。顧客の受け入れテスト用。

必要なインスタンスと場所を決定します（通常、すべてのレベルのテストで各インスタンスのうち少なくとも 1 つ）。

**作成者** — このインスタンスで、作成者がコンテンツを入力したり公開したりできます。

**公開** — このインスタンスは、訪問者がアクセスするための、公開済みの形式の Web サイトを表します。

Dispatcher を使用してテスト。

最後に、実際のハードウェアを考慮する必要があります。パフォーマンステストは、可能な限り最終的な実稼働環境に近い設定のシステム上で行う必要があります。このため、プロジェクトのローンチは、次のように分割することをお勧めします。

**ソフトローンチ** – 可用性を制限。実稼動環境の現実的な条件下でパフォーマンステスト、チューニングおよび最適化を行う時間を確保できます。

**ハードローンチ** - 完全な可用性。
