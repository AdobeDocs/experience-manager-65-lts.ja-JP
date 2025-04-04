---
title: インタラクティブ通信の設定プロパティ
description: インタラクティブ通信で使用するデフォルトの設定プロパティの編集
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
docset: aem65
feature: Interactive Communication
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 73e4cd72-0479-4b3c-82d2-653cded590b9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 100%

---

# インタラクティブ通信の設定プロパティ{#interactive-communications-configuration-properties}

インタラクティブ通信には、[AEM Forms アドオン](../../forms/using/installing-configuring-aem-forms-osgi.md)パッケージのインストール後に自動的に設定されるプロパティが含まれています。インタラクティブ通信の作成者は、**Adobe Experience Manager Web コンソール設定**&#x200B;ページを使用して、これらのデフォルトの設定プロパティを編集できます。

次の URL を使用して、**Adobe Experience Manager Web コンソール設定**&#x200B;ページを開きます。

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

設定プロパティには次のものが含まれます。

* [ドキュメントフラグメントの設定](#document-fragments-configuration)
* [通信設定の作成](#create-correspondence-configuration)
* [アダプティブフォームおよびインタラクティブ通信 web チャネルの設定](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [アダプティブフォームおよびインタラクティブ通信 web チャネルテーマの設定](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## ドキュメントフラグメントの設定 {#document-fragments-configuration}

**Adobe Experience Manager web コンソール設定**&#x200B;ページの「**ドキュメントフラグメント設定**」を選択して、ドキュメントフラグメントの設定プロパティを表示します。

<table>
 <tbody> 
  <tr> 
   <td>プロパティ</td> 
   <td>説明</td> 
   <td>デフォルト</td> 
   <td>指定できる値</td> 
  </tr> 
  <tr> 
   <td>データの表示形式</td> 
   <td>印刷チャネルと web チャネル用のインタラクティブ通信を作成する際に使用可能なフィールド、変数、フォームデータモデル要素用のロケール固有の表示形式。</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR, and ja_JP</li> 
     <li>dateFormat = dd-MM-yyyy</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>--</p> </td> 
  </tr> 
  <tr> 
   <td>インデント</td> 
   <td>リストドキュメントフラグメント内のテキストに適用される単一ユニットのインデント幅。</td> 
   <td>12.7mm</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>最小幅のローマ数字</td> 
   <td>リストドキュメントフラグメント内でローマ数字を使用する際に、箇条書きフィールドまたは番号フィールドに適用される最小幅。 </td> 
   <td>12.7mm</td> 
   <td>数値</td> 
  </tr> 
  <tr> 
   <td>最小幅の数値</td> 
   <td>リストドキュメントフラグメント内でローマ数字以外の番号付きリストを使用する際に、箇条書きフィールドまたは番号フィールドに適用される最小幅。</td> 
   <td>8.0mm</td> 
   <td>数値</td> 
  </tr> 
 </tbody> 
</table>

## 通信設定の作成 {#create-correspondence-configuration}

**Adobe Experience Manager web コンソール設定**&#x200B;ページの「**通信の作成設定**」を選択して、エージェント UI の設定プロパティを表示します。

<table>
 <tbody> 
  <tr> 
   <td>プロパティ</td> 
   <td>説明</td> 
   <td>デフォルト</td> 
   <td>指定できる値</td> 
  </tr> 
  <tr> 
   <td>編集用に解決されたコンテンツの表示</td> 
   <td>エージェント UI 上でテキストモジュールを編集する際に、チェックボックスを選択して、解決されたコンテンツ（プレースホルダーではなく実際の値）を表示します。</td> 
   <td>未選択</td> 
   <td>該当なし</td> 
  </tr> 
  <tr> 
   <td>プレビュー中に透かしを適用</td> 
   <td>チェックボックスを選択して、プレビューモードでインタラクティブ通信の印刷チャネルに透かしを適用します。</td> 
   <td>未選択</td> 
   <td>適用なし</td> 
  </tr> 
  <tr> 
   <td>PDF へのフォントの埋め込みを有効化</td> 
   <td><p>チェックボックスを選択すると、PDF ドキュメントへのフォントの埋め込みが有効になります。このオプションを選択すると、エージェント UI を使用して PDF ドキュメントを生成またはプレビューした後、新しいフォントを埋め込むことができます。インタラクティブ通信の印刷チャネルを使用して、PDF ドキュメントを生成およびプレビューします。</p> <p>PDF ドキュメントへのフォントの埋め込みは、あるフォントが、PDF の生成に使用したマシンでは使用でき、PDF にアクセスするクライアントマシンでは使用できない場合に役立ちます。</p> <p>フォントの埋め込みについて詳しくは、<a href="../../forms/using/customize-text-editor.md" target="_blank">テキストエディターのカスタマイズ</a>を参照してください。</p> </td> 
   <td>未選択</td> 
   <td>適用なし</td> 
  </tr> 
 </tbody> 
</table>

## アダプティブフォームおよびインタラクティブ通信 web チャネルの設定 {#adaptive-form-and-interactive-communication-web-channel-configuration}

**Adobe Experience Manager web コンソール設定**&#x200B;ページの「**アダプティブフォームおよびインタラクティブ通信 web チャネルの設定**」を選択して、アダプティブフォームおよびインタラクティブ通信 web チャネルの設定プロパティを表示します。次のテーブルに、インタラクティブ通信に関連するプロパティを示します。

| プロパティ | 説明 | デフォルト | 指定できる値 |
|---|---|---|---|
| プレースホルダーを表示 | チェックボックスを選択して、アダプティブフォームおよびインタラクティブ通信に含まれているフィールドのプレースホルダー表示を有効にします。 | 選択 | 適用なし |
| 最大キャッシュエントリ数 | キャッシュメモリを使用して取得できるアダプティブフォームおよびインタラクティブ通信の最大数を設定します。 | 100 | 数値 |
| 一意のファイル名を作成 | チェックボックスを選択して、アダプティブフォームおよびインタラクティブ通信に添付ファイルとして含まれているファイルに一意の名前を付けます。 | 未選択 | 適用なし |

## アダプティブフォームおよびインタラクティブ通信 web チャネルテーマの設定 {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

**Adobe Experience Manager web コンソール設定**&#x200B;ページの「**アダプティブフォームおよびインタラクティブ通信 web チャネルテーマの設定**」を選択して、アダプティブフォームおよびインタラクティブ通信 web チャネルテーマの設定プロパティを表示します。

<table>
 <tbody> 
  <tr> 
   <td>プロパティ</td> 
   <td>説明</td> 
   <td>デフォルト</td> 
   <td>指定できる値</td> 
  </tr> 
  <tr> 
   <td>フォントリスト名</td> 
   <td>フォントのリストは、アダプティブフォームおよびインタラクティブ通信を作成する際に使用できるようになります。</td> 
   <td><p>Georgia</p> <p>Book Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impact</p> <p>Palatino Linotype</p> </td> 
   <td>すべての有効なアドビサーバーフォント</td> 
  </tr> 
 </tbody> 
</table>
