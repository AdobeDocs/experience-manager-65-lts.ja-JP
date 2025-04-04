---
title: AEM Forms におけるアセットの読み込みと書き出し
description: アダプティブフォームおよびテンプレートを AEM インスタンスに読み込んだり書き出したりできます。これは、フォームを移行したり、複数のシステム間で移動したりするのに役立ちます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin,User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
exl-id: 98304115-1c27-4261-9c34-70a9d7e7cd53
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2450'
ht-degree: 100%

---

# AEM Forms におけるアセットの読み込みと書き出し{#importing-and-exporting-assets-to-aem-forms}

フォームと、関連するアセット、テーマ、データ辞書、ドキュメントフラグメントおよびレターを異なる AEM Forms インスタンス間で移動できます。そうした移動が必要になるのは、システムを移行する場合か、ステージサーバーから実稼働サーバーへ AEM Form を移動する場合です。AEM Forms UI を介したアップロードおよび読み込みがサポートされるアセットの場合、書き出しや読み込みに Forms UI を使用することをお勧めします。このようなアセットの書き出しや読み込みに AEM パッケージマネージャーを使用するのは、お勧めしません。

## フォームとドキュメントアセットのダウンロードまたはアップロード {#download-or-upload-forms-amp-documents-assets}

AEM Forms ユーザーインターフェイスを使用すると、アセットを AEM CRX パッケージまたはバイナリファイルとしてダウンロードして、AEM インスタンスからアセットを書き出すことができます。その後、ダウンロードした AEM CRX パッケージまたはバイナリファイルを別の AEM インスタンスに読み込むことができます。

AEM Forms ユーザーインターフェイスを介した書き出しと読み込みは、アダプティブフォームテンプレートおよびアダプティブフォームコンテンツポリシーを除くすべてのアセットでサポートされます。そのため、AEM Forms UI からのアダプティブフォームの書き出し時に、関連するアダプティブフォームテンプレートおよびコンテンツポリシーは、他の関連するアセットのように自動的に書き出されません。

これらのアセットタイプの場合、AEM パッケージマネージャーを使用して、ソースの AEM サーバー上で CRX パッケージを作成し、出力先のサーバーにパッケージをインストールする必要があります。パッケージの作成とインストールについて詳しくは、「[パッケージの操作](/help/sites-administering/package-manager.md)」を参照してください。

### フォームとドキュメントアセットのダウンロード {#download-forms-amp-documents-assets}

フォームとドキュメントアセットをダウンロードするには、以下の手順を実行します。

1. AEM Forms インスタンスにログインします。
1. Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) アイコン／ナビゲーション ![コンパス](assets/compass.png) アイコン／フォーム／フォームとドキュメントを選択します。
1. フォームアセットを選択し、「**ダウンロード**」アイコンを選択します。
1. 「アセットをダウンロード」で、以下のオプションのうち 1 つを選択し、「**ダウンロード**」を選択します。

   * 「**CRX パッケージとしてダウンロード**」：このオプションを使用すると、選択したすべてのアセットおよび関連する依存関係をダウンロードして、AEM Forms インスタンスから別のインスタンスに移動します。すべてのアセットおよびフォルダーを CRX パッケージとしてダウンロードします。AEM で作成されたフォーム（アダプティブフォーム、インタラクティブ通信、アダプティブフォームフラグメント）、フォームセット、フォームテンプレート、PDF ドキュメント、各種リソース（XSD、XFS、画像）など、すべてのフォームアセットを AEM Forms UI からパッケージとしてダウンロードできます。
アセットをパッケージとしてダウンロードすることのメリットは、ダウンロード用に選択されたアセットで使用されてきたアセットもダウンロードできることです。例えば、フォームテンプレート、XSD および画像を使用するアダプティブフォームがあるとします。このアダプティブフォームを選択してパッケージとしてダウンロードする場合、ダウンロードされたパッケージには、フォームテンプレート、XSD および画像も含まれています。そのアセットに関連付けられているすべてのメタデータプロパティ（カスタムプロパティを含む）も同様にダウンロードされます。

   * 「**アセットをバイナリファイルとしてダウンロード**」：このオプションを使用して、フォームテンプレート（XDP）、PDF forms（PDF）、ドキュメント（PDF）、リソース（画像、スキーマ、スタイルシート）のみをダウンロードします。これらのアセットは、外部アプリケーションで編集できます。バイナリ（XSD、XDP、画像、PDF など）を持つフォームアセットを .zip ファイルとしてダウンロードします。
「**アセットをバイナリファイルとしてダウンロード**」オプションを使用して、アダプティブフォーム、インタラクティブ通信、アダプティブフォームフラグメント、テーマ、フォームセットをダウンロードすることはできません。これらのアセットをダウンロードするには、「**CRX パッケージとしてダウンロード**」オプションを使用する必要があります。

   選択したアセットはアーカイブ（.zip ファイル）としてダウンロードされます。

   >[!NOTE]
   >
   >AEM パッケージとバイナリファイルはどちらもアーカイブ（.zip ファイル）としてダウンロードされます。アセットと一緒にアセット用のテンプレートがダウンロードされることはありません。アセット用のテンプレートは、個別に書き出す必要があります。

### フォームとドキュメントアセットのアップロード {#upload-forms-amp-documents-assets}

フォームとドキュメントアセットをアップロードするには、以下の手順を実行します。

<!--[!VIDEO](https://vimeo.com/)-->

1. AEM Forms インスタンスにログインします。
1. Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) アイコン／ナビゲーション ![コンパス](assets/compass.png) アイコン／フォーム／フォームとドキュメントを選択します。
1. **作成**／**ファイルのアップロード**&#x200B;を選択します。フォームまたはパッケージのアップロードダイアログが表示されます。
1. ダイアログボックスで、読み込むパッケージまたはアーカイブを参照し、選択します。PDF ドキュメント、XSD、画像、スタイルシートおよび XDP フォームを選択することもできます。「**開く**」を選択します。選択するフォルダーまたはファイル名に特殊文字を含めないでください。

   ダイアログボックスで、アップロードするアセットの詳細を確認し、「**アップロード**」を選択します。

   既存のフォームアセットをアップロードすると、そのアセットが更新されます。

   >[!NOTE]
   >
   >パッケージのアップロードによって既存のフォルダー階層が置換されることはありません。例えば、あるサーバーの /content/dam/formsanddocuments という場所に「トレーニング」という名前のアダプティブフォームがあるとします。ユーザーがそのアダプティブフォームをダウンロードし、他のサーバー上にアップロードします。このアップロード先のサーバーにも、同じ /content/dam/formsanddocuments に「Training」という名前のフォルダーがありました。アップロードは失敗します。

## テーマのダウンロードとアップロード {#downloading-or-uploading-a-theme}

AEM Forms では、テーマを作成、ダウンロード、アップロードできます。テーマは、フォーム、ドキュメント、レターなどの他のアセットと同様に作成できます。テーマを作成、ダウンロードし、別のインスタンスにアップロードして再利用できます。テーマについて詳しくは、「[AEM Forms のテーマ](../../forms/using/themes.md)」を参照してください。

### テーマのダウンロード {#downloading-a-theme}

他のプロジェクトやインスタンスで使用する AEM Forms のテーマを書き出すことができます。AEM では、テーマを zip ファイルとしてダウンロードし、それをインスタンスにアップロードできます。

テーマをダウンロードするには、以下の手順を実行します。

1. AEM Forms インスタンスにログインします。
1. Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) アイコン／ナビゲーション ![コンパス](assets/compass.png) アイコン／フォーム／テーマを選択します。
1. テーマを選択し、「**ダウンロード**」を選択します。テーマはアーカイブ（.zip ファイル）としてダウンロードされます。

### テーマのアップロード {#uploading-a-theme}

プロジェクトにスタイル設定がプリセットされた作成済みのテーマを使用できます。他の人が作成したテーマのパッケージをプロジェクトにアップロードしてインポートできます。

テーマをアップロードするには、以下の手順を実行します。

1. Experience Manager で、**フォーム／テーマ**&#x200B;に移動します。
1. テーマページで、**作成／ファイルのアップロード**&#x200B;をクリックします。
1. ファイルのアップロードプロンプトで、コンピューター上のテーマパッケージを参照して選択し、「**アップロード**」をクリックします。アップロードされたテーマは、テーマページで使用することができます。

1. AEM Forms インスタンスにログインします。
1. Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) アイコン／ナビゲーション ![コンパス](assets/compass.png) アイコン／フォーム／テーマを選択します。
1. **作成**／**ファイルのアップロード**&#x200B;をクリックします。ファイルのアップロードプロンプトで、コンピューター上のテーマパッケージを参照して選択し、「**アップロード**」をクリックします。テーマがアップロードされます。

## Correspondence Management におけるアセットの読み込みと書き出し {#import-and-export-assets-in-correspondence-management}

データ辞書、レター、ドキュメントフラグメントなどのアセットを 2 つの異なる Correspondence Management の実装間で共有するには、.cmp ファイルを作成して共有します。.cmp ファイルには、1 つまたは複数のデータ辞書、レター、ドキュメントフラグメント、フォームを含めることができます。

### ドキュメントフラグメント、レター、データ辞書の書き出し {#export-document-fragments-letters-and-or-data-dictionaries}

1. レター、ドキュメントフラグメントまたはデータ辞書のページの中で、単一のパッケージとして書き出すアセットを選択し、次に「ダウンロードのキュー」を選択します。書き出し用のアセットが一覧表示されます。
1. 必要に応じて上記の手順を繰り返し、レター、ドキュメントフラグメント、データ辞書を追加します。
1. 「**ダウンロード**」を選択します。
1. Correspondence Management に「アセットをダウンロード」ダイアログが表示され、エクスポートリストにアセットが一覧表示されます。

   ![export](assets/export.png)

1. 書き出された依存関係を表示するには、「解決」を選択します。または、スキップして次の手順に進みます。依存関係は「解決」を選択しなくても書き出されます。
1. .cmp ファイルをダウンロードするには「**OK**」を選択します。
1. Correspondence Management によって .cmp ファイルがお使いのコンピューターにダウンロードされます。

   .cmp ファイル には書き出されたアセットが含まれています。他のユーザーと .cmp ファイルを共有することができます。他のユーザーは、異なるサーバーに .cmp ファイルを読み込んで、新しいサーバーですべてのアセットを取得することができます。

### すべての Correspondence Management アセットをパッケージとして書き出し {#export-all-the-correspondence-management-assets-as-a-package}

このオプションを使用して、すべての Correspondence Management アセットおよび関連する依存関係を、AEM Forms インスタンスからパッケージとしてダウンロードします。

例えば、Correspondence Management に画像とテキストを使用しているレターが含まれている場合、ダウンロードしたパッケージにもレターに関連する画像とテキストが含まれます。そのアセットに関連付けられているすべてのメタデータプロパティ（カスタムプロパティを含む）も同様にダウンロードされます。パッケージ（.cmp）をダウンロードすると、[パッケージを別の AEM Forms インスタンスに読み込む](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p)ことができます。

すべての Correspondence Management アセットおよび関連する依存関係をパッケージとしてダウンロードするには、次の手順を実行します。

1. AEM Forms サーバーに Forms ユーザーとしてログインします。
1. グローバルナビゲーションバーで「**Adobe Experience Manager**」を選択します。
1. 「![ツール](assets/tools.png)」を選択し、「**Forms**」を選択します。
1. 「**Correspondence Management アセットを書き出し**」を選択します。

   ![publish-cmp-assets-1](assets/publish-cmp-assets-1.png)

   「すべての Correspondence Management アセットをエクスポート」ページが表示され、前回試行されたエクスポート処理の情報と、前回正常にエクスポートされたパッケージをダウンロードするためのリンクが表示されます。

   ![export-last-run-details](assets/export-last-run-details.png)

1. 「**書き出し**」を選択し、確認メッセージが表示されたら「**OK**」を選択します。

   バッチ処理が完了すると、前回の実行詳細とパッケージをダウンロードするためのリンクが更新されます。これには管理者ログインや、バッチの実行が成功したか失敗したかなどの情報が含まれます。アセットがパッケージに書き出されて、「書き出したパッケージをダウンロード」リンクが表示されます。

   >[!NOTE]
   >
   >「すべてのアセットを書き出し」処理は、開始してからキャンセルすることはできません。また、すべてのアセットを書き出している間は、アセットを作成、削除、変更、公開したり、「すべてのアセットを公開」処理を開始したりしないでください。

1. 「**書き出したパッケージをダウンロード**」リンクを選択して、パッケージファイルをダウンロードします。

   パッケージ内のアセットを Correspondence Management の別のインスタンスに追加するには、[パッケージを AEM Forms インスタンスにインポート](../../forms/using/import-export-forms-templates.md#p-upload-forms-documents-assets-p)します。

### ドキュメントフラグメント、レターまたはデータ辞書の Correspondence Management への読み込み {#import-document-fragments-letters-and-or-data-dictionaries-into-correspondence-management}

.cmp ファイルに書き出されたアセットを読み込むことができます。.cmp ファイルには、1 つまたは複数のレター、データ辞書、ドキュメントフラグメント、依存アセットが含まれています。

>[!NOTE]
>
>移行したい古い Correspondence Management アセットを読み込んでいる間、管理者アカウントを使用してログインします。古い Correspondence Management アセットの移行について詳しくは、[AEM 6.1 Forms への Correspondence Management アセットの移行](/help/forms/using/migration-utility.md)を参照してください。

1. データ辞書、レター、ドキュメントフラグメントのページ上で、**作成／ファイルのアップロード**&#x200B;を選択し、.cmp ファイルを選択します。
1. Correspondence Management にアセットの読み込みダイアログが表示され、読み込まれるアセットが一覧表示されます。「**読み込み**」を選択します。

   アセットが読み込まれると、次のアセットのプロパティが更新されます（その他のプロパティは変更されません）。

   * 作成者：アセットをサーバーに読み込んだユーザーの ID を表示します。
   * 変更済み：アセットがサーバーに読み込まれた時刻

   >[!NOTE]
   >
   >XDP を cmp ファイルの一部として、または別の方法でアップロードできるようにするには、ユーザーは forms-power-users グループに含まれている必要があります。アクセス権については、管理者に問い合わせてください。

## ワークフローアプリケーションの書き出し {#export-a-workflow-application}

AEM パッケージマネージャーを使用して、ワークフローアプリケーションを書き出すことができます。手順を以下に示します。

1. AEM Forms パッケージマネージャーを開きます。パッケージマネージャーの URL は、https://&lt;server>:&lt;port>/crx/packmgr です。
1. 「**[!UICONTROL パッケージを作成]**」をクリックします。**[!UICONTROL 新規パッケージ]**&#x200B;ダイアログボックスが表示されます。
1. パッケージの名前、バージョン、グループを指定します。「**[!UICONTROL OK]**」をクリックします。
1. 「**[!UICONTROL 編集]**」をクリックし、「**[!UICONTROL フィルター]**」タブを開きます。「**[!UICONTROL フィルターを追加]**」をクリックします。ワークフローアプリケーションのパスを指定します。例えば、/etc/fd/dashboard/startpoints/homemortgage などです。「**[!UICONTROL ルールを追加]**」をクリックします。

1. 「**[!UICONTROL 詳細]**」タブを開きます。ACL Handling フィールドで、「**[!UICONTROL 結合]**」または「**[!UICONTROL 上書き]**」を選択します。「**[!UICONTROL 保存]**」をクリックします。
1. 「**[!UICONTROL ビルド]**」をクリックし、パッケージを作成します。

   パッケージが作成されたら、パッケージをダウンロードして別のサーバーに読み込むことができます。パッケージがアップロードされるサーバーにワークフローアプリケーションが表示されます。

   >[!NOTE]
   >
   >ワークフローアプリケーションを正しく動作させるために、作業アプリケーションを使用して対応するアダプティブフォームとワークフローモデルも書き出します。

## フォルダーとアセットの整理 {#folders-and-organizing-assets}

AEM Forms のユーザーインターフェイスは、フォルダーを利用してアセットを整理します。これらのフォルダーは、AEM Forms ユーザーインターフェイスで作成されたアセットの整理に使用されます。これらのフォルダーでは、名前の変更やサブフォルダーの作成、アセットおよびドキュメントの保存を行うことができます。フォルダー内でドキュメントおよびアセットを整理すると、ファイルをグループ化して容易に管理できます。フォルダーを選択し、ダウンロードするか削除するかを選択します。

フォルダーを作成するには、以下の手順を実行します。

### フォルダーの作成 {#create-a-folder}

1. `https://<server>:<port>/aem/forms.html` で、AEM Forms ユーザーインターフェイスにログインします。
1. フォルダーを作成する場所に移動します。
1. 作成／フォルダーを選択します。
1. 以下の詳細を入力します。

   * **タイトル**：フォルダーの表示名
   * **名前**：*（必須）*&#x200B;リポジトリー内のフォルダーを保存するノード名

   >[!NOTE]
   >
   >デフォルトでは、名前フィールドの値がタイトルから自動入力されます。名前には、英数字、ハイフン（-）、下線（_）のみを含めることができます。タイトルにその他の特殊文字を入力すると、それらは自動的にハイフンに置換され、この新しい名前を確認するよう指示されます。提示された名前をそのまま使用するか、またはそれを編集できます。

1. 定義したタイトルを持つ新しいフォルダーは、アセットリスト内の現在の場所に表示されます。

   指定した名前を持つフォルダーが既に存在する場合は、送信はエラーになり失敗します。名前フィールドの横に表示されるエラー ![aem6forms_error_alert](assets/aem6forms_error_alert.png) アイコンの上にマウスポインターを置くと、エラーメッセージを見ることができます。

   新しく作成されたフォルダーを選択してフォルダー内に移動し、フォルダー内でアセットまたはフォルダーを作成できます。さらに、フォルダーを選択し、ダウンロードのキューに入れるか、削除するか、名前を編集するかを選択できます。

   ![editdeletedownloadafolder](assets/editdeletedownloadafolder.png)

### 1 つまたは複数のアセットまたはレターのコピーを作成する {#create-copies-of-one-or-more-assets-or-letters}

既存のアセットやレターを使用して、類似のプロパティ、コンテンツ、継承されたアセットを持つアセットやレターをすばやく作成できます。データ辞書、ドキュメントフラグメントおよびレターをコピーして貼り付けることができます。

アセットとレターのコピーを作成するには、次の手順を実行します。

1. 関連するアセットまたはレターページで、1 つまたは複数のアセットまたはレターを選択します。UI にコピーアイコンが表示されます。
1. 「コピー」を選択します。UI に貼り付けアイコンが表示されます。レターを貼り付ける前に、フォルダー内に移動することもできます。複数のフォルダーに同じ名前のアセットを保管することができます。フォルダーについて詳しくは、[フォルダーとアセットの整理](#folders-and-organizing-assets)を参照してください。
1. 「貼り付け」を選択します。貼り付けダイアログが表示されます。アセットまたはレターの新しいコピーに自動的に名前とタイトルが生成されて割り当てられますが、これらのタイトルと名前は編集できます。

   同じ場所にアセットまたはレターをコピーアンドペーストすると、アセットまたはレターの既存の名前の最後に「-CopyXX」が追加されます。コピーされたアセットやレターにタイトルが存在しない場合、自動生成されたタイトルフィールドは空白のままです。

1. 必要に応じて、コピーを保存するアセットまたはレターのタイトルと名前を編集します。
1. 「貼り付け」を選択します。コピーされたアセットの新しいコピーが作成されます。

## 検索 {#search-forms}

AEM Forms の UI を使用して、コンテンツを検索することができます。上部バーで検索 **[A]** を選択すると、アセットやドキュメントなどのリソースをコンテンツから検索することができます。

アセットを検索する場合、AEM Forms にサイドパネルが表示されます。![アセットブラウザーコンテンツのみ](assets/assets-browser-content-only.png)／フィルター **[B]** を選択して、サイドパネルを呼び出すこともできます。サイドパネルに表示される各種フィルターを使用して、検索範囲を絞り込むことができます。サイドパネルを使用して、検索を保存することもできます。

![search_topbar](assets/search_topbar.png)

**A.** 検索 **B.** フィルター

![サイドパネル - フィルター](assets/search_sidepanel.png)

サイドパネル - フィルター

サイドパネルで、次のフィルターを使用して検索範囲を絞り込むことができます。

* 検索ディレクトリ
* タグ
* 検索基準（変更日、公開ステータス、ライブコピーのステータスなど）。

サイドパネルを使用して、選択した名前を使用して検索設定を保存することもできます。

検索、フィルター、保存した検索、サイドパネルとそれらの使用について詳しくは、「[検索](/help/sites-authoring/search.md)」を参照してください。
