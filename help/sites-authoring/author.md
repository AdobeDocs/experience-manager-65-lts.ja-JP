---
title: オーサリング
description: Adobe Experience Manager 6.5 でのオーサリングと公開の概念について説明します。
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 314a6c65-9b90-4f4c-9e4a-d551dbb646e9
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 100%

---

# オーサリング{#authoring}

## オーサリング（および公開）の概念 {#concept-of-authoring-and-publishing}

AEM には次の 2 種類の環境があります。

* 作成者
* 公開

これらの環境が相互に影響することで、コンテンツが web サイト上に公開され、訪問者がコンテンツを閲覧できるようになります。

オーサー環境は、コンテンツを作成および更新し、実際にコンテンツを公開する前にレビューするためのメカニズムを提供します。

* 作成者は、コンテンツ（ページ、アセット、パブリケーションなどの様々な種類のコンテンツ）を作成およびレビューします。
* このコンテンツは、ある時点で web サイトに公開されます。

![環境の概要](assets/chlimage_1-132.png)

オーサー環境では、AEM の機能は 2 種類の UI で利用できます。パブリッシュ環境では、ユーザーに公開するインターフェイスの全体的なルックアンドフィールをデザインします。

### オーサー環境 {#author-environment}

作成者は、**オーサー環境**&#x200B;と呼ばれる環境で作業します。この環境では、使いやすいインターフェイス（グラフィカルユーザーインターフェイス（GUI または UI））を使用して、コンテンツを作成できます。この環境は、完全に保護された企業のファイアウォールの内側に配備されるので、作成者は、適切なアクセス権限が割り当てられたアカウントを使用してログインする必要があります。

>[!NOTE]
>
>アカウントには、コンテンツの作成、編集または公開を行う適切なアクセス権が必要です。

使用しているインスタンスや個人のアクセス権の設定に合わせて、コンテンツに対して次のように様々なタスクを実行できます。

* ページに対して新しいコンテンツの生成や既存のコンテンツの編集を行います。
* 事前に定義されたテンプレートを使用して、新しいコンテンツページを作成します。
* アセットやコレクションを作成、編集および管理します。
* パブリケーションを作成、編集および管理します。
* キャンペーンや関連リソースを開発します。
* コンテンツページやアセットなどを移動、コピーまたは削除します。
* ページやアセットなどを公開（または非公開に）します。

さらに、コンテンツの管理に役立つ次のような管理タスクがあります。

* 変更の管理方法を制御するワークフロー（パブリケーション前のレビューの適用など）
* 個々のタスクを調整するプロジェクト

>[!NOTE]
>
>また、AEM は、大部分のタスクについてオーサー環境から[管理](/help/sites-administering/home.md)されます。

#### パブリッシュ環境 {#publish-environment}

準備が完了した AEM サイトのコンテンツは、**パブリッシュ環境**&#x200B;に公開されます。対象となるオーディエンスは、デザインされたインターフェイスのルックアンドフィールに従って web サイトのページを利用できます。

通常、パブリッシュ環境は保護解除された領域（DMZ）内に配置されます。つまり、インターネットで使用できますが、内部ネットワークの完全保護下にはありません。

>[!NOTE]
>
>用語が一部重複して使用されている場合があります。この状況は次の用語で発生しています。
>
>* **公開／非公開**
>  環境でコンテンツを公開する（または非公開にする）アクションに対して主に使用される用語です。
>
>* **アクティブ化／非アクティブ化**
>  公開／非公開と同義です。
>
>* **レプリケート／レプリケーション**
>  これらは、ユーザーコメントの公開やリバースレプリケーションの際などに行われる、ある環境から別の環境へのデータ（ページコンテンツ、ファイル、コード、ユーザーコメントなど）の移動を説明する技術用語です。
>

#### Dispatcher {#dispatcher}

Web サイトの訪問者に対するパフォーマンスを最適化するには、**[Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)** を使用してロードバランシングとキャッシュを実装します。
