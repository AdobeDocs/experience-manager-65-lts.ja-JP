---
title: Adobe Target との統合の前提条件
description: Adobe Target との統合の前提条件について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
exl-id: e1771229-b2ce-406a-95a5-99b11fafbe34
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 63%

---

# Adobe Targetとの統合の前提条件{#prerequisites-for-integrating-with-adobe-target}

[AEM と Adobe Target の統合](/help/sites-administering/target.md)の一環として、Adobe Target を登録し、レプリケーションエージェントを設定して、パブリッシュノードでアクティビティ設定を保護する必要があります。

## Adobe Targetへの登録 {#registering-with-adobe-target}

AEM と Adobe Target を統合するには、有効な Adobe Target アカウントが必要です。このアカウントには、**承認者**&#x200B;レベル以上の権限が必要です。Adobe Target に登録すると、クライアントコードを受け取ります。AEM を Adobe Target に接続するには、クライアントコードおよび Adobe Target のログイン名とパスワードが必要です。

クライアントコードは、Adobe Target サーバーの呼び出し時にAdobe Targetのカスタマーアカウントを識別します。

>[!NOTE]
>
>Target チームが統合を使用するには、お使いのアカウントを有効にする必要があります。
>
>そうでない場合は、[Adobe カスタマーケア](https://experienceleague.adobe.com/en/docs/target/using/cmp-resources-and-contact-information)にご連絡ください。

## Target レプリケーションエージェントの有効化 {#enabling-the-target-replication-agent}

Test &amp; Target [レプリケーションエージェント](/help/sites-deploying/replication.md)をオーサーインスタンス上で有効にする必要があります。AEM のインストールに [nosamplecontent](/help/sites-deploying/configure-runmodes.md#using-samplecontent-and-nosamplecontent) 実行モードを使用した場合、このレプリケーションエージェントはデフォルトでは有効になっていません。本番環境の保護に関する情報については、[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。

1. AEM のホームページで、**ツール**／**デプロイメント**／**レプリケーション**&#x200B;をクリックします。
1. 「**作成者のエージェント**」をクリックします。
1. **Test &amp; Target** レプリケーションエージェントをクリックして、「**編集**」をクリックします。
1. 「有効」オプションをオンにして、「**OK**」をクリックします。

   >[!NOTE]
   >
   >Test &amp; Target レプリケーションエージェントを設定する際、「**トランスポート**」タブでは、URI はデフォルトで `tnt:///` に設定されます。 この URI を `https://admin.testandtarget.omniture.com` に置き換えないでください。
   >
   >`tnt:///` を使用して接続をテストしようとすると、期待される動作であるエラーが表示されます。 URI が内部でのみ使用されるからです。 **接続をテスト** では使用しないでください。

## アクティビティ設定ノードの保護 {#securing-the-activity-settings-node}

通常のユーザーがアクセスできないように、パブリッシュインスタンス上のアクティビティ設定ノード **cq:ActivitySettings** を保護します。 アクティビティ設定ノードには、Adobe Target へのアクティビティの同期を処理するサービスのみがアクセスできるようにしてください。

**cq:ActivitySettings** ノードは、CRXDE Liteのアクティビティ `/content/campaigns/*nameofbrand*` ノードの `jcr:content`* *の下にあります。 （例：`/content/campaign/we-retail/master/myactivity/jcr:content/cq:ActivitySettings`）。このノードは、コンポーネントのターゲティング後にのみ作成されます。

アクティビティの **の下にある:ActivitySettings** cq`jcr:content` ノードは、次の ACL によって保護されています。

* 全員にすべてを拒否します。
* `jcr:read,rep:write` に `target-activity-authors` を許可します（作成者は、標準でこのグループのメンバーです）。
* `jcr:read,rep:write` に `targetservice` を許可します。

これらの設定により、権限を持たないユーザーがノードプロパティにアクセスできなくなります。オーサーインスタンスとパブリッシュインスタンスの両方で同じ ACL を使用します。詳しくは、[ユーザー管理とセキュリティ](/help/sites-administering/security.md)を参照してください。

## AEM Link Externalizer の設定 {#configuring-the-aem-link-externalizer}

Adobe Target でアクティビティを編集する場合、AEM オーサーノードで URL を変更していなければ、URL は **localhost** を指しています。書き出すコンテンツを特定の&#x200B;*Publish*&#x200B;ドメインに指定する場合は、AEM Link Externalizer を設定できます。

>[!NOTE]
>
>[クラウド設定を追加](/help/sites-administering/experience-fragments-target.md#add-the-cloud-configuration)も参照してください。

AEM Externalizer を設定するには：

>[!NOTE]
>
>詳しくは、[URL の外部化 ](/help/sites-developing/externalizer.md) を参照してください。

1. **https://&lt;server>:&lt;port>/system/console/configMgr** の OSGi Web コンソールに移動します。
1. **Day CQ Link Externalizer** を探し、オーサーノードのドメインを入力します。

   ![Day CQ Link Externalizer](assets/aem-externalizer-01.png)
