---
title: フォームのプレビュー
description: 公開またはアクティベートする前にフォームをプレビューして、期待どおりになっていることを確認します。プレビューのオプションは、サポートされているフォームタイプにより異なる場合があります。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 377d804d-4a75-4c93-8125-d2660cf56418
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 8afc775f-2178-4acc-afb7-718970c435b4
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 100%

---

# フォームのプレビュー {#previewing-a-form}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

## 概要 {#overview}

AEM Forms では、リポジトリ内にあるフォームやドキュメントをプレビューできます。プレビューを使用すると、フォームがエンドユーザーにリリースされる際にどのように表示され、動作するかを明確に理解できます。

フォームをプレビューすると、フォームはインタラクティブインターフェイスでレンダリングされ、ユーザーはフォームにデータを入力できます。ドキュメントをプレビューすると、ドキュメントは非インタラクティブモードでレンダリングされ、ユーザーはドキュメントの表示のみが可能です。フォームの場合、カスタムプレビューの追加オプションが使用できます。このオプションを使用すると、XML ファイルのデータを使用してフォームをプレビューできます。プレビューしているフォームのフィールドの一部またはすべてにデータが入力されます。

次の表に、サポートされているフォームのタイプごとに使用できるプレビューオプションを示します。

<table>
 <tbody>
  <tr>
   <td><strong>アセットタイプ</strong><br /> </td>
   <td><strong>使用できるプレビューオプション</strong><br /> </td>
  </tr>
  <tr>
   <td>ドキュメント</td>
   <td>PDF プレビュー</td>
  </tr>
  <tr>
   <td>PDF フォーム</td>
   <td>PDF プレビューとデータを使用したプレビュー<br /> </td>
  </tr>
  <tr>
   <td>アダプティブフォーム</td>
   <td>HTML プレビューとデータを使用した HTML プレビュー</td>
  </tr>
  <tr>
   <td>フォームテンプレート</td>
   <td>PDF プレビュー、データを使用した PDF プレビュー、HTML プレビュー、データを使用した HTML プレビュー<br /> </td>
  </tr>
 </tbody>
</table>

## フォームのプレビュー {#previewing-a-form-1}

1. プレビューするアセットを選択し、アクションツールバーのプレビュー ![aem6forms_preview](assets/aem6forms_preview.png) をクリックします。

   >[!NOTE]
   >
   >アセットを選択するには、デフォルトのカード表示をリスト表示に切り替えます。![aem6forms_viewlist](assets/aem6forms_viewlist.png) または ![aem6forms_viewcard](assets/aem6forms_viewcard.png) をクリックして、表示を切り替えます。

1. 「プレビュー」をクリックすると、選択されているアセットタイプで適用できるプレビューオプションが表示されます。必要なオプションをクリックして、選択したアセットを新しいタブでレンダリングします。

   以下のオプションがあります。

   * HTML としてプレビュー
   * データを使用したプレビュー
   * PDF としてプレビュー（フォームテンプレートから選択可能）

## データを使用してプレビュー {#preview-with-data}

「**データを使用したプレビュー**」を選択すると、実際のデータが入力された状態でフォームの様子を見ることができます。データを使用したプレビューオプションでは、サンプルユーザーデータを含めた XML をアップロードできます。サンプルユーザーデータを使用して、選択した形式でプレビューフォームに入力します。

1. アセットを選択し、プレビュー ![aem6forms_preview](assets/aem6forms_preview.png) をクリックし、「**データを使用してプレビュー**」を選択します。
1. フォームのプレビューダイアログで、FormData を XML ファイルとして指定します。「プレビュー」をクリックして、XML からのマージされたデータとフォームをレンダリングします。
