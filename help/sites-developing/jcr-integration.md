---
title: JCR 統合
description: JCR レベルで Adobe Experience Manager と統合する必要がある場合のヒントを説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 6c5715f8-ff7e-47c3-8469-f97b6ea6fe03
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 100%

---

# JCR 統合{#jcr-integration}

## JCR API よりも Sling リソース API を優先 {#prefer-the-sling-resource-api-to-jcr-api}

Sling API は、JCR API よりも高度な抽象レベルで機能します。これにより、コードの再利用性を高め、コードを基になるストレージから独立させることができます。したがって、必要に応じて ResourceProvider メカニズムを利用して外部の仮想データを含めることがより簡単になります。

## 可能な限りクエリを回避 {#avoid-queries-wherever-possible}

常に、クエリを実行するよりも、リポジトリ内を移動してデータを取得する方が速くなります。エンドユーザークエリやリポジトリ全体から構造化されたコンテンツを探す必要がある場合などクエリが必要になりますが、それ以外の場合は必要なノードに移動することをお勧めします。ナビゲーション要素、「最近の項目リスト」、項目数などのレンダリングロジックでは、常にクエリを回避してください。このような場合、階層をたどっていくか、レンダリング時に直接結果を使用できるように事前に結果をキャッシュに格納しておく方が効率的です。

## JCR 監視の範囲の制限 {#restrict-the-scope-of-jcr-observation}

リポジトリでイベントをリッスンするときには、できる限り範囲を絞り込むことが重要です。例えば、`/etc` でリッスンするよりも `/etc/mycompany` でイベントをリッスンする方がはるかに効率的です。決してリポジトリルートではイベントをリッスンしないでください。加えて、コールバックメソッドが実行すべき内容が何もない場合は、可能な限り速やかに処理を完了するようにしてください。

## JCR 管理者アクセスの使用を排除する {#eliminate-use-of-jcr-admin-access}

AEM 6 以降、ResourceResolverFactory からの管理セッションが廃止されているのと同様、管理ログインも廃止されています。代わりに、このタイプのアクセスを必要とするバックオフィス操作には、サービスアカウントを作成してください。ResourceResolverFactory を使用して、このアカウントの ResourceResolver を取得できます。
