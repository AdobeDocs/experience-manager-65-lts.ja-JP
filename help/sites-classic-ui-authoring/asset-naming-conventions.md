---
title: アセットの命名規則のテスト
description: リポジトリーのノードは、Java コンテンツリポジトリーの命名規則の対象です。ただし、アセットノード名には Adobe Experience Manager によって追加の規則が課せられます。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
exl-id: 37de1a8b-b7db-469e-98a7-20ddb6218510
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 100%

---

# アセットの命名規則のテスト{#naming-conventions-for-assets-testing}

リポジトリーのノードは、[Java コンテンツリポジトリー](/help/sites-developing/the-basics.md#java-content-repository)の命名規則の対象です。ただし、アセットノード名には Adobe Experience Manager によって追加の規則が課せられます。

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
