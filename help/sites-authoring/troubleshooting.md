---
title: AEM でのオーサリング時のトラブルシューティング
description: AEM の使用時に発生する可能性のある問題をいくつか紹介します。
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
exl-id: 1e735d57-834a-4251-9b92-ccc6d4712f2a
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 100%

---

# オーサリング時の AEM のトラブルシューティング {#troubleshooting-aem-when-authoring}

ここでは、AEM の使用時に発生する可能性のあるいくつかの問題を取り上げます。また、それらのトラブルシューティング方法に関する推奨事項についても説明します。

>[!NOTE]
>
>問題が発生した場合は、お使いのインスタンス（リリースおよびサービスパック）に関する[既知の問題](/help/release-notes/release-notes.md)の一覧を確認すると役に立ちます。

>[!NOTE]
>
>管理者権限を持ち AEM の問題をトラブルシューティングするユーザーは、[AEM のトラブルシューティング（管理者向け）](/help/sites-administering/troubleshoot.md)に記載されたトラブルシューティング方法を使用できます。十分な権限がない場合は、AEM のトラブルシューティングに関してシステム管理者にお問い合わせください。

## 公開されたサイト上に古いバージョンのページがまだある {#old-page-version-still-on-published-site}

* **問題**：

   * ページに変更を加えてそのページを公開サイトにレプリケートしましたが、公開サイトでは古いバージョンのページが依然として表示されます&#x200B;*。*

* **理由**:

   * いくつかの原因が考えられます。キャッシュ（ローカルブラウザーまたは Dispatcher のキャッシュ）が原因である場合がほとんどですが、レプリケーションキューに問題がある場合もあります。

* **ソリューション**:

   * これには、様々な原因が考えられます。
   * ページが正しくレプリケートされていることを確認します。ページのステータスと、必要に応じてレプリケーションキューの状態をチェックします。
   * ローカルブラウザーのキャッシュをクリアして、ページに再度アクセスします。
   * ページ URL の末尾に `?` を追加します。以下に例を示します。

      * `http://localhost:4502/sites.html/content?`
      *  これによって、ページが AEM から直接リクエストされ、Dispatcher がスキップされます。更新されたページを受け取った場合、Dispatcher のキャッシュをクリアする必要があることを表しています。

   * システム管理者に問い合わせて、レプリケーションキューに問題があることを伝えます。

## コンポーネントのアクションがツールバーに表示されない {#component-actions-not-visible-on-toolbar}

* **問題**：

   * オーサー環境でのコンテンツページの編集中に、使用可能なすべてのコンポーネントのアクションが表示されません。

* **理由**:

   * まれに、前のアクションがツールバーに影響を及ぼすことがあります。

* **解決策**:

   * ページを更新します。
