---
title: コードの落とし穴
description: AEM の開発時に避けるべき一般的なコードの落とし穴
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 95656312-2648-455e-80fb-3e03bf1cd633
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 100%

---

# コードの落とし穴{#code-pitfalls}

## Java コードで Sling Binding を使用しない {#avoid-sling-bindings-in-java-code}

Sling Binding はほとんどの場合、サービスにアクセスする方法として適切ではありません。代わりに、*@Reference* または *@Inject* 注釈を使用してください。

## Java コードで Thread.interrupt を使用しない {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* を不適切なタイミングで呼び出すと、Lucene ファイルや永続キャッシュファイルなどのファイルが閉じられる可能性があるので危険です。

## Java 同期を ReadWriteLock と共に使用しない {#avoid-mixing-java-synchronization-with-readwritelocks}

競合状態が発生し、最終的にコードのデッドロックが発生することがあります。
