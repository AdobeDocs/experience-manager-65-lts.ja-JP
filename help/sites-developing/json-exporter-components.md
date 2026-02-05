---
title: コンポーネントの JSON 書き出しの有効化
description: モデラーフレームワークに基づいてコンテンツの JSON 書き出しを生成するように、コンポーネントを適応させることができます。
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: aeb8e954-dd6c-4e18-bb78-6eaac86fa4b9
source-git-commit: cc96a14ebaf9f895a798b5f4904f5b4769b990bb
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 56%

---

# コンポーネントの JSON エクスポートを有効にする{#enabling-json-export-for-a-component}

モデラーフレームワークに基づいてコンテンツの JSON 書き出しを生成するように、コンポーネントを適応させることができます。

## 概要 {#overview}

JSON の書き出しは、[Sling Models](https://sling.apache.org/documentation/bundles/models.html) と、[Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) フレームワーク（それ自体は [Jackson 注釈 &#x200B;](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) に依存）に基づいて行われます。

つまり、JSON を書き出す必要がある場合、コンポーネントには Sling モデルが必要です。 したがって、次の 2 つの手順に従って、任意のコンポーネントで JSON 書き出しを有効にします。

* [コンポーネントに Sling Model を定義する](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Sling Model インターフェイスに注釈を付ける](#annotate-the-sling-model-interface)

## コンポーネントに Sling Model を定義する {#define-a-sling-model-for-the-component}

まず、コンポーネントの Sling モデルを定義する必要があります。

>[!NOTE]
>
>Sling モデルの使用例について詳しくは、[AEM での Sling モデルエクスポーターの開発](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter)を参照してください。

Sling Model の実装クラスに次のような注釈を付ける必要があります。

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

これにより、コンポー `.model` ントセレクターと `.json` 拡張機能を使用して、コンポーネントを独自に書き出すことができます。

さらに、Sling Model クラスを `ComponentExporter` インターフェイスに適応させることができるかどうかを指定します。

>[!NOTE]
>
>Jackson 注釈は Sling モデルクラスレベルではなく、モデルインターフェイスレベルで指定されます。このアプローチは、JSON 書き出しが確実にコンポーネント API の一部と見なされるようにするためです。

>[!NOTE]
>
>`ExporterConstants` クラスと `ComponentExporter` クラスは `com.adobe.cq.export.json` バンドルから取得されます。

### 複数のセレクターを使用 {#multiple-selectors}

標準的なユースケースではありませんが、`model` セレクターに加えて複数のセレクターを設定することができます。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

ただし、この場合 `model` セレクターは最初のセレクターで、拡張子は `.json` にする必要があります。

## Sling Model インターフェイスに注釈を付ける {#annotate-the-sling-model-interface}

JSON エクスポーターフレームワークでこれを処理するには、モデルインターフェイスに `ComponentExporter` インターフェイス（またはコンテナコンポーネントの `ContainerExporter`）を実装する必要があります。

対応する Sling モデルインターフェイス（`MyComponent`）には、[Jackson 注釈](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)を使用して注釈が付けられ、どのように書き出し（シリアル化）が行われるかが定義されます。

シリアル化するメソッドを定義するには、Model インターフェイスに適切な注釈を付ける必要があります。 デフォルトでは、ゲッターの通常の命名規則に従うすべてのメソッドはシリアル化され、JSON プロパティ名がゲッター名から自然に派生します。 この方法は、`@JsonIgnore` または `@JsonProperty` を使用して、JSON プロパティの名前を変更することで、防止または上書きできます。

## 例 {#example}

コアコンポーネントは、[リリース 1.1.0](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/introduction) 以降、JSON 書き出しをサポートしており、参照として使用できます。

例えば、画像コアコンポーネントの Sling Model 実装とその注釈されたインターフェイスを参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-core-wcm-components プロジェクトを開きます](https://github.com/adobe/aem-core-wcm-components)
* プロジェクトを [ZIP ファイル](https://codeload.github.com/adobe/aem-core-wcm-components/zip/main)としてダウンロードします


## 関連ドキュメント {#related-documentation}

* [Assets ユーザーガイドのコンテンツフラグメントに関するトピック](https://experienceleague.adobe.com/ja/docs/experience-manager-64/assets/home#)
* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
* [コンテンツフラグメントを使用したオーサリング](/help/sites-authoring/content-fragments.md)
* [コンテンツサービス用の JSON エクスポーター](/help/sites-developing/json-exporter.md)
* [コアコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/introduction)および[コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/wcm-components/content-fragment-component)
