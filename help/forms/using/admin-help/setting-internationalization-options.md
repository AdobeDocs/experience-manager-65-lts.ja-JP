---
title: 国際化対応オプションの設定
description: フォームのレンダリングに使用するロケールの指定方法と、出力ストリームのエンコードに使用する文字セットの指定方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 47a49147-2921-4d28-8d04-2281c0b9a190
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 100%
---
# 国際化対応オプションの設定{#setting-internationalization-options}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

## フォームのレンダリングに使用するロケールの指定 {#specify-the-locale-used-to-render-forms}

PDF フォームをレンダリングする際に使用するロケールを指定できます。 PDF フォームのフィールドでは、指定されたロケールを使用してデータを表示します。 例えば、ロケールがドイツ語に設定されている場合、フォームでは、数値にドイツ語の小数点記号を使用します。 ロケールは、Web ブラウザーなどのクライアントデバイスに、HTML 変換の一部として検証メッセージを送信する場合にも使用されます。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「国際化対応」の「言語」リストで、フォームのレンダリングに使用するロケールを選択します。 デフォルト値は「英語（米国）」です。
1. 「保存」をクリックします。

## 出力ストリームのエンコードに使用する文字セットの指定 {#specify-the-character-set-used-to-encode-the-output-stream}

1. 「国際化対応」の「文字セット」リストで、文字セットを選択します。 この設定は、使用する API（renderHTMLForm または renderPDFForm）によって異なります。 リストにない文字セットを指定するには、「カスタム」を選択し、表示されたボックスでエンコーディング値を指定します。

   HTML の変換について AEM Forms で使用できるエンコーディング値は、`java.nio.charset` パッケージで定義されています。 sFormPreference が PDFForm の場合は、特定の文字セットのみがサポートされます。 文字セットは、有効な正規名で指定する必要があります。 デフォルト値は「ISO-8859-1」です。

1. 「保存」をクリックします。
