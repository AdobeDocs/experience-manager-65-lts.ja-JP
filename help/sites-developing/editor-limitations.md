---
title: エディターの制限事項
description: タッチ操作対応 UI のエディターでは、オーバーレイを使用して iframe 内に含まれるコンテンツを操作します。この操作には、エディターの使用と開発者に対していくつかの制限事項があります。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 9f66c1c5-0fe7-47be-ad78-ef4548e4e26b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 100%

---

# エディターの制限事項{#editor-limitations}

タッチ操作対応 UI のエディターでは、オーバーレイを使用して iframe 内に含まれるコンテンツを操作します。この操作には、エディターの使用と開発者に対していくつかの制限事項があります。このページでは、これらの制限事項をまとめ、可能な限り解決策や回避策を提供します。

## 機能の制限事項 {#functional-limitations}

作成者は、エディターを使用してページを作成する際に、次の機能上の制限を受ける場合があります。

### リンクがアクティブにならない {#links-not-active}

[ページの編集](/help/sites-authoring/editing-content.md)時に、リンクがアクティブになりません。

* [コンテンツ内のリンクを使用して移動するには、**プレビュー**&#x200B;モード](/help/sites-authoring/editing-content.md#preview-mode)に切り替えます。

### 構造ページ {#structure-pages}

ページに `structure` という名前を付けることはできません。`structure` と名前が付けられたページは、ページエディターで編集できません。

## CSS の制限 {#css-limitations}

開発者は、エディターでの CSS の操作に次の制限を受ける場合があります。

### 要素が絶対配置される {#absolutely-positioned-elements}

絶対配置された要素により、そのオーバーレイの位置に問題が生じる可能性があります。

* この場合、エディターはまったく同じ寸法のオーバーレイを作成するので、絶対配置された要素の寸法が正しいことを確認します。

### vh 単位 {#vh-units}

iframe の高さは Adobe Experience Manager（AEM）によって自動調整されるので、`vh` 単位はサポートされません。

### 固定の背景画像 {#fixed-background-images}

固定の背景画像は、iframe 内に埋め込まれるので、スクロール時に固定されているように表示されない可能性があります。

* ヘッダーバーのアクションで「**公開済みとしてページを表示**」を選択すると、ページが正しく表示されます。

### 100 ％の高さ {#height}

ページの body 要素では、100 ％の高さはサポートされていません。

* フルスクリーンの body を実装するには、次のように body 要素を「拡張」することで、回避することが可能です。

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### 余白の折りたたみ {#margin-collapsing}

余白の折りたたみの問題は、body 要素の最初の子要素に余白がある場合に発生することがあります。

* 解決策として、次のように body 要素レベルに clearfix を追加します。

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```
