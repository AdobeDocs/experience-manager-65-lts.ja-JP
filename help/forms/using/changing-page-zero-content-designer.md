---
title: Designer でのページゼロコンテンツの変更
description: XFA PDF を アドビ以外の PDF ビューアーで表示するとき、Page Zero に表示されるメッセージを変更する方法をご存知ですか。
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms,Forms Designer,Designer
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: f966f5fb-338a-4d8e-91c6-aa0eddd03420
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 100%

---

# Designer での Page Zero コンテンツの変更 {#changing-page-zero-content-in-designer}

[!DNL Chrome] または [!DNL Firefox] のデフォルト PDF ビューアなど、アドビ以外の PDF ビューアで PDF／XFA フォームのコンテンツを読み取れない場合、Page Zero コンテンツがデフォルトで表示されます。デフォルトの Page Zero メッセージは、以下のとおりです。

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] バージョンの Designer を使用すると、Page Zero に表示されるメッセージを変更できます。Page Zero メッセージを変更するには、以下の手順を実行します。

1. [!DNL AEM Forms] バージョンの Designer がインストールされていることを確認します。Designer のバージョン情報画面で、バージョンを確認できます。

1. Page Zero コンテンツを変更するフォームを開きます。

1. **[!UICONTROL ファイル]**／**[!UICONTROL フォームのプロパティ]**&#x200B;をクリックします。

1. [!UICONTROL フォームのプロパティ]ダイアログで、![プラス](assets/plus.png)（プラスアイコン）をクリックしてカスタムプロパティを追加します。

1. プロパティの名前として **_pagezerocontent** を指定します。
1. 新しい Page Zero メッセージを、リッチテキスト形式で値として追加します。次に例を示します。


   `<body xmlns="http://www.w3.org/1999/xhtml" xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/reader_download_jp.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </span></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </span>https://www.adobe.com/go/acrreader_jp.</p></body>`

1. フォームを PDF として保存します。

1. PDF フォームをブラウザーで表示して、メッセージが更新されたことを確認します。前述の例は、以下のように表示されます。

   ![changedmessage](assets/changedmessage.png)

>[!NOTE]
>
>フォームを再度開いたときに、作成したカスタムプロパティがフォームプロパティダイアログに正しく表示されない場合があります。その場合でも、動作には問題ありません。フォームには、更新後の Page Zero メッセージが表示されます。
