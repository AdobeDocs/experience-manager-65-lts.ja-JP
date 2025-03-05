---
product: adobe experience manager
description: Adobe Experience Manager 6.5 LTS ドキュメント。
git-repo: https://github.com/AdobeDocs/experience-manager-65-lts.ja-JP
hide: y
type: Documentation
solution: Experience Manager
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
source-git-commit: 59969e1e669f6aef3f0d480b5dbdad0bdf28a1d7
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 52%

---


# 内部使用メタデータ

GitHub オーサリングシステムのメタデータは階層的で、次に示す上位段階まで定義されています。

1. metadata.md
1. 目次
1. 記事

metadata.md ファイルで定義されたメタデータはリポジトリ全体に適用されますが、目次と記事のレベルで上書きできます。メタデータの上書きは、可能な限り低いレベルで行う必要があります。

最低限必要なのは、experience-manager-cloud-service.en リポジトリ内のメタデータです。

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
* `contentOwner` （`/help/assets` 下のコアアセットコンテンツのみ）
