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
source-wordcount: '557'
ht-degree: 55%
---
# コンポーネントのJSON エクスポートを有効にする{#enabling-json-export-for-a-component}

モデラーフレームワークに基づいてコンテンツの JSON 書き出しを生成するように、コンポーネントを適応させることができます。

## 概要 {#overview}

JSON書き出しは、[Sling Model](https://sling.apache.org/documentation/bundles/models.html)および[Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) フレームワーク（それ自体は[Jackson注釈](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)に依存）に基づいています。

このアプローチは、JSONを書き出す必要がある場合、コンポーネントにSling モデルが必要であることを意味します。 したがって、次の 2 つの手順に従って、任意のコンポーネントで JSON 書き出しを有効にします。

* [コンポーネントに Sling Model を定義する](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Sling Model インターフェイスに注釈を付ける](#annotate-the-sling-model-interface)

## コンポーネントに Sling Model を定義する {#define-a-sling-model-for-the-component}

最初に、コンポーネントにSling モデルを定義する必要があります。

>[!NOTE]
>
>Sling モデルの使用例について詳しくは、[AEM での Sling モデルエクスポーターの開発](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter)を参照してください。

Sling Model の実装クラスに次のような注釈を付ける必要があります。

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

これにより、`.model` セレクターと`.json`拡張機能を使用して、独自にコンポーネントを書き出すことができます。

また、Sling Model クラスを`ComponentExporter` インターフェイスに適応させることができることを指定します。

>[!NOTE]
>
>Jackson 注釈は Sling モデルクラスレベルではなく、モデルインターフェイスレベルで指定されます。 このアプローチは、JSON書き出しがコンポーネント APIの一部と見なされるようにするためのものです。

>[!NOTE]
>
>`ExporterConstants` クラスと `ComponentExporter` クラスは `com.adobe.cq.export.json` バンドルから取得されます。

### 複数のセレクターを使用 {#multiple-selectors}

標準的なユースケースではありませんが、`model` セレクターに加えて複数のセレクターを設定することができます。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

ただし、そのような場合、`model` セレクターは最初のセレクターで、拡張子は`.json`である必要があります。

## Sling Model インターフェイスに注釈を付ける {#annotate-the-sling-model-interface}

JSON エクスポーターフレームワークで処理するには、モデルインターフェイスで`ComponentExporter` インターフェイス（コンテナコンポーネントの場合は`ContainerExporter`）を実装する必要があります。

対応する Sling モデルインターフェイス（`MyComponent`）には、[Jackson 注釈](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)を使用して注釈が付けられ、どのように書き出し（シリアル化）が行われるかが定義されます。

どのメソッドをシリアル化するかを定義するには、モデル インターフェイスに適切に注釈を付ける必要があります。 デフォルトでは、ゲッターの通常の命名規則を尊重するすべてのメソッドはシリアル化され、JSON プロパティ名はゲッター名から自然に派生します。 このアプローチは、`@JsonIgnore`または`@JsonProperty`を使用してJSON プロパティの名前を変更することで、防止または上書きできます。

## 例 {#example}

コアコンポーネントは、[リリース 1.1.0](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/introduction) 以降、JSON 書き出しをサポートしており、参照として使用できます。

例えば、画像コアコンポーネントの Sling Model 実装とその注釈されたインターフェイスを参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHubでaem-core-wcm-components プロジェクトを開きます](https://github.com/adobe/aem-core-wcm-components)
* プロジェクトを [ZIP ファイル](https://codeload.github.com/adobe/aem-core-wcm-components/zip/main)としてダウンロードします


## 関連ドキュメント {#related-documentation}

* [Assets ユーザーガイドのコンテンツフラグメントに関するトピック](https://experienceleague.adobe.com/en/docs/experience-manager-64/assets/home#)
* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
* [コンテンツフラグメントを使用したオーサリング](/help/sites-authoring/content-fragments.md)
* [コンテンツサービス用の JSON エクスポーター](/help/sites-developing/json-exporter.md)
* [コアコンポーネント](https://experienceleague.adobe.com/ja/docs/experience-manager-core-components/using/introduction)および[コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/wcm-components/content-fragment-component)
