---
title: We.Finance 自動保険更新リファレンスサイトのチュートリアル
description: ウォークスルーして、「We.Finance」自動保険更新リファレンスサイトについて説明します。
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: User, Developer
exl-id: 3f9f1a20-9029-4e30-9c9d-ef452512f7e9
source-git-commit: c0bf6864bb344e582c4f88371c892d401ce2827c
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 48%

---

# `We.Finance` 自動保険更新リファレンスサイトのチュートリアル{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## `We.Finance` 参照サイトのシナリオ  {#we-finance-reference-site-scenario}

`We.Finance` の Web サイトは、AEM Formsのインタラクティブ通信機能の学習に役立つ金融サービスサイトです。

AEM Forms とMicrosoft® Dynamics との統合によって金融サービス会社の顧客体験をパーソナライズする方法を示す、`We.Finance` 自動保険のユースケースについて詳しく説明します。 このインタラクティブなチュートリアルは、金融会社における複雑なデジタルトランザクションや、顧客とのコミュニケーションの実装を容易にすることを目的としています。

**まず、ユースケースをご覧ください。**

Sarah Rose は既存の `We.Finance` 顧客で、自動保険ポリシーを購入しています。 現在、Sarah は保険ポリシーの更新時期を迎えています。Gloria Rios は彼女の保険営業担当です。`We.Finance` の web サイトから、Sarah にポリシーの更新に関するリマインダーがメールで送信されます。 Sarah はメールの指示に従い、プロセスを正常に完了します。

## 自動保険申し込みのチュートリアル {#auto-insurance-application-walkthrough}

`We.Finance` の自動保険申し込みのシナリオでは、次の 2 人のペルソナを使用して視覚的に説明します。

* Sarah Rose （`We.Finance` のお客様）
* `We.Finance`、保険代理店、Gloria Rios

### Gloria が `We.Finance` から保険証券の更新に関する通信を送信します {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria は AEM インスタンスにログインし、「**自動保険更新**」をクリックしてから「**エージェント UI を開く**」をクリックします。クリックすると、Sarah Rose のポリシーの詳細が保険関連ドキュメントに表示されます。Gloria が「**送信** をクリックすると、画面に「送信開始」メッセージが表示されたあと、数秒後に「送信完了」と表示されます。

Sarah は「自動保険更新」という件名のメールを受信します。

![エージェント UI](assets/agent_ui_email_new.png)

#### 実際の動作確認 {#see-it-yourself}

**Adobe Experience Manager** / **Forms** / **Formsとドキュメント** / **`We.Finance`** / **自動保険** に移動します。 「自動保険更新／**インタラクティブなコミュニケーション**」を選択し、「**エージェント UI を開く**」をクリックします。エージェント UI でインタラクティブなコミュニケーションが開きます。ポリシードキュメントが添付されたメールを受信するには、有効なメールアドレスを入力して「送信」をクリックします。

`https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.` から自動保険更新インタラクティブなコミュニケーションに直接アクセスして確認することができます。

### Sarah は `We.Finance` から保険ポリシー更新通知を受信し、更新を決定します {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah は、`We.Finance` から添付ファイル付きのメールを受信し、自動保険ポリシーの有効期限が近づいていることを Sarah に知らせます。 添付ファイルは、印刷用の自動保険レターです。

Sarah が「**今すぐ更新する**」オプションをクリックすると、自動保険レターの Web 版にリダイレクトされます。 このレターの上部には、ポリシーの期限が切れるまでの残り時間が表示されます。 このページには、保険証券の概要が表示されます。 ポリシー番号、請求額、割引オファー、ロイヤルティ報酬について詳しく説明します。 ポリシーの下部の **今すぐ更新する** をクリックします。

![ref1](assets/ref1.png)

#### 仕組み {#how-it-works}

自動保険レターの Web 版と印刷版は、インタラクティブ通信のマルチチャネル機能を使用して作成されます。

メールの「今すぐ更新」ボタンは、自動保険更新アプリケーションにリンクされています。自動保険更新アプリケーションは、パブリッシュインスタンス上のインタラクティブ通信です。

#### 実際の動作確認 {#see-it-yourself-1}

PDF が添付されたメールを受信します。PDF は自動保険レターの印刷版です。「**今すぐ更新する**」をクリックしてポリシーの Web 版にアクセスします。自分の個人情報やポリシーの詳細を確認し、**今すぐ更新する** をクリックすると、別のインタラクティブ通信が表示されます。

メールの「**今すぐ更新**」ボタンをクリックすると、Sarah はポリシーの web 版にリダイレクトされます。次の URL にアクセスできます。

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

自動保険更新の詳細な概要を確認してからページ下部の&#x200B;**今すぐ更新する**&#x200B;をクリックします。

### Sarah は支払いページを表示します {#sarah-reaches-the-payment-page}

`We.Finance` の web サイトで Sarah は支払いページを表示します。 Sarah は、自分の記録と照らし合わせて、ポリシー番号と有効期限を再確認します。ページの右側で契約更新の支払いの概要を確認します。合計金額からプレミアム割引として 10％差し引かれていることがわかります。

#### 仕組み {#how-it-works-1}

「今すぐ更新」ボタンをクリックすると、支払いページが表示されます。支払いページはアダプティブフォームです。

#### 実際の動作確認 {#see-it-yourself-2}

「**今すぐ更新する**」をクリックして支払いページにアクセスします。クレジットカード情報を入力し、「**支払う**」をクリックします。

以下のオーサリングインスタンスから支払いページにアクセスすることができます。

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah は支払いを行ってプロセスを完了します {#sarah-makes-the-payment-and-completes-the-process}

Sarah はクレジットカードの詳細を入力し、**支払う**&#x200B;をクリックします。

#### 仕組み {#how-it-works-2}

Sarah がクレジットカードの詳細を入力し、送信をクリックすると、クレジットカードによるお支払いが処理され、アダプティブフォームに設定されたありがとうメッセージが画面に表示されます。

#### 実際の動作確認 {#see-it-yourself-3}

「支払う」をクリックすると、確認メッセージが以下の URL に表示されます。

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
