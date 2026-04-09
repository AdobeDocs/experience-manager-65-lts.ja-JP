---
product: adobe experience manager
description: Adobe Experience Manager 6.5 LTS ドキュメント。
git-repo: https://github.com/AdobeDocs/experience-manager-65-lts.ja-JP
index: true
type: Documentation
solution: Experience Manager, Experience Manager 6.5 LTS
version: Experience Manager 6.5 LTS
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: b8671573afd711dec4b883b3b382304e13889852
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 52%

---


# 内部使用メタデータ

GitHub オーサリングシステムのメタデータは階層であり、次のレベルの前例で定義されています。

1. metadata.md
1. 目次
1. 記事

metadata.md ファイルで定義されたメタデータはリポジトリ全体に適用されますが、目次と記事のレベルで上書きできます。メタデータの上書きは、可能な限り低いレベルで行う必要があります。

experience-manager-cloud-service.en リポジトリのメタデータは、必要な最小値です。

metadata.md

* `product`
* `git-repo`
* `index`
* `solution-title`
* `solution-hub-url`
* `getting-started-title`
* `getting-started-url`
* `tutorials-title`
* `tutorials-url`

目次

* `sub-product`
* `user-guide-title`

記事

* `title`
* `description`
* `contentOwner` （`/help/assets`以下のコアアセットコンテンツに対してのみ）
