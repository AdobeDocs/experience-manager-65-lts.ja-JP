---
title: 集計した使用状況の統計の収集をオプトインする方法
description: 集計した使用状況の統計をオプトインする方法について説明します。
contentOwner: raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 410691eb-27a9-4f8e-b926-01027c7f84d4
source-git-commit: cc96a14ebaf9f895a798b5f4904f5b4769b990bb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 58%

---

# 集計された使用統計の収集をオプトイン{#opting-into-aggregated-usage-statistics-collection}

## はじめに {#introduction}

Adobe Experience Manager（AEM）とのやり取りに関する Adobe 統計を送信することで、Adobe Experience Cloud の改善に役立てることができます。 この情報には会社のサイト訪問者に関するデータは含まれておらず、アドビがユーザーエクスペリエンスを提供、サポート、改善するためにのみ使用されます。

使用状況の統計の収集をオプトインするには、タッチ UI または web コンソールを使用します。

>[!NOTE]
>
>GDPR や CCPA など、様々なデータ保護およびプライバシー規制があります。 AEM Sites では、データ保護やプライバシーコンプライアンスに関する義務をお客様が果たすのを支援する準備が整っています。 このページでは、集計された使用状況の統計情報コレクションをオプトイン（またはオプトアウト）する手順について説明します。
>
>詳しくは、[アドビのプライバシーセンター](https://www.adobe.com/jp/privacy.html)も参照してください。

>[!NOTE]
>
>[Web コンソール ] （/help/sites-deploying/opt-in-aggregated-usage-statistics.md#opt-in-by-using-the-web-consoleを使用するか、AEM オプトイン画面でオプトインオプションを選択しないことで、いつでもオプトアウトできます。

## タッチ UIを使用したオプトイン {#opt-in-by-using-the-touch-ui}

AEMを初めて起動する場合は、次のようにタッチ UIを使用してオプトインできます。

1. AEM ナビゲーション画面で、**インボックス**（ベル）アイコンをクリックします。

   ![usage_statisticsnavigationscreen](assets/usage_statisticsnavigationscreen.png)

1. ドロップダウンリストで、**集計された使用状況の統計コレクションを有効にする**&#x200B;をクリックします。

   ![usage_statisticsnavigationscreen2](assets/usage_statisticsnavigationscreen2.png)

1. オプトイン画面で、「**[!UICONTROL 集計された使用統計の収集を許可する]**」オプションをクリックします。

   ![usage_statisticsopt-inscreen](assets/usage_statisticsopt-inscreen.png)

1. 「**完了**」をクリックします。

## Web コンソールを使用したオプトイン {#opt-in-by-using-the-web-console}

Web コンソールを使用して、次のようにオプトイン（またはオプトアウト）できます。

1. AEM ナビゲーション画面で、**ツール**／**操作** の順にクリックします。

   ![usage_statisticsopsdashboard](assets/usage_statisticsopsdashboard.png)

1. 操作ウィンドウで「**Web コンソール**」をクリックします。

   ![usage_statisticswebconsole](assets/usage_statisticswebconsole.png)

1. **集計された使用状況の統計コレクション**&#x200B;を検索します。
1. **編集**&#x200B;アイコンをクリックします。

   ![usage_statisticscollectedit](assets/usage_statisticscollectionedit.png)

1. 「**Enabled**」チェックボックスをオンにします。 または、使用状況の統計の収集をオプトアウトする場合は、このチェックボックスをオフにします。

   ![usage_statisticsselect](assets/usage_statisticsselect.png)

1. 「**保存**」をクリックします。
