---
title: ContextHub
description: ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
exl-id: c7c42bcd-d90a-430a-bbcd-b104d0670ebf
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 100%

---

# ContextHub{#contexthub}

ContextHub は、コンテキストデータを保存、操作および表示するためのフレームワークです。クライアントサイド JavaScript API を使用してデータにアクセスし、コンテンツをパーソナライズします。

>[!NOTE]
>
>[We.Retail 参照実装](/help/sites-developing/we-retail.md)は、ContextHub を実装しており、ContextHub をプロジェクトに組み込む際の参考になります。

>[!CAUTION]
>
>[We.Retail 参照実装](/help/sites-developing/we-retail.md)で使用される ContextHub 設定のサンプルを含むパス（`/libs/settings/cloudsettings/legacy`）は、独自の設定を作成する際の参考としてご利用ください。
>
>独自の ContextHub 設定としてプロジェクトで使用しないでください。

## 永続性 {#persistence}

ContextHub ストアは、コンテキストデータをクライアント上に保持します。ContextHub JavaScript API を使用してストアにアクセスし、必要に応じてデータを作成、更新および削除できます。したがって、ContextHub はページ上のデータレイヤーに相当します。

個々の ContextHub ストアは、事前定義されたストアタイプのインスタンスです。

* ContextHub には、いくつかの[ストアタイプのサンプル](/help/sites-developing/ch-samplestores.md)が用意されています。
* AEM コンソールを使用して[ストアを作成](ch-configuring.md#creating-a-contexthub-store)します。
* デベロッパーは、[カスタムストアタイプを作成](/help/sites-developing/ch-extend.md#creating-custom-store-candidates)できます。
* 開発者は、JavaScript を使用して[ストアデータにアクセス](/help/sites-developing/ch-adding.md#interacting-with-contexthub-stores)できます。

## セグメント化 {#segmentation}

ContextHub には、セグメントの管理や、現在のコンテキストで解決されるセグメントを判断するセグメント化エンジンが含まれています。いくつかのセグメントが定義されています。JavaScript API を使用して、[解決されたセグメントを判断](/help/sites-developing/ch-adding.md#determining-resolved-contexthub-segments)できます。

## プレゼンテーション {#presentation}

マーケターと作成者は、[ContextHub ツールバー](/help/sites-authoring/ch-previewing.md)を使用してストアデータを表示および操作し、ページのオーサリング時にユーザーエクスペリエンスをシミュレートできます。このツールバーは、ContextHub ストアへのアクセスを提供する UI モジュールのグループで構成されています。

各 ContextHub UI モジュールは、事前定義されたモジュールタイプのインスタンスです。

* ContextHub には、いくつかの[モジュールタイプのサンプル](/help/sites-developing/ch-samplemodules.md)が用意されています。
* AEM コンソールを使用して [UI モジュールを追加](ch-configuring.md#adding-a-ui-module)し、[UI モードにグループ化](ch-configuring.md#adding-a-ui-mode)します。

* 開発者は、[カスタムモジュールタイプを作成](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)できます。

開発者は、[ContextHub コンポーネントをページに追加](/help/sites-developing/ch-adding.md)する必要があります。
