---
title: アセットの命名規則のテスト
description: リポジトリーのノードは、Java コンテンツリポジトリーの命名規則の対象です。 ただし、アセットノード名には Adobe Experience Manager によって追加の規則が課せられます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 37de1a8b-b7db-469e-98a7-20ddb6218510
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 100%
---
# アセットの命名規則のテスト{#naming-conventions-for-assets-testing}

リポジトリーのノードは、[Java コンテンツリポジトリー](/help/sites-developing/the-basics.md#java-content-repository)の命名規則の対象です。 ただし、アセットノード名には Adobe Experience Manager によって追加の規則が課せられます。

## クラシック UI {#classic-ui}

クラシック UI にはさらに厳しい制約があります。

* アセット名が有効と判断されるのは、明示的なノード名が次のいずれかの場合です。

  * ノード名に変換されるようにアセットタイトルが指定されている。
  * 明示的なノード名が指定されている。

* 有効な文字（アセットがクラシック UI で作成されるとき次の文字のみが有効です）：

  * a～z
  * A～Z
  * 0～9
  * _（アンダースコア）
  * `-`（ダッシュ／マイナス）
