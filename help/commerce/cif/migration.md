---
title: AEM Commerce Integration Framework（CIF）アドオンへの移行
description: 旧バージョンから AEM Commerce Integration Framework（CIF）アドオンに移行する方法。
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: 847c33c1-17d6-447a-9f2c-91f2a81a3f04
source-git-commit: 981b175b039fd7ffbddf558a77d2da2fed52ad79
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 93%

---

# Experience Manager アドオンの移行ガイド {#cif-migration}

このガイドは、Experience Manager アドオンの移行に向けて更新が必要な領域を特定するのに役立ちます。

## CIF アドオン

CIF アドオンは、[ ソフトウェア配布ポータル ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?fulltext=commerce*&2_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2Fdc%3Aversion&2_group.propertyvalues.operation=equals&2_group.propertyvalues.0_values=target-version%3Aaem%2F6-5-lts&orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&orderby.sort=desc&layout=list&p.offset=0&p.limit=16) を通じて入手できます。 このアドオンは Experience Manager as a Cloud Service 向けの CIF アドオンと互換性があり、同じ機能を提供します。

[AEM Content and Commerce 使用の手引き](getting-started.md)を参照してください。

CIF をデプロイするプロジェクトをサポートするために、アドビでは [AEM CIF コアコンポーネント](https://github.com/adobe/aem-core-cif-components)を提供しています。

## 製品カタログ

製品カタログデータのインポートは、CIF アドオンではサポートされていません。CIF アドオンの原則に従って、製品およびカタログリクエストは、外部コマースソリューションへのリアルタイム呼び出しを通じてオンデマンドで行われます。コマースソリューションの統合について詳しくは、「統合」の章を参照してください。

>[!TIP]
>
>リアルタイム API を使用できない場合は、API を使用した外部製品キャッシュを統合に使用する必要があります。例：[Magento オープンソース](https://business.adobe.com/jp/products/magento/open-source.html)

## AEM レンダリングを使用した製品カタログエクスペリエンス

クラシック CIF でカタログブループリントを使用する場合は、製品カタログワークフローを更新する必要があります。CIF アドオンは、AEM カタログテンプレートを使用して、製品カタログエクスペリエンスをその場でレンダリングするようになりました。製品データや製品ページのレプリケーションは不要になりました。

## キャッシュ不可データとショッピングインタラクション

キャッシュ不可データおよびインタラクションについてのクライアントサイドのリクエスト（例：買い物かごへの追加、検索）は、CDN や Dispatcher を介してコマースエンドポイント（コマースソリューションまたは統合レイヤー）に直接送信する必要があります。AEM がプロキシに過ぎない呼び出しは、すべて削除します。
