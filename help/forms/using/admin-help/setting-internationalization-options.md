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
exl-id: 47a49147-2921-4d28-8d04-2281c0b9a190
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 100%

---

# 国際化対応オプションの設定{#setting-internationalization-options}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

## フォームのレンダリングに使用するロケールの指定 {#specify-the-locale-used-to-render-forms}

PDF フォームをレンダリングする際に使用するロケールを指定できます。PDF フォームのフィールドでは、指定されたロケールを使用してデータを表示します。例えば、ロケールがドイツ語に設定されている場合、フォームでは、数値にドイツ語の小数点記号を使用します。ロケールは、Web ブラウザーなどのクライアントデバイスに、HTML 変換の一部として検証メッセージを送信する場合にも使用されます。

1. 管理コンソールで、サービス／Forms をクリックします。
1. 「国際化対応」の「言語」リストで、フォームのレンダリングに使用するロケールを選択します。デフォルト値は「英語（米国）」です。
1. 「保存」をクリックします。

## 出力ストリームのエンコードに使用する文字セットの指定 {#specify-the-character-set-used-to-encode-the-output-stream}

1. 「国際化対応」の「文字セット」リストで、文字セットを選択します。この設定は、使用する API（renderHTMLForm または renderPDFForm）によって異なります。リストにない文字セットを指定するには、「カスタム」を選択し、表示されたボックスでエンコーディング値を指定します。

   HTML の変換について AEM Forms で使用できるエンコーディング値は、`java.nio.charset` パッケージで定義されています。sFormPreference が PDFForm の場合は、特定の文字セットのみがサポートされます。文字セットは、有効な正規名で指定する必要があります。デフォルト値は「ISO-8859-1」です。

1. 「保存」をクリックします。
