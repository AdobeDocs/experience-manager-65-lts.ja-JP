---
title: カスタム名前空間
description: AEM 6.5 LTSにカスタム名前空間を定義してデプロイする方法について説明します。
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: f2d27a5f-0d67-4d85-8a24-86a8d8a3574b
    internal-label: Developer tools
subfeature_v2:
  - id: cd14456d-a492-4b5c-8a82-1fbd4460dbd2
    internal-label: Java Content Repository
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: d1f055e0688c24b55f80c7e2be974fe1d28ae8d5
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 61%
---

# カスタム名前空間{#custom-namespaces}

カスタム [名前空間](https://experienceleague.adobe.com/en/tools/aem-api-documentation/spec/jcr/1.0/4.5_Namespaces.html)を定義してAEM 6.5 LTSにデプロイする方法について説明します。

カスタム名前空間は、JCR プロパティの「`:`」の前にあるオプション部分です。 AEM では、次のようないくつかの名前空間を使用します。

+ `jcr`（JCR システムプロパティの場合）
+ `cq`（AEM（旧称 Adobe CQ）プロパティの場合）
+ `dam`（DAM アセット固有の AEM プロパティの場合）
+ `dc`（Dublin Core プロパティの場合）

その他多数

名前空間を使用すると、プロパティの範囲と目的を示すことができます。 カスタム名前空間（多くの場合、会社名）を作成すると、AEM 実装に固有のノードやプロパティを明確に識別し、自社のビジネスに固有のデータを含めることができます。

カスタム名前空間は[Sling リポジトリ初期化（repoinit） &#x200B;](https://sling.apache.org/documentation/bundles/repository-initialization.html) スクリプトで管理され、プロジェクトの設定パッケージのOSGi設定（例：`ui.config`）としてデプロイされます。

## リソース {#resources}

+ [Sling リポジトリー初期化（repoinit）のドキュメント](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios)

## コード {#code}

次のコードを使用して、`wknd` 名前空間を設定します。

### RepositoryInitializer OSGi 設定

`/ui.config/src/main/content/jcr_root/apps/wknd-examples/osgiconfig/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~wknd-examples-namespaces.cfg.json`

```json
{
    "scripts": [
        "register namespace (wknd) https://site.wknd/1.0"
    ]
}
```

これにより、`register namespace`命令の後の最初のパラメーターで示される`wknd`名前空間を使用したカスタムプロパティをAEMで使用できるようになります。 より詳細なスクリプト定義については、[Sling リポジトリ初期化（repoinit）のドキュメント](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios)で取り上げている例を確認してください。
