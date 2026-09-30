---
title: 通信を作成ソリューションとカスタムポータルの統合
description: 通信の作成 UI とカスタムポータルを統合する方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 496b125b-b091-4843-ba9f-2479dbeba07b
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 47%
---
# カスタムポータルとの`Create Correspondence` ソリューションの統合{#integrating-create-correspondence-ui-with-your-custom-portal}

## 概要 {#overview}

この記事では、`Create Correspondence` ソリューションを環境と統合する方法について詳しく説明します。

## URL ベースの呼び出し {#url-based-invocation}

カスタムポータルから`Create Correspondence` アプリケーションを呼び出す方法の1つは、次のリクエストパラメーターを使用してURLを準備することです。

* 文字テンプレートの識別子（cmLetterId パラメーターを使用）。

* 目的のデータソースから取得した XML データの URL（cmDataUrl パラメーターを使用）。

例えば、カスタムポータルは、次のような URL を準備します\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`（ポータル上のリンクからの href にすることができます）。

>[!NOTE]
>
>この呼び出し方法は安全ではありません。必要なパラメーターが URL に明示される GET リクエストとして渡されるからです。

>[!NOTE]
>
>`Create Correspondence` アプリケーションを呼び出す前に、データを保存してアップロードし、指定されたdataURLで`Create Correspondence` UIを呼び出します。 このプロセスは、カスタムポータル自体から、または別のバックエンドプロセスを通じて実行できます。

## インラインデータベースの呼び出し {#inline-data-based-invocation}

`Create Correspondence` アプリケーションを呼び出すもう1つの、より安全な方法は、URL （https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html）にアクセスすることです。 パラメーターとデータを送信する際にこのURLを実行して、`Create Correspondence` アプリケーションをPOST リクエストとして呼び出し、エンドユーザーから非表示にします。 このワークフローでは、`Create Correspondence` アプリケーションのXML データをインラインで（同じリクエストの一部として、`cmData` パラメーターを使用して）渡せるようになりました。 以前のアプローチでは、このワークフローは不可能であり、理想的でもありませんでした。

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
   <td>cq、ftp、http、fileなどの基本的なプロトコルを使用したソースファイルからのXML データ。<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>文字列</td> 
   <td>レターインスタンスで使用可能なxml データを使用します。</td> 
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
   <td>ブーリアン</td> 
   <td>「True」に設定されている場合、レターをプレビューモードで開きます<br /> </td> 
  </tr>
  <tr>
   <td>ランダム</td> 
   <td>Timestamp</td> 
   <td>ブラウザーのキャッシュに関する問題を解決します。</td> 
  </tr>
 </tbody>
</table>

`cmDataURL`にhttp プロトコルまたはcq プロトコルを使用する場合は、`http/cq`のURLに匿名でアクセスできる必要があります。
