---
title: アクセス可能な複雑なテーブルを HTML5 フォームで作成する
description: アクセス可能なテーブルを HTML5 フォームで作成する方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 3504afe1-abf5-4fbf-a0d2-e093361764bd
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: e6e6c08a-3bed-4713-a0e0-2a02607c7fc7
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 100%

---

# アクセス可能な複雑なテーブルを HTML5 フォームで作成する {#create-accessible-complex-tables-in-html-forms}

HTML5 フォームでのテーブルのデフォルト実装では、テーブルのレンダリングに HTML DIV 要素が使用されます。さらに、アクセシビリティ要件を満たす目的で ARIA ロールも使用されます。

ARIA ロールとデータテーブルの組み合わせを完全にはサポートしていないスクリーンリーダーでアクセシビリティの問題が発生するのを防ぐには、HTML5 フォームでテーブル用の代替レンディションを使用します。これらのテーブルは、Designer で導入された新しいテーブル形式に基づいており、次の項目もサポートしています。

* 行ヘッダー
* 行幅

HTML5 フォームで新しい形式を使用するには、テーブルを複雑なテーブルとしてマークする必要があります。複雑なテーブルとしてマークするには、テーブルのサブフォームの XML ソースに `extras` タグを次のように追加します。

```xml
</extras>
 <text name="complexTable">1</text>
 </extras>
```

*complexTable* としてマークされたテーブルはネイティブの HTML レンディションに従うため、特定のスクリーンリーダーのアクセシビリティの範囲が拡大します。行幅を作成するには、テーブル内の 1 つの列で連続する複数のセルを選択し、選択範囲を右クリックして、「**[!UICONTROL セルの結合]**」をクリックします。

>[!NOTE]
>
>行幅の作成は一番左のセルでのみ機能します。

行を行ヘッダーとしてマークするには、その行のすべてのセルを選択し、選択範囲を右クリックして、「**[!UICONTROL ヘッダーをマーク]**」をクリックします。

セルを列ヘッダーとしてマークするには、その列内の任意のセルを選択し、選択範囲を右クリックして、「**[!UICONTROL ヘッダーをマーク]**」をクリックします。

新しい *AccessibleTable* 形式には次の制限事項があります。

* テーブルに行幅を設定する場合は、拡大可能なフィールドを使用できない
* ネストされたテーブル（テーブルのセルに含まれている別のテーブル）は使用できない
* 行幅はヘッダー行とヘッダーセルのみに適用できる
* 使用可能なテーブルは標準テーブルのみである
* 行幅が 1 を超えるテーブルではデータを事前入力できない
