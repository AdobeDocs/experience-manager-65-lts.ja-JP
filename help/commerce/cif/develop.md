---
title: AEM Commerce の開発
description: AEM プロジェクトアーキタイプを使用してコマース対応の AEM プロジェクトを生成する方法を説明します。プロジェクトを構築し、ローカル開発環境にデプロイする方法を説明します。
topics: Commerce, Development
feature: Commerce Integration Framework
doc-type: tutorial
kt: 5826
thumbnail: 39476.jpg
solution: Experience Manager,Commerce
role: Admin, Developer
exl-id: 22fcdadf-12c0-4545-a854-76345806386f
source-git-commit: 5995dda0aac101e6c0d506ac5bba786674b0735b
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 56%

---

# AEM Commerce の開発 {#develop}

Commerce integration framework（CIF）に基づくAEM Commerce プロジェクトをAEM用に開発する場合も、他のAEM プロジェクトと同じルールとベストプラクティスに従います。 最初に次の点を確認します。

- [AEM開発ユーザーガイド](/help/sites-developing/getting-started.md)
- [AEM の中心概念](/help/sites-developing/the-basics.md)
- [AEM の開発 - ガイドラインとベストプラクティス](/help/sites-developing/dev-guidelines-bestpractices.md)
- [Apache Maven を使用して AEM プロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)

## AEM Commerceのローカル開発 {#local}

CIF プロジェクトを使用する場合は、ローカル開発環境を使用することをお勧めします。

>[!NOTE]
>
>以下の手順は、CIF for AEM 6.5 LTS を使用してAEM Commerce用のローカル AEM開発環境をセットアップする場合に役立ちます。 AEM as a Cloud Service を使用している場合は、[AEM Commerce as a Cloud Service](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/content-and-commerce/introduction#) ドキュメントを参照してください。

CIF アドオンと呼ばれるAEM用のAEM Commerce アドオンもローカル開発が可能で、AEM パッケージとして提供されます。 これは、[&#x200B; ソフトウェア配布ポータル &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) から機能パックとしてダウンロードできます。

### 必要なソフトウェア

以下をローカルにインストールしておく必要があります。

- ローカル AEM 6.5 LTS
- [Java 17/Java 21](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/general.html)
- [Apache Maven](https://maven.apache.org/)（3.3.9 以降）
- [Node LTS](https://nodejs.org/ja/)
- [npm 6 以降](https://www.npmjs.com/)
- [Git](https://git-scm.com/)

### CIF アドオンへのアクセス

CIF アドオンは、[&#x200B; ソフトウェア配布ポータル &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html) からダウンロードして、`AEM Commerce add-on` を検索できます。

>[!TIP]
>
>常に最新バージョンのCIF アドオンを使用するようにしてください。

### ローカル設定

AEMとアドオン CIFを使用するローカル CIF プロジェクト開発の場合は、次の手順を実行します。

1. AEM.jar を解凍し、`crx-quickstart` フォルダーを作成します。次を実行します。

   ```bash
   java -jar <jar name> -unpack
   ```

1. `crx-quickstart/install` フォルダーの作成

1. ソフトウェア配布ポータルからダウンロードした CIF アドオンのすべてのパッケージを `crx-quickstart/install` フォルダーにコピーします。

>[!TIP]
>
>または、パッケージマネージャーを使用してCIF アドオンパッケージをインストールします。

1. AEM クイックスタートを起動します。

OSGI コンソールを使用して設定を確認します：`http://localhost:4502/system/console/osgi-installer`。 このリストには、CIF アドオン関連バンドル、コンテンツパッケージ、OSGI 設定が含まれている必要があります。すべてのバンドルが起動されていることを確認します。

## プロジェクトのセットアップ {#project}

CIF を使用して AEM Commerce プロジェクトを開始する方法は 2 とおりあります。

### AEM プロジェクトアーキタイプの使用

CIF を使い始めるために事前に設定されたプロジェクトを Bootstrap するには、[AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)が主なツールです。CIF コアコンポーネントと必要なすべての設定を、生成されたプロジェクトに 1 つの追加オプションで含めることができます。

>[!TIP]
>
>プロジェクトを生成するには、[AEM プロジェクトアーキタイプ 25 以降](https://github.com/adobe/aem-project-archetype/releases)を使用します。

AEM プロジェクトの生成方法については、AEM プロジェクトアーキタイプの「[使用手順](https://github.com/adobe/aem-project-archetype#usage)」を参照してください。プロジェクトに CIF を含めるには、`includeCommerce` オプションを使用します。

次に例を示します。

```bash
mvn -B archetype:generate \
 -D archetypeGroupId=com.adobe.granite.archetypes \
 -D archetypeArtifactId=aem-project-archetype \
 -D aemVersion=6.5.5 \
 -D appTitle="My Site" \
 -D appId="mysite" \
 -D groupId="com.mysite" \
 -D frontendModule=general \
 -D includeExamples=n \
 -D includeCommerce=y
```

CIF コアコンポーネントは、任意のプロジェクトで使用できます。 提供された `all` パッケージを含めるか、CIF コンテンツパッケージと関連する OSGi バンドルを個別に使用します。 次の依存関係を使用して、CIF コアコンポーネントを手動でプロジェクトに追加します。

```java
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-apps</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-config</artifactId>
    <type>zip</type>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>core-cif-components-core</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>graphql-client</artifactId>
    <version>x.y.z</version>
</dependency>
<dependency>
    <groupId>com.adobe.commerce.cif</groupId>
    <artifactId>magento-graphql</artifactId>
    <version>x.y.z</version>
</dependency>
```

### AEM Venia 参照用ストアの使用

CIF プロジェクトを開始する 2 つ目の方法は、[AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)をコピーして使用する方法です。AEM Venia 参照用ストアは、AEM 用の CIF コアコンポーネントの使用方法を示すサンプルのストアフロントアプリケーションです。これは、ベストプラクティス例として意図されていて、独自機能を開発するための有望な出発点としての役割も果たします。

[Git リポジトリをクローンして Venia 参照用ストアの使用を開始し &#x200B;](https://github.com/adobe/aem-cif-guides-venia) 必要に応じてプロジェクトをカスタマイズする開始。

>[!NOTE]
>
>Venia 参照用ストアプロジェクトには、AEM as a Cloud Service 用および AEM 6.5 用の 2 つのビルドプロファイルが含まれています。[project readme.md](https://github.com/adobe/aem-cif-guides-venia/blob/main/README.md) を参照して、使用方法を確認してください。AEM 6.5 の場合は、 `classic` プロファイルを使用します。

### コマースシステムへの AEM の接続

プロジェクトをコマースシステムに接続するには、コマースシステムのGraphQL エンドポイントをAEMに設定する必要があります。

[AEM プロジェクトアーキタイプで生成されたプロジェクトにも &#x200B;](https://github.com/adobe/aem-project-archetype) [AEM Venia 参照用ストア &#x200B;](https://github.com/adobe/aem-cif-guides-venia) で生成されたプロジェクトにも、デフォルト設定が既に含まれており、これを調整する必要があります。

`com.adobe.cq.commerce.graphql.client.impl.GraphqlClientImpl~default.cfg.json` の `url` の値を、プロジェクトで使用されるコマースシステムの GraphQL エンドポイントに置き換えます。

AEM Commerce アドオンとCIF コアコンポーネントは、AEM サーバーを介してCommerce GraphQL エンドポイントに接続します。 または、ブラウザーから直接。 クライアントサイドのCIF コアコンポーネントとCIF アドオンのオーサリングツールは、デフォルトで `/api/graphql` に接続します。 必要に応じて、CIF Cloud Service設定を使用して調整できます（以下を参照）。

CIF アドオンは、`/api/graphql` で GraphQL プロキシサーブレットを提供します。ローカルの AEM Dispatcher を使用する予定がない場合は、GraphQL プロキシサーブレットも設定することをお勧めします。

http://localhost:4502/system/console/configMgr に移動し、`Adobe CIF GraphQL Proxy Configuration` サービスの OSGI 設定を作成します。 上記の GraphQL クライアントで使用したのと同じ GraphQL エンドポイントを、コマースシステムで使用します。

## その他のリソース

- [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
- [AEM Venia 参照用ストア](https://github.com/adobe/aem-cif-guides-venia)
