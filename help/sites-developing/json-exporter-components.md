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
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 100%

---

# コンポーネントの JSON 書き出しの有効化{#enabling-json-export-for-a-component}

モデラーフレームワークに基づいてコンテンツの JSON 書き出しを生成するように、コンポーネントを適応させることができます。

## 概要 {#overview}

JSON 書き出しは、[Sling Model](https://sling.apache.org/documentation/bundles/models.html) と [Sling Model Exporter](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) フレームワーク（それ自体が [Jackson 注釈](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)に依存）に基づいています。

つまり、JSON を書き出す必要がある場合、コンポーネントには Sling Model が必要です。したがって、次の 2 つの手順に従って、任意のコンポーネントで JSON 書き出しを有効にします。

* [コンポーネントに Sling Model を定義する](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Sling Model インターフェイスに注釈を付ける](#annotate-the-sling-model-interface)

## コンポーネントに Sling Model を定義する {#define-a-sling-model-for-the-component}

まず、コンポーネントに Sling モデルを定義する必要があります。

>[!NOTE]
>
>Sling モデルの使用例について詳しくは、[AEM での Sling モデルエクスポーターの開発](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=ja)を参照してください。

Sling Model の実装クラスに次のような注釈を付ける必要があります。

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

これにより、`.model` セレクターと `.json` 拡張子を使用して、コンポーネントをそれ自体に書き出すことができます。

さらに、Sling Model クラスが `ComponentExporter` インターフェイスに適応できるように指定されます。

>[!NOTE]
>
>Jackson 注釈は Sling モデルクラスレベルではなく、モデルインターフェイスレベルで指定されます。これは、JSON 書き出しがコンポーネント API の一部とみなされるようにするためです。

>[!NOTE]
>
>`ExporterConstants` クラスと `ComponentExporter` クラスは `com.adobe.cq.export.json` バンドルから取得されます。

### 複数のセレクターの使用 {#multiple-selectors}

標準的なユースケースではありませんが、`model` セレクターに加えて複数のセレクターを設定することができます。

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

ただし、その場合は、`model` セレクターを最初のセレクターにし、拡張子を `.json` にする必要があります。

## Sling Model インターフェイスに注釈を付ける {#annotate-the-sling-model-interface}

JSON エクスポーターフレームワークで認識されるようにするには、モデルインターフェイスに `ComponentExporter` インターフェイス（またはコンテナコンポーネントの場合は `ContainerExporter`）を実装する必要があります。

対応する Sling モデルインターフェイス（`MyComponent`）には、[Jackson 注釈](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)を使用して注釈が付けられ、どのように書き出し（シリアル化）が行われるかが定義されます。

シリアル化されるメソッドを定義するためには、モデルインターフェイスに適切に注釈を付ける必要があります。デフォルトでは、getter の通常の命名規則に準拠するすべてのメソッドがシリアル化され、JSON プロパティ名が getter 名から派生されます。これを回避または上書きするには、`@JsonIgnore` または `@JsonProperty` を使用して JSON プロパティの名前を変更します。

## 例 {#example}

コアコンポーネントは、[リリース 1.1.0](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) 以降、JSON 書き出しをサポートしており、参照として使用できます。

例えば、画像コアコンポーネントの Sling Model 実装とその注釈されたインターフェイスを参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub の aem-core-wcm-components プロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)としてダウンロードします

## 関連ドキュメント {#related-documentation}

詳しくは、次を参照してください。

* [Assets ユーザーガイドのコンテンツフラグメントに関するトピック](https://helpx.adobe.com/jp/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [コンテンツフラグメントモデル](/help/assets/content-fragments/content-fragments-models.md)
* [コンテンツフラグメントを使用したオーサリング](/help/sites-authoring/content-fragments.md)
* [コンテンツサービス用の JSON エクスポーター](/help/sites-developing/json-exporter.md)
* [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja)および[コンテンツフラグメントコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=ja)
