---
title: 通信作成用ソリューションのカスタムポータルとの統合
description: 通信の作成 UI とカスタムポータルを統合する方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 496b125b-b091-4843-ba9f-2479dbeba07b
source-git-commit: 16f57ae1663f035d1dc39005d37426c7a0d8dc16
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 46%

---

# `Create Correspondence` ソリューションとカスタムポータルの統合{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概要 {#overview}

この記事では、`Create Correspondence` ソリューションをお使いの環境と統合する方法について詳しく説明します。

## URL ベースの呼び出し {#url-based-invocation}

カスタムポータルから `Create Correspondence` アプリケーションを呼び出す 1 つの方法は、次のリクエストパラメーターを含む URL を準備することです。

* 文字テンプレートの識別子（cmLetterId パラメーターを使用）。

* 目的のデータソースから取得した XML データの URL（cmDataUrl パラメーターを使用）。

例えば、カスタムポータルは、次のような URL を準備します\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`（ポータル上のリンクからの href にすることができます）。

>[!NOTE]
>
>この呼び出し方法は安全ではありません。必要なパラメーターが URL に明示される GET リクエストとして渡されるからです。

>[!NOTE]
>
>`Create Correspondence` アプリケーションを呼び出す前に、データを保存してアップロードし、指定された dataURL で `Create Correspondence` UI を呼び出します。 このプロセスは、カスタムポータル自体から、または別のバックエンドプロセスを通じて実行できます。

## インラインデータベースの呼び出し {#inline-data-based-invocation}

`Create Correspondence` アプリケーションを呼び出すもう 1 つの安全な方法は、URL （https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html）に移動することです。 パラメーターとデータを送信しながら、この URL を実行して、`Create Correspondence` アプリケーションを POST リクエストとして呼び出し、エンドユーザーに対して非表示にします。 また、このワークフローでは、`Create Correspondence` アプリケーションの XML データをインラインで（同じリクエストの一部として `cmData` パラメーターを使用して）渡すことができるようになりました。 このワークフローは、以前のアプローチでは不可能または理想的でした。

### レターを指定するパラメーター {#parameters-for-specifying-letter}

| **名前** | **タイプ** | **説明** |
| --- | --- | --- |
| cmLetterInstanceId | 文字列 | レターインスタンスの ID です。 |
| cmLetterId | 文字列 | レターテンプレートの名前です。 |

テーブル中のパラメーターの順序が、レターの読み込みに使用されるパラメーターの優先順位を指定します。

### XML データソースを指定するパラメーター {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td> 
   <td><strong>種類</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>cq、ftp、http、file.<br /> などの基本的なプロトコルを使用するソースファイルの XML データ </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>文字列</td> 
   <td>レターインスタンスで使用可能な xml データを使用します。</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>ブール値</td> 
   <td>データディクショナリに添付されたテストデータを再利用する。</td> 
  </tr>
 </tbody>
</table>

テーブル中のパラメーターの順序が、XML データの読み込みに使用されるパラメーターの優先順位を指定します。

### その他のパラメーター {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>名前</strong></td> 
   <td><strong>種類</strong></td> 
   <td><strong>説明</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>ブール値</td> 
   <td>「True」に設定されている場合、レターをプレビューモードで開きます<br /> </td> 
  </tr>
  <tr>
   <td>ランダム</td> 
   <td>Timestamp</td> 
   <td>ブラウザーのキャッシュに関する問題を解決します。</td> 
  </tr>
 </tbody>
</table>

`cmDataURL` に http または cq プロトコルを使用する場合、`http/cq` の URL には匿名でアクセスできる必要があります。
