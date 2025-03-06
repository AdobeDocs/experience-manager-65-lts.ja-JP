---
title: コマース統合フレームワークを使用した、AEM と Adobe Commerce の統合
description: AEM と Adobe Commerce は、コマース統合フレームワーク（CIF）を使用してシームレスに統合されます。CIF を使用すると、AEM は Adobe Commerce インスタンスにアクセスし、GraphQL を介して Adobe Commerce と通信できます。また、AEM オーサーは、製品とカテゴリの選択機能と製品コンソールを使用して、Adobe Commerce からオンデマンドで取得した製品およびカテゴリデータを参照できます。さらに、CIF には、コマースプロジェクトの迅速化に役立つ標準搭載のストアフロントが用意されています。
thumbnail: aem-magento-architecture.jpg
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: cecd9591-bff4-4b4e-a3fd-4ab4278a0b81
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 100%

---

# コマース統合フレームワークを使用した、AEM と Adobe Commerce（Magento）の統合 {#aem-commerce-framework}

Experience Manager と Adobe Commerce は、コマース統合フレームワーク（CIF）を使用してシームレスに統合されます。CIF を使用すると、AEM は Adobe Commerce の [GraphQL API](https://devdocs.magento.com/guides/v2.4/graphql/) を使用して、コマースインスタンスに直接アクセスして通信できます。

>[!NOTE]
>
>サポートされる GraphQL API の最小バージョンは 2.3.5 です。一部の機能は、新しいバージョンでのみ、または Adobe Commerce エディションでのみサポートされます。

## アーキテクチャの概要 {#overview}

全体的なアーキテクチャは次のとおりです。

![CIF アーキテクチャの概要](../assets/AEM_Magento_Architecture.png)

CIF 内では、サーバーサイドとクライアントサイドの通信パターンがサポートされます。
サーバーサイドの API 呼び出しは、組み込みの汎用 [GraphQL クライアント](https://github.com/adobe/commerce-cif-graphql-client)と、コマース GraphQL スキーマ用に[生成された一連のデータモデル](https://github.com/adobe/commerce-cif-magento-graphql)を組み合わせて実装されます。さらに、任意の GraphQL クエリや GQL 形式のバリエーションも使用できます。

[React](https://reactjs.org/) を使用して構築されるクライアントサイドコンポーネントの場合は、[Apollo Client](https://www.apollographql.com/docs/react/) が使用されます。

## AEM CIF コアコンポーネントのアーキテクチャ {#cif-core-components}

![AEM CIF コアコンポーネントのアーキテクチャ](../assets/cif-component-architecture.jpg)

[AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)は、[AEM WCM コアコンポーネント](https://github.com/adobe/aem-core-wcm-components)と同様の設計パターンとベストプラクティスに従っています。

AEM CIF コアコンポーネントの Adobe Commerce とのビジネスロジックとバックエンドの通信は、Sling Model で実装されます。プロジェクト固有の要件を満たすために、このロジックをカスタマイズする必要がある場合は、Sling モデルの委任パターンを使用できます。

>[!TIP]
>
>[AEM CIF コアコンポーネントのカスタマイズ](../customizing/customize-cif-components.md)ページには、CIF コアコンポーネントのカスタマイズ方法に関する詳細な例とベストプラクティスが記載されています。

プロジェクト内では、AEM CIF コアコンポーネントとカスタムプロジェクトコンポーネントは、Sling Context-Aware 設定を使用して、AEM ページに関連付けられた Adobe Commerce ストア用に設定されたクライアントを簡単に取得できます。
