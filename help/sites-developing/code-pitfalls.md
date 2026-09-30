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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 100%
---
# コードの落とし穴{#code-pitfalls}

## Java コードで Sling Binding を使用しない {#avoid-sling-bindings-in-java-code}

Sling Binding はほとんどの場合、サービスにアクセスする方法として適切ではありません。 代わりに、*@Reference* または *@Inject* 注釈を使用してください。

## Java コードで Thread.interrupt を使用しない {#avoid-thread-interrupt-in-java-code}

*Thread.interrupt* を不適切なタイミングで呼び出すと、Lucene ファイルや永続キャッシュファイルなどのファイルが閉じられる可能性があるので危険です。

## Java 同期を ReadWriteLock と共に使用しない {#avoid-mixing-java-synchronization-with-readwritelocks}

競合状態が発生し、最終的にコードのデッドロックが発生することがあります。
