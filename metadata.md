---
product: adobe experience manager
description: Adobe Experience Manager 6.5 LTS ドキュメント。
git-repo: https://github.com/AdobeDocs/experience-manager-65-lts.ja-JP
index: true
type: Documentation
solution: Experience Manager, Experience Manager 6.5 LTS
nudge: 'yes'
usetq: true
landing-page-name: experience-manager-65-lts
landing-page-breadcrumb-title: AEM 6.5 LTS
version: Experience Manager 6.5 LTS
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
cloud: Experience Cloud
recommendations: noDisplay
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: ae206583-dab1-444b-b978-a37aad4a988c
    internal-label: Experience Manager 6.5 LTS
source-git-commit: 58a193a94397bae99fec88ee9353c415d374912a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 2%
---

# 内部使用のためのメタデータ

GitHub オーサリングシステムのメタデータは階層であり、次のレベルの前例で定義されています。

1. metadata.md
1. ToC
1. 記事

metadata.md ファイルで定義されたメタデータは、リポジトリ全体に適用されますが、ToC レベルとアーティクルレベルで上書きできます。 メタデータの上書きは、可能な限り低いレベルで行う必要があります。

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

ToCs

* `sub-product`
* `user-guide-title`

記事

* `title`
* `description`
* `contentOwner` （`/help/assets`以下のコアアセットコンテンツに対してのみ）
