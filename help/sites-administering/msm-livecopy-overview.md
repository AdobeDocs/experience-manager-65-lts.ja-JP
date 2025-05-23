---
title: ライブコピーの概要コンソール
description: ライブコピーの概要コンソールの基本について説明します。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
feature: Multi Site Manager
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: ddd50c64-0f17-4638-a57e-17ededaca27b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 100%

---

# ライブコピーの概要コンソール{#live-copy-overview-console}

**ライブコピーの概要**&#x200B;では、次のことが可能です。

* サイト全体での継承の表示／管理：

   * ブループリントツリーと対応するライブコピー構造およびそれらの継承ステータスを表示
   * 継承ステータス（休止、再開など）を変更
   * ブループリントおよびライブコピープロパティを表示

* ロールアウトアクションの実行

## ライブコピーの概要を開く {#opening-the-live-copy-overview}

ライブコピーの概要は、以下から開くことができます。

* [ブループリントページの参照サイドパネル（Sites コンソール）](#opening-live-copy-overview-references-for-a-blueprint-page)
* [ブループリントページのプロパティ](#opening-live-copy-overview-properties-of-a-blueprint-page)

### ライブコピーの概要を開く - ブループリントページの参照 {#opening-live-copy-overview-references-for-a-blueprint-page}

「**ライブコピーの概要**」は、**Sites** コンソールの&#x200B;**参照**&#x200B;サイドパネルから開くことができます。

1. **Sites** コンソールで、[ブループリントページに移動して選択](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)します。
1. **[参照](/help/sites-authoring/basic-handling.md#references)**&#x200B;パネルを開き、「**ライブコピー**」を選択します。

   ![参照パネル - ライブコピー](assets/chlimage_1-359.png)

   >[!NOTE]
   >
   >また、先に参照を開いてからブループリントを選択することもできます。

1. 「**ライブコピーの概要**」を選択して、選択したブループリントに関連するすべてのライブコピーの概要を表示および使用します。
1. 「**閉じる**」を使用して終了し、**Sites** コンソールに戻ります。

### ライブコピーの概要を開く - ブループリントページのプロパティ {#opening-live-copy-overview-properties-of-a-blueprint-page}

**ライブコピーの概要**&#x200B;は、ブループリントページのプロパティを表示する際に開くことができます。

1. 該当するブループリントページの&#x200B;**プロパティ**&#x200B;を開きます。
1. 「**ブループリント**」タブを開きます。「**ライブコピーの概要**」オプションが上部のツールバーに表示されます。

   ![「ブループリント」タブ - ライブコピーの概要](assets/chlimage_1-360.png)

1. 「**ライブコピーの概要**」を選択して、現在のブループリントに関連するすべてのライブコピーの概要を表示および使用します。

1. 「**閉じる**」を使用して終了し、**Sites** コンソールに戻ります。

## ライブコピーの概要の使用 {#using-the-live-copy-overview}

**ライブコピーの概要**&#x200B;を使用して、ライブコピーに対してアクションを実行することもできます。

1. **ライブコピーの概要**&#x200B;を開きます。
1. 必要なブループリントページまたはライブコピーページを選択します。ツールバーが更新されて、使用できるアクションが表示されます。使用できる[アクション](/help/sites-administering/msm.md#terms-used)は、[ブループリント](#actions-for-a-blueprint-page)ページまたは[ライブコピー](#actions-for-a-live-copy-page)ページのどちらを選択したかによって異なります。

### ブループリントページのアクション {#actions-for-a-blueprint-page}

ブループリントページを選択した場合は、以下のアクションを使用できます。

![ブループリントを選択した場合に使用可能なアクション](assets/chlimage_1-361.png)

* 編集

   * ブループリントページを編集用に開きます。

* [ロールアウト](/help/sites-administering/msm.md#rollout-and-synchronize)

   * ロールアウトを実行して、ソースからライブコピーに変更をプッシュします。

### ライブコピーページのアクション {#actions-for-a-live-copy-page}

ライブコピーページを選択した場合は、以下のアクションを使用できます。

![ライブコピーページを選択した場合に使用可能なアクション](assets/chlimage_1-362.png)

* 編集

   * ライブコピーページを編集用に開きます。

* [関係ステータス](#relationship-status)

   * ステータスおよび継承に関する情報を表示します。

* [同期](/help/sites-administering/msm.md#rollout-and-synchronize)

   * ライブコピーを同期して、ソースからライブコピーに変更内容をプルします。

* [リセット](/help/sites-administering/msm-livecopy.md#resetting-a-live-copy-page)

   * ライブコピーページをリセットして、すべての継承のキャンセルを削除し、ソースページと同じ状態にページを戻します。

* [休止](/help/sites-administering/msm.md#suspending-and-cancelling-inheritance-and-synchronization)

   * ライブコピーとそのブループリントページの間のライブ関係を一時的にアクティベート解除します。

* [再開](/help/sites-administering/msm-livecopy.md#resuming-inheritance-for-a-page)

   * 再開すると、休止状態の関係を復帰できます。

* [分離](/help/sites-administering/msm.md#detaching-a-live-copy)

   * ライブコピーとそのブループリントページの間のライブ関係を永続的に削除します。

## 関係ステータス {#relationship-status}

**関係ステータス**&#x200B;コンソールには、様々な機能を提供する 2 つのタブがあります。

* [関係ステータス情報](#relationship-status-information)
* [ライブコピー情報](#live-copy-information)

### 関係ステータス情報 {#relationship-status-information}

このタブには、ブループリントとライブコピーの関係のステータスに関する詳細情報が表示されます。

![関係のステータスに関する情報](assets/chlimage_1-363.png)

### ライブコピー情報 {#live-copy-information}

このタブでは、ライブコピー設定を表示および編集できます。

![ライブコピー情報](assets/chlimage_1-364.png)
