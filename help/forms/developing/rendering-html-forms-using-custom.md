---
title: カスタム CSS ファイルを使用した HTML フォームのレンダリング
description: Forms サービスを使用してカスタム CSS ファイルを参照し、web ブラウザーからの HTTP リクエストに応答して HTML フォームをレンダリングします。Java API と web サービス API を使用して、CSS ファイルを使用する HTML フォームをレンダリングできます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: b70404ee-21dc-4c0b-a66f-c37a6f29f98e
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 100%

---

# カスタム CSS ファイルを使用した HTML フォームのレンダリング {#rendering-html-forms-using-custom-css-files}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Forms サービスは、web ブラウザーからの HTTP リクエストに応答して HTML フォームをレンダリングします。HTML フォームをレンダリングする際は、Forms サービスはカスタム CSS ファイルを参照できます。Forms サービスを使用して HTML フォームをレンダリングする際に、ビジネス要件を満たすカスタム CSS ファイルを作成し、その CSS ファイルを参照することができます。

Forms サービスは、カスタム CSS ファイルをサイレントに解析します。つまり、Forms サービスは、カスタム CSS ファイルが CSS 標準に準拠していないためにエラーが発生しても報告しません。この場合、Forms サービスはこのスタイルを無視し、CSS ファイルの残りのスタイルを引き続き使用します。

次のリストは、カスタム CSS ファイルでサポートしているスタイルを示します。

* **クラスレベルのセレクターとスタイルのペア**：カスタム CSS ファイルに存在する場合、クラススタイルとして HTML フォームで使用したセレクターが使用されます。未使用のクラススタイルは無視されます。
* **識別情報レベルのセレクターとスタイルのペア**：HTML フォームで使用される場合は、すべての 識別情報スタイルが使用されます。
* **要素レベルのセレクターとスタイルのペア**：HTML フォームで使用される場合は、すべての要素スタイルが使用されます。
* **スタイルの優先度**：スタイルの優先度（重要など）がサポートされており、カスタム CSS ファイルで使用できます。
* **メディアタイプ**：1 つ以上のセレクターとスタイルのペアを @media スタイルでラップして、メディアタイプを定義できます。Forms サービスは、指定されたメディアタイプがサポートされているかどうかをチェックしません。カスタム CSS ファイルで指定されたメディアタイプは、HTML フォームにマージされます。

FormsIVS アプリケーションを使用すると、CSS ファイルのサンプルを取得できます。フォームをアップロードして「フォームデザインのテスト」ページで選択し、「GenerateCSS」をクリックします。ボタンをクリックする前に、HTML 変換タイプを設定する必要はありません。次に、保存を選択します。ビジネス要件を満たすように、この CSS ファイルを編集することができます。

>[!NOTE]
>
>カスタム CSS ファイルを使用する HTML フォームをレンダリングする前に、HTML フォームのレンダリングについて理解していることが重要です。（[フォームを HTML としてレンダリングする](/help/forms/developing/rendering-forms-html.md)を参照してください）。

>[!NOTE]
>
>Forms サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## 手順の概要 {#summary-of-steps}

CSS ファイルを使用する HTML フォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Java API オブジェクトを作成します。
1. CSS ファイルを参照します。
1. HTML フォームをレンダリングします。
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルのインクルード**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Java API オブジェクトの作成**

Forms サービスでサポートされている操作をプログラムで実行する前に、Forms クライアントオブジェクトを作成する必要があります。

**CSS ファイルの参照**

カスタム CSS ファイルを使用する HTML フォームをレンダリングするには、既存の CSS ファイルを参照していることを確認してください。

**HTMLフォームのレンダリング**

HTML フォームをレンダリングするには、Designer で作成され XDP ファイルとして保存されたフォームデザインを指定します。HTML 変換タイプを選択します。たとえば、Internet Explorer 5.0 以降のダイナミック HTML をレンダリングする HTML 変換タイプを指定できます。

HTML フォームのレンダリングには、他のフォームタイプのレンダリングに必要な URI などの値も必要です。

**クライアント web ブラウザーへのフォームデータストリームの書き込み**

Forms サービスで HTML フォームをレンダリングすると、フォームデータストリームが返されます。HTML フォームをユーザーに表示するために、返されたデータストリームをクライアント web ブラウザーに書き込む必要があります。

**関連項目**

[Java API を使用して、CSS ファイルを使用する HTML フォームをレンダリングする](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms を HTML としてレンダリング](/help/forms/developing/rendering-forms-html.md)

[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API を使用して、CSS ファイルを使用する HTML フォームをレンダリングする {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

カスタム CSS ファイルを使用する HTML フォームを Forms API（Java）を使用してレンダリングする

1. プロジェクトファイルを含める

   クライアント JAR ファイル（adobe-forms-client.jar など）を Java プロジェクトのクラスパスに含めます。

1. Forms Java API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`FormsServiceClient` オブジェクトを作成します。

1. CSS ファイルの参照

   * コンストラクターを使用して `HTMLRenderSpec` オブジェクトを作成します。
   * カスタム CSS ファイルを使用する HTML フォームをレンダリングするには、`HTMLRenderSpec` オブジェクトの `setCustomCSSURI` メソッドを呼び出し、CSS ファイルの場所と名前を指定する文字列値を渡します。

1. HTML フォームのレンダリング

   `FormsServiceClient` オブジェクトの `(Deprecated) (Deprecated) renderHTMLForm` メソッドを呼び出して、以下の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定します。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * HTML の環境設定タイプを指定する `TransformTo` enum 値。例えば、Internet Explorer 5.0 以降の動的 HTML と互換性のある HTML フォームをレンダリングするには、`TransformTo.MSDHTML` を指定します。
   * フォームに結合するデータを含む `com.adobe.idp.Document` オブジェクト。データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * HTML の実行時オプションが格納された `HTMLRenderSpec` オブジェクト。
   * `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)` などの `HTTP_USER_AGENT` ヘッダー値を指定する文字列値。
   * HTML フォームのレンダリングに必要な URI 値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクト。これはオプションのパラメーターで、 フォームにファイルを添付しない場合は `null` を指定できます。

   `(Deprecated) renderHTMLForm` メソッドは、 クライアント web ブラウザーに書き込む必要があるフォームデータストリームを含んだ `FormsResult` オブジェクトを返します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `setContentType` メソッドを呼び出してコンテンツタイプを設定し、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.h\ttp.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、`javax.servlet.ServletOutputStream` オブジェクトを作成します。このオブジェクトは、フォームデータストリームをクライアント web ブラウザーに書き込むために使用されます。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出して、`java.io.InputStream` オブジェクトを作成します。
   * `InputStream` オブジェクトの `read` メソッドを呼び出してバイト配列を引数として渡すことによって、バイト配列を作成してフォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連項目**

[カスタム CSS ファイルを使用した HTML フォームのレンダリング](#rendering-html-forms-using-custom-css-files)

[クイックスタート（SOAP モード）：Java API を使用して CSS ファイルを使用する HTML フォームをレンダリングします](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用して、CSS ファイルを使用する HTML フォームをレンダリングする {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Forms API（web サービス）を使用して、カスタム CSS ファイルを使用する HTML フォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * クラスパスに Java プロキシクラスを含めます。

1. Forms Java API オブジェクトの作成

   `FormsService` オブジェクトを作成し、認証情報を設定します。

1. CSS ファイルの参照

   * コンストラクターを使用して `HTMLRenderSpec` オブジェクトを作成します。
   * カスタム CSS ファイルを使用する HTML フォームをレンダリングするには、`HTMLRenderSpec` オブジェクトの `setCustomCSSURI` メソッドを呼び出し、CSS ファイルの場所と名前を指定する文字列値を渡します。

1. HTML フォームのレンダリング

   `FormsService` オブジェクトの `(Deprecated) renderHTMLForm` メソッドを呼び出して、以下の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定します。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * HTML の環境設定タイプを指定する `TransformTo` enum 値。例えば、Internet Explorer 5.0 以降の動的 HTML と互換性のある HTML フォームをレンダリングするには、`TransformTo.MSDHTML` を指定します。
   * フォームに結合するデータを含む `BLOB` オブジェクト。データを結合しない場合は、`null` を渡します。（[編集可能なレイアウトを使用した Forms の事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md)を参照してください）。
   * HTML 実行時オプションを格納する `HTMLRenderSpec` オブジェクト。
   * `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)` などの `HTTP_USER_AGENT` ヘッダー値を指定する文字列値。この値を設定しない場合は、空の文字列を渡します。
   * HTML フォームのレンダリングに必要な URI 値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクト。このパラメーターはオプションであり、フォームにファイルを添付しない場合は `null` を指定できます。
   * `(Deprecated) renderHTMLForm` メソッドによって設定された空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト。このパラメーター値には、レンダリングされたフォームが格納されます。
   * `(Deprecated) renderHTMLForm` メソッドで入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト。このパラメーターには、出力 XML データが格納されます。
   * `(Deprecated) renderHTMLForm` メソッドでデータが入力される空の `javax.xml.rpc.holders.LongHolder` オブジェクト。この引数には、フォームのページ数が格納されます。
   * `(Deprecated) renderHTMLForm` メソッドでデータが入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。この引数には、ロケール値が格納されます。
   * `(Deprecated) renderHTMLForm` メソッドでデータが入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。この引数には、使用する HTML レンダリング値が格納されます。
   * この操作の結果を格納する空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。

   `(Deprecated) renderHTMLForm` メソッドは、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアント web ブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバーの値を取得して、`FormResult` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、フォームデータを含む `BLOB` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`BLOB` オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `setContentType` メソッドを呼び出してコンテンツタイプを設定し、`BLOB` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、クライアントの web ブラウザーにフォームデータストリームを書き込むために使用する `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `BLOB` オブジェクトの `getBinaryData` メソッドを呼び出し、バイト配列を作成して入力します。このタスクは、`FormsResult` オブジェクトのコンテンツをバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連項目**

[カスタム CSS ファイルを使用した HTML フォームのレンダリング](#rendering-html-forms-using-custom-css-files)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
