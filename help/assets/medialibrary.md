---
title: 基本的なデジタルアセット管理での Media Library の使用
description: '[!DNL Experience Manager Assets] とアセット管理用の Media Library。'
contentOwner: AG
role: Architect, Leader
feature: Asset Management
hide: true
solution: Experience Manager, Experience Manager Assets
exl-id: 50a980e5-3b35-4485-9a5b-44d1a42a837c
source-git-commit: 51f6da4da0bb3f79aa6fa17371b8084b72de7546
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 99%

---

# 基本的なアセット管理での Media Library の使用 {#manage-assets-using-media-library}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/medialibrary.html?lang=ja) |
| AEM 6.5 | この記事 |

[!DNL Adobe Experience Manager] プラットフォームには、アセットを管理するための様々な機能が用意されています。Media Library を使用すると、少数のアセットをリポジトリにアップロードし、Web ページで検索して使用し、アセットに対して簡単なアセット管理タスクを実行できます。

Media Library は、[!DNL Adobe Experience Manager Sites] ライセンスを補完する軽量のデジタルアセット管理（DAM）ソリューションです。[!DNL Sites] は、Web コンテンツ管理（WCM）ソリューションです。Media Library は、Experience Manager のすべての機能と連携します。

[!DNL Adobe Experience Manager Assets] ライセンスは別途購入可能です。[!DNL Experience Manager Assets] では、エンタープライズのユースケースを介したアセットの堅牢な処理、メタデータ、スキーマ、検索、ユーザーインターフェイスのカスタマイズなど、Media Library が提供する機能以外の様々な機能を利用できます。

## ライセンス要件 {#avail-media-library-license}

[!DNL Sites] ライセンスがあれば、Media Library を使用することができます。[!DNL Experience Manager] のすべてのコンポーネントで機能します。

Media Library は Sites の一部としてインストールされます。Sites のライセンスとインストール以外に、追加のライセンスやパッケージは必要ありません。

## [!DNL Assets] と Media Library {#assets-and-media-library}

Experience Manager Assets は、エンタープライズグレードの DAM 機能を提供します。Assets の機能は、[!DNL Experience Manager] と共に 1 つのパッケージで提供されます。ただし、Assets ライセンスを購入していないユーザーは、高度な DAM 機能を使用する権利はありません。Assets ライセンスがない場合、[Media Library 機能](#use-media-library)のみ使用できます。

ライセンスを所有していない [!DNL Assets] 機能を意図せずに使用することを防ぐには、[!DNL Assets] 固有のワークフロー、コンポーネント、分類、オプションおよび [!DNL Assets] 管理を [!DNL Experience Manager] からすべて削除します。これによって、ユーザーがライセンスのない [!DNL Assets] の機能を誤って使用することを防ぐことができます。

## Media Library の使用 {#use-media-library}

Media Library には、次の使用例に対する基本的な DAM 機能が用意されています。

* [!DNL Adobe Experience Manager Sites] を使用して作成された web ページ。
* [!DNL Adobe Experience Manager Forms] を使用して作成されたアダプティブフォームと通信
* [!DNL Adobe Experience Manager Screens] を使用して作成されたデジタルスクリーンエクスペリエンス
* ヘッドレス操作用の [!DNL Assets] HTTP REST API

<!--
 TBD: Remove this after confirmation. May need to merge this list with the list provided by PMs.
* Static renditions

-->

Media Library 機能を使用するには、デフォルトの [!DNL Experience Manager] ユーザーインターフェイスを使用できます。Media Library は [!DNL Experience Manager Sites] インストールに含まれており、別のインターフェイスやアドオンは必要ありません。Media Library ユーザーは、既存のインターフェイスを使用して、次のタスクを実行できます。

* アセットを整理するフォルダーの作成
* アセットのアップロード
* アセットの公開
* アセットの編集、移動、およびコピー
* アセットの参照、フィルタリング、および検索（類似性検索を含む）
* メタデータフィールドの値の追加および編集（デフォルトでは、アセットの[!UICONTROL プロパティ]ページの「[!UICONTROL 基本]」タブで使用できる「スマートタグ」フィールドを除く）
* 静的レンディションの追加および削除
* フォルダー、アセット、アセットレンディションのダウンロード
* アセットバージョンの作成
* アセットに対するレビュータスクの作成および実行
* アセットへの注釈を付け
* コンテンツファインダーを使用した [!DNL Sites] ページへのアセットの追加
* [!DNL Content Fragments] の使用
* [!DNL Content Fragments] と参照先のメディアアセットに対する HTTP REST および GraphQL API の使用（Sites ライセンスの下で）
* Experience Cloud との統合
* アセット管理ユーザーインターフェイスのカスタマイズと拡張
* クエリビルダー（API）にアクセスして検索機能を拡張
* 静的タグの作成
* プロジェクトとタスクのオーサリング
* アクティビティストリーム（タイムライン）
* コメントと注釈

<!-- TBD: Define exactly which basic Assets workflow are available for use with Media Library?

As per PM, we must avoid stating such a list, as we do not have a list that makes sense in Cloud Service.
-->

>[!IMPORTANT]
>
>DAM の高度なユースケースの多くは、[!DNL Experience Manager Assets] で処理されます。Media Library ライセンスでは、Media Library を使用して、記載されているユースケースのみを実行することができます。ユースケースがリストに表示されていない場合は、Media Library ライセンスで使用しないでください。質問がある場合は、アドビカスタマーサポートまで問い合わせください。

なお、[!DNL Assets] ライセンスがなければ、スマートタグ、[!DNL Asset] リンク、[!DNL Asset] セレクター、一括タグ付け、アセットワークフローの変更、Media Library にアクセスするための標準 [!DNL Adobe Experience Manager] ユーザーインターフェイスは使用できません。

<!-- TBD: Add a CTA - how to contact Adobe for queries. -->

>[!MORELIKETHIS]
>
>* [ [!DNL Experience Manager Assets] の DAM 機能](https://experienceleague.adobe.com/ja/docs/experience-manager-65-lts/content/assets/assets)
>* [[!DNL Experience Manager] 6.5 Managed Services 製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-managed-services.html)
>* [[!DNL Experience Manager] 6.5 オンプレミス製品の説明](https://helpx.adobe.com/jp/legal/product-descriptions/adobe-experience-manager-on-premise.html)
