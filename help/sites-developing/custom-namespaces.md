---
title: カスタム名前空間
description: AEM 6.5 LTSにカスタム名前空間を定義してデプロイする方法について説明します。
solution: Experience Manager, Experience Manager Sites
feature: Developing,JCR
role: Developer
source-git-commit: 31d67c5b9bff651077df5a497e5c318b86a48158
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 66%

---


# カスタム名前空間{#custom-namespaces}

カスタム [名前空間](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/4.5_Namespaces.html)を定義してAEM 6.5 LTSにデプロイする方法について説明します。

カスタム名前空間は、JCR プロパティの「`:`」の前にあるオプション部分です。 AEM では、次のようないくつかの名前空間を使用します。

+ `jcr`（JCR システムプロパティの場合）
+ `cq`（AEM（旧称 Adobe CQ）プロパティの場合）
+ `dam`（DAM アセット固有の AEM プロパティの場合）
+ `dc`（Dublin Core プロパティの場合）

その他多数

名前空間を使用すると、プロパティの範囲と目的を示すことができます。 カスタム名前空間（多くの場合、会社名）を作成すると、AEM 実装に固有のノードやプロパティを明確に識別し、自社のビジネスに固有のデータを含めることができます。

カスタム名前空間は[Sling リポジトリ初期化（repoinit） ](https://sling.apache.org/documentation/bundles/repository-initialization.html) スクリプトで管理され、プロジェクトの設定パッケージのOSGi設定（例：`ui.config`）としてデプロイされます。

## リソース

+ [Sling リポジトリー初期化（repoinit）のドキュメント](https://sling.apache.org/documentation/bundles/repository-initialization.html#repoinit-parser-test-scenarios)

## コード

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
