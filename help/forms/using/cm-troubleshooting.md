---
title: Correspondence Management：トラブルシューティング
description: AEM Forms 環境でレターの保存時に発生するエラーを処理する方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 57794b13-471b-4aae-aa57-ddfc2dfc58c9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 100%

---

# Correspondence Management：トラブルシューティング {#correspondence-management-troubleshooting}

## レターの保存時にエラーが発生する {#errors-when-saving-a-letter}

### 問題 {#issue}

レターの保存時に、次のいずれかのエラーが表示されます。

* テキストモジュールにデータバインディングが存在しない
* 次の項目に必要なプロパティ情報を指定します

### 理由 {#reason}

このエラーは次のいずれかの理由で発生します。

* データ辞書はレターにバインドされているが、サーバー上には存在していない。
* データ辞書はレターにバインドされているが、名前にアンダースコア（_）が含まれている。

### 対処方法 {#workaround}

レターで使用しているデータ辞書がサーバー上に存在しており、名前にアンダースコア（_）が含まれていないことを確認してください。

## レターのプレビュー時にエラーが発生する {#error-when-previewing-a-letter}

### 問題 {#issue-1}

レターをプレビューしている間、レターに含まれる未公開のテキストアセットが公開されていても、「レターの読み込み中のエラー：XML 入力からアセットを読み込めませんでした」というエラーが表示される。

### 対処方法 {#workaround-1}

次の手順を使用してパブリッシュインスタンスのレター キャッシュをリセットし、レターの表示を再試行します。

1. **`https://'[server]:[port]'/[contextPath]/system/console/configMgr`** に移動して管理者としてログインします。
1. 「**Correspondence Management の設定**」を選択します。
1. 「**Correspondence Management の設定**」で、「**レターのキャッシュを有効にする**」を無効にして「**保存**」をクリックします。
1. 「**レターのキャッシュを有効にする**」をオンにし、「**保存**」をクリックします。
1. レターの表示を再試行します。
