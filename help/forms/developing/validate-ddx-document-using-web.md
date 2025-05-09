---
title: Web サービス API を使用した DDX ドキュメントの検証
description: DDX ドキュメントを検証するには、Assembler Service API を使用します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
hide: true
hidefromtoc: true
exl-id: f934b721-1ca3-4626-9039-a38f0dfecea2
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 100%

---

# Web サービス API を使用した DDX ドキュメントの検証 {#validate-a-ddx-document-using-theweb-service-api}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Assembler Service API（web サービス）を使用して DDX ドキュメントを検証します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >localhost を Forms サーバーの IP アドレスに置き換えます。

1. PDF Assembler クライアントを作成します。

   * デフォルトのコンストラクターを使用して、`AssemblerServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`AssemblerServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding` フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `AssemblerServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `AssemblerServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDX ドキュメントの保存に使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを保存するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` プロパティにバイト配列のコンテンツを割り当てて、`BLOB` オブジェクトを入力します。

1. DDX ドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトの `validateOnly` データメンバーに true の値を割り当てることにより、DDX ドキュメントを検証するように Assembler サービスに指示する実行時オプションを設定します。
   * `AssemblerOptionSpec` オブジェクトの `logLevel` データメンバーに文字列値を割り当てて、Assembler サービスがログファイルに書き込む情報の量を設定します。DDX ドキュメントを検証する場合、検証プロセスに役立つ詳細情報をログファイルに書き込みます。その結果、`FINE` または `FINER` の値を指定できます。設定できる実行時オプションについて詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `AssemblerOptionSpec` クラス参照を参照してください。

1. 検証を実行します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、次の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクト。
   * 通常は PDF ドキュメントを格納する `Map` オブジェクトの値 `null`。
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクト。

   `invokeDDX` メソッドは、DDX ドキュメントが有効かどうかを示す情報が格納される `AssemblerResult` オブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * コンストラクターを呼び出し、ログファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。ファイル名の拡張子が .xml であることを確認します。
   * `AssemblerResult` オブジェクトの `jobLog` データメンバーの値を取得して、ログ情報を格納する `BLOB` オブジェクトを作成します。
   * `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` フィールドの値を取得して、バイト配列に入力します。
   * コンストラクターを呼び出し、`System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * バイト配列のコンテンツを PDF ファイルに書き込むには、`System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡してください。

   >[!NOTE]
   >
   >DDX ドキュメントが無効な場合、`OperationException` がスローされます。catch ステートメント内で、`OperationException` オブジェクトの `jobLog` メンバーの値を取得できます。

**関連トピック**

[DDX ドキュメントの検証](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
