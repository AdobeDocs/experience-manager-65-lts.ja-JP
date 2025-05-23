---
title: Java コンテンツリポジトリのノードの命名規則
description: リポジトリのノードは、Java コンテンツリポジトリーの命名規則の対象です
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 36025dac-890e-45ba-adea-a230a5231a0b
source-git-commit: a869ffbc6015fd230285838d260434d9c0ffbcb0
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 99%

---

# 命名規則 {#naming-conventions}

リポジトリのノードは、[Java コンテンツリポジトリ](/help/sites-developing/the-basics.md#java-content-repository)の命名規則の対象です。ただし、AEM によってページノード名に追加の規則が課せられます。

## ページの命名規則 {#naming-conventions-for-pages}

これらの命名規則は、以下のような様々なレベルで実装されます。

* JcrUtil：[JCR ユーティリティ](#jcr-utilities)の AEM 実装。
* ページマネージャー：[ページマネージャー](#page-manager)は、ページレベルの操作用のメソッドを提供します。
* 使用する UI：

   * [標準のタッチ操作対応 UI](#standard-ui)
   * [クラシック UI](#classic-ui)

### JCR ユーティリティ {#jcr-utilities}

[JcrUtil](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) は JCR ユーティリティの AEM 実装です。名前の検証では特に、制御する文字マッピングおよび次の点が確認されます。

* `isValidName`

   * 名前が空でなく、有効な文字のみが含まれるかどうかを確認します。
   * 推奨される名前が有効かどうかを確認するのに使用できます。

* `createValidName`

   * 任意の文字列から有効なラベルを作成します。
   * タイトルから名前を作成するのに使用できます。

### ページマネージャー {#page-manager}

[ページマネージャー](https://developer.adobe.com/experience-manager/reference-materials/6-5-lts/javadoc/com/day/cq/wcm/api/PageManager.html)は、[JCRUtil](#jcr-utilities) に基づいて、ページレベル操作用のメソッドを提供します。

### 標準 UI {#standard-ui}

標準のタッチ操作対応 UI：

* 次のいずれかの場合、ページマネージャーによって課せられる制約に従って名前が確認されます。

   * ノード名に変換されるようにページタイトルが提供されている。
   * 明示的なノード名が提供されている。

### クラシック UI {#classic-ui}

クラシック UI にはさらに厳しい制約があります。

* 名前が有効と判断されるのは、明示的なノード名が次のいずれかの場合です。

   * ノード名に変換されるようにページタイトルが提供されている。
   * 明示的なノード名が提供されている。

* 有効な文字（`PageManagerImpl` によって他の文字の使用が許可されていても、クラシック UI でページを作成する場合は、次の文字のみが有効です）。

   * a～z
   * A～Z
   * 0～9
   * _（アンダースコア）
   * `-`（ダッシュ／マイナス）
