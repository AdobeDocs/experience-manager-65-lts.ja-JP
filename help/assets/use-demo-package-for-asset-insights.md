---
title: アセットインサイトにデモパッケージを使用
description: デモパッケージを使用して、アセットインサイトで web ページからデータを取得し、web ページのインサイトを生成できるようにします。
contentOwner: AG
role: User, Admin
feature: Asset Insights,Asset Reports
solution: Experience Manager, Experience Manager Assets
exl-id: 12f457e4-f5d7-47cb-b38a-9d63e7c19475
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 100%

---

# アセットインサイトにデモパッケージを使用 {#using-demo-package-for-asset-insights}

デモパッケージを使用して、アセットインサイトでサンプル web ページからデータを取得し、サンプル web ページのインサイトを生成できるようにします。

## [!DNL Use Experience Manager Assets] サンプル web ページを使用したインサイト  {#using-aem-assets-insights-with-sample-web-page}

1. [アセットインサイトの設定](configure-asset-insights.md)の手順を使用してアセットインサイトを設定します。
1. 次に示すサンプル Assets パッケージをダウンロードして、CRXDE パッケージマネージャーでインストールします。

[ファイルを入手](assets/insightsdemo.zip)

1. 次に示すサンプル web ページを含む ZIP ファイルをダウンロードして、ローカルファイルシステムに抽出します。

[ファイルを入手](assets/demosite.zip)

1. Web ブラウザーで開く Web ページをクリックします。

   >[!CAUTION]
   >
   >Web ページは localhost のサーバーからアセットを読み込むように設定されます。サーバーが別の場所で実行している場合は、localhost のサーバーアドレスを web ページの HTML コンテンツのサーバーアドレスに変更してください。

   >[!NOTE]
   >
   >外部の web ページは、[!DNL Experience Manager] 自体でホストされたものでもかまいません。
