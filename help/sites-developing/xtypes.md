---
title: xtype の使用（クラシック UI）
description: Adobe Experience Manager で利用できるすべての xtype について説明します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: 4a78de53-33bf-4999-ba3c-7d0bc33196a4
source-git-commit: 24bd1f57da3f9ce613ee28276d1ae9465b6dfba6
workflow-type: tm+mt
source-wordcount: '3668'
ht-degree: 59%

---

# xtype の使用（クラシック UI）{#using-xtypes-classic-ui}

このページでは、Adobe Experience Manager（AEM）で利用できるすべての xtype について説明します。

ExtJS 言語では、xtype はクラスに付与されるシンボル名です。xtype とその使用方法について詳しくは、[ExtJS 2 の概要](https://docs.sencha.com/)の「Component XTypes」の段落を参照してください。

AEMで使用可能なすべてのウィジェットについて詳しくは、[widget API ドキュメント &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を参照してください。

AEMで特定の xtype が使用されるコンポーネントを調べるには、CRXDE で次の `Xpath` クエリを使用します。 &#39;checkbox&#39;を目的の xtype に置き換えるだけです。

`//element(*, cq:Widget)[@xtype='checkbox']`

>[!NOTE]
>
>このページでは、クラシック UI での ExtJS xtype の使用方法について説明します。
>
>アドビでは、[Coral UI](/help/sites-developing/touch-ui-concepts.md#coral-ui) および [Granite UI](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components) に基づく標準の最新の[タッチ対応 UI](/help/sites-developing/touch-ui-concepts.md) を使用することをお勧めします。

## xtype {#xtypes}

Adobe Experience Manager で使用可能な xtype を以下に示します。

* `annotation`

  [CQ.wcm.Annotation](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Annotation` は特別な窓です。 本文にフォーム、フッターにボタングループが含まれています。 通常はコンテンツの編集に使用されますが、単に情報のみを表示するために使用されることもあります。

* `arraystore`

  [CQ.Ext.data.ArrayStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  以前の名称：`SimpleStore`。

  配列データからの [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s の作成を容易にする小さなヘルパークラス。 `ArrayStore` は、[CQ.Ext.data.ArrayReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) で自動的に設定されます。

* `asseteditor`

  [CQ.dam.AssetEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Asset Editor` は DAM 管理で使用されます。

* `assetreferencesearchdialog`

  [CQ.wcm.AssetReferenceSearchDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `AssetReferenceSearchDialog` は、ページがアセットまたはタグを参照する場合にポップアップ表示されるダイアログボックスです。

* `blueprintconfig`

  [CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BlueprintConfig` にはブループリントのライブコピーを表示したり、このブループリントのプロパティ（同期トリガーと同期操作）を編集したりできるパネルがあります。

* `blueprintstatus`

  [CQ.wcm.msm.BlueprintStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BlueprintStatus は、ブループリントとライブコピーの関係を表示および編集できるパネルを提供します。[CQ.wcm.msm.BlueprintStatus.Tree](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用してブラウジングし、[CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) および [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用して編集します。

* `box`

  [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [コンポーネント](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)の基底クラスであり、幅と高さを使用して、ボックスとしてサイズを変更します。

  BoxComponent は、サイズと位置を自動的に調整するボックスモデルを提供し、コンポーネントのレンダリングモデルで正常に動作します。

* `browsedialog`

  [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BrowseDialog により、ユーザーはパスを選択するためにリポジトリを参照できます。通常は、[BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) で使用されます。

* `browsefield`

  [CQ.form.BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **非推奨：代わりに [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用**

* `bulkeditor`

  [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BulkEditor` は、検索エンジンと、検索結果を編集するためのグリッドを提供します。

  `BulkEditor` は、HTML フォームに挿入する必要があります（読み込み機能で必要）。 [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) で適切に動作します。

* `bulkeditorform`

  [CQ.wcm.BulkEditorForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BulkEditorForm は、HTML フォームで囲まれた [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を提供します。[CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) のスタンドアロンバージョン 「読み込み」ボタンにはHTML フォームが必要です。

* `button`

  [CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  シンプルな Button クラス

* `buttongroup`

  [CQ.Ext.ButtonGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ボタングループのためのコンテナ。

* `chart`

  [CQ.Ext.chart.Chart](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CQ.Ext.chart パッケージは、Flash ベースのグラフを使用したデータの視覚化を実現します。各グラフは、CQ.Ext.data.Store に直接バインドされ、グラフの自動更新が可能になります。グラフの外観を変更するには、[chartStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) および [extraStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の設定オプションを確認します。

* `checkbox`

  [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  単一チェックボックスフィールド。従来のチェックボックスフィールドにそのまま置き換えて使用できます。

* `checkboxgroup`

  [CQ.Ext.form.CheckboxGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) コントロールのグループ化コンテナ。

* `clearcombo`

  [CQ.form.ClearableComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ClearableComboBox は、値を消去するトリガーを持つ、編集できないコンボボックスです。

* `colorfield`

  [CQ.form.ColorField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ColorField は、ユーザーが直接または[CQ.Ext.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を使用して色の hex 値を入力できるようにします。

* `colorlist`

  [CQ.form.ColorList](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

   ColorList は、ユーザーが編集可能なリストから色を選択できるようにします。

* `colormenu`

  [CQ.Ext.menu.ColorMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) コンポーネントを含むメニュー。

* `colorpalette`

  [CQ.Ext.ColorPalette](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  色を選択するためのシンプルなカラーパレットクラス。パレットはどのコンテナにもレンダリングできます。

* `combo`

  [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  オートコンプリート、リモートローディング、ページングなど、その他多くの機能をサポートするコンボボックスコントロール。

  ComboBox は、従来の HTML &lt;select>フィールドと同じように動作します。相違点として、[valueField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を送信するために、非表示の入力フィールドを作成する [hiddenName](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を指定する必要があります。

* `component`

  [CQ.Ext.Component](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  すべての `Ext` コンポーネントの基本クラス。 コンポーネントのすべてのサブクラスは、`Ext`Container[&#x200B; クラスが提供する、作成、レンダリング、破棄の自動 &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) コンポーネントライフサイクルに関与できます。 コンポーネントは、コンテナ作成時に、[items](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 設定オプションでコンテナに追加されます。

* `componentextractor`

  [CQ.wcm.ComponentExtractor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ComponentExtractor は、ユーザーが web サイト／ページからコンポーネントを抽出できるようにします。

* `componentselector`

  [CQ.form.ComponentSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  グループ化され、順序付けされた利用可能なコンポーネント群。

* `componentstyles`

  [CQ.form.ComponentStyles](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `compositefield`

  [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  1 つのフォームフィールドまたはフォームフィールドのグループを含む、パネルをベースとした複雑なフォームフィールドの基本クラス。

* `container`

  [CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  その他のコンポーネントを含められる [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の基底クラス。コンテナは、アイテムの格納の基本動作（アイテムの追加、挿入、削除など）を処理します。

  最もよく使用される Container クラスは、[CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) および [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) です。

* `contentfinder`

  [CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinder は、左に実際のコンテンツファインダー、右にコンテンツフレームを含む、2 列の専用の[ビューポート](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)です。

* `contentfindertab`

  [CQ.wcm.ContentFinderTab](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinderTab は、[CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) のタブパネルで使用される機能を提供する専用のパネルです。通常、検索フォーム（クエリボックス）と、検索を表示するデータビューが備わっています。

* `cq.workflow.model.combo`

  [CQ.wcm.WorkflowModelCombo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  WorkflowModelCombo は、利用できるワークフローモデルのリストを表示する、カスタマイズされた [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) です。

* `cq.workflow.model.selector`

  [CQ.wcm.WorkflowModelSelector](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  WorkflowModelSelector は、WorkflowModelCombo を、ワークフローのサムネール画像のほか、ワークフローモデルの作成および編集のためのボタンと組み合わせたものです。

* `createsitewizard`

  [CQ.wcm.CreateSiteWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CreateSiteWizard は、（MSM）サイトを作成するためのステップバイステップ方式のウィザードです。

* `createversiondialog`

  [CQ.wcm.CreateVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CreateVersionDialog は、バージョンのページを作成できるダイアログボックスです。

* `customcontentpanel`

  [CQ.CustomContentPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CustomContentPanel は、[CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) で使用するための特別なパネルです。そのコンテンツは、ダイアログボックス内の他のフィールドとは異なる URL から取得され、送信されます。

* `cycle`

  [CQ.Ext.CycleButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 要素のメニューを含む専用の SplitButton。このボタンは、アクティブなメニューアイテムに対してボタンの [change](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) イベントを生成しながら（または指定されている場合は、ボタンの [changeHandler](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 関数を呼び出しながら）、クリックごとに各メニューアイテムを循環します。

* `dataview`

  [CQ.Ext.DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  カスタムレイアウトテンプレートと書式設定を使用してデータを表示するメカニズム。DataView は、内部テンプレートのメカニズムとして [CQ.Ext.XTemplate](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用し、[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) にバインドされます。ストア内のデータが変更されると、ビューは変更を反映して自動的に更新されます。

* `datefield`

  [CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) ドロップダウンと自動日付検証機能を備えた日付入力フィールドを提供します。

* `datemenu`

  [CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) コンポーネントを含むメニュー。

* `datepicker`

  [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ポップアップ日付選択。 このクラスは、有効な日付を参照および選択できるようにするために、[DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) クラスで使用されます。

* `datetime`

  [CQ.form.DateTime](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  DateTime は、[CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)と[CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を組み合わせて、ユーザーが日付と時刻を入力できるようにします。

* `dialog`

  [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ダイアログは特別なウィンドウです。 本文にフォーム、フッターにボタングループが含まれています。 通常はコンテンツの編集に使用されますが、単に情報のみを表示するために使用されることもあります。

* `dialogfieldset`

  [CQ.form.DialogFieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  DialogFieldSet は、[Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) で使用される [FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) です。

* `directstore`

  [CQ.Ext.data.DirectStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.data.DirectProxy](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) および [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) で設定された [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を作成して、[CQ.Ext.Direct](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) サーバーサイドの [Provider](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) とのやり取りを容易にする小さなヘルパークラス。

* `displayfield`

  [CQ.Ext.form.DisplayField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  検証されることも送信されることもない、表示専用のテキストフィールド。

* `editbar`

  [CQ.wcm.EditBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  EditBar は、ユーザーがバーのボタンを使用してコンテンツを編集できるようにします。

  ここには記載されていませんが、EditBar には、[CQ.wcm.EditBase](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) のすべてのメンバーがあります。

* `editor`

  [CQ.Ext.Editor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  要求に応じて表示／非表示を処理し、いくつかのビルトインのサイズ変更およびイベント処理ロジックを持つ基本エディターフィールド。

* `editorgrid`

  [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  このクラスは、[GridPanel クラス](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を拡張し、選択した[列](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)でセルを編集できるようにします。編集可能な列は、[列の設定](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)で[エディター](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を提供することで指定されます。

* `editrollover`

  [CQ.wcm.EditRollover](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  EditRollover は、ユーザーがダブルクリックすることでコンテンツを編集できるようにし、コンテキストメニューを通じてさらに編集操作を提供します。編集可能な領域は、マウスがコンテンツにロールオーバーされたときに、フレームによって示されます。

* `feedimporter`

  [CQ.wcm.FeedImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FeedImporter は、ユーザーが RSS／Atom フィードをインポートし、フィードエントリごとにページを作成できるようにします。

* `field`

  [CQ.Ext.form.Field](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  フォームフィールドの基底クラスであり、デフォルトのイベントの処理、サイズ設定、値の処理およびその他の機能を提供します。

* `fieldset`

  [CQ.Ext.form.FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [フォーム](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)内のアイテムのグループ化に使用される標準コンテナ。

* `fileuploaddialogbutton`

  [CQ.form.FileUploadDialogButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadDialogButton は、FileUploadField を使用してファイルをアップロードするための新しいダイアログボックスを開くボタンを作成します。 別のフォームでアップロードする必要がある、編集ダイアログボックス内で使用できます。

* `fileuploadfield`

  [CQ.form.FileUploadField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadField は、ユーザーがアップロードする単一のファイルを選択できるようにします。

* `findreplacedialog`

  [CQ.wcm.FindReplaceDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FindReplaceDialog は、ページおよびその子ページ内のトークンを検索して置換するためのダイアログ・ボックスです。

* `flash`

  [CQ.Ext.FlashComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `grid`

  [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  このクラスは、行と列の表形式でデータを表示する、コンポーネントをベースにしたグリッドコントロールのプライマリインターフェイスを表示します。

* `groupingstore`

  [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  利用可能なフィールドの 1 つでレコードをグループ化できるようにする、専用のストア実装。[CQ.Ext.grid.GroupingView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) と共に使用して、グループ化された GridPanel のデータモデルを証明します。

* `heavymovedialog`

  [CQ.wcm.HeavyMoveDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HeavyMoveDialog は、ページとその子ページを移動するためのダイアログボックスであり、以前アクティブ化したページの再アクティブ化も考慮に入れます（「heavy」移動）。

* `hidden`

  [CQ.Ext.form.Hidden](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  フォームの送信で渡す必要があるフォーム内の非表示の値を格納するための、基本的な非表示フィールド。

* `historybutton`

  [CQ.HistoryButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HistoryButton は、前後のボタンを簡単に提供する小さなヘルパークラスです。 通常、2 つの関連インスタンスが必要になります。進むボタンのインスタンスは、履歴を処理する戻るボタンのインスタンスに関連付けられたシンプルなボタンです。

* `htmleditor`

  [CQ.Ext.form.HtmlEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  軽量のHTML エディターコンポーネントを提供します。 Safari では、一部のツールバー機能をサポートしていないので、必要に応じて自動的に非表示になります。 必要に応じて、設定オプションに記載されます。

  エディターのツールバーボタンには、[buttonTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) プロパティで定義されたツールチップがあります。

* `iframedialog`

  [CQ.IframeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  iframe のコンテンツを表示し、iframe でフォームを許可するプレーンダイアログボックス。

* `iframepanel`

  [CQ.IframePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  iframe を含むパネル。iframe の作成、iframe の読み込みイベント、iframe のコンテンツへのアクセスを簡単にします。

* `inlinetextfield`

  [CQ.form.InlineTextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  InlineField は、フォーカスされていないときにラベルとして表示されるテキストフィールドです。

* `jsonstore`

  [CQ.Ext.data.JsonStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  JSON データからの [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s の作成を容易にする小さなヘルパークラス。 JsonStore には自動的に [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) が設定されます。

* `label`

  [CQ.Ext.form.Label](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

   基本ラベルフィールド。

* `languagecopydialog`

  [CQ.wcm.LanguageCopyDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LanguageCopyDialog は、言語ツリーをコピーするためのダイアログボックスです。

* `linkchecker`

  [CQ.wcm.LinkChecker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  linkchecker は、サイト内の外部リンクを確認するためのツールです。

* `listview`

  [CQ.Ext.list.ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CQ.Ext.list.ListView は、[Grid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) に似たビューの高速かつ軽量の実装です。

* `livecopyproperties`

  [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LiveCopyProperties は、ライブコピープロパティ（関係の継承、同期のトリガー、同期操作）を表示および編集できるパネルを提供します。

* `lvbooleancolumn`

  [CQ.Ext.list.BooleanColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ブーリアン型のデータフィールドをレンダリングする Column 定義クラスです。詳しくは、[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 設定オプションを参照してください。

* `lvcolumn`

  [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  このクラスは、[ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の初期化に使用される列設定データをカプセル化します。

* `lvdatecolumn`

  [CQ.Ext.list.DateColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  デフォルトのロケールまたは設定された[形式](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)に従って渡された日付をレンダリングする Column 定義クラスです。詳しくは、[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 設定オプションを参照してください。

* `lvnumbercolumn`

  [CQ.Ext.list.NumberColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [形式](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)の文字列に従って数値データフィールドをレンダリングする Column 定義クラスです。詳しくは、[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 設定オプションを参照してください。

* `mediabrowsedialog`

  [CQ.MediaBrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **非推奨：代わりに[コンテンツファインダー](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を使用して、メディアを参照してください。**

  MediaBrowseDialog は、メディアライブラリを参照するためのダイアログボックスです。

* `menu`

  [CQ.Ext.menu.Menu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニューオブジェクト。メニュー項目を追加できるコンテナ。 Menu は、別のコンポーネントをベースにした特殊なメニュー（[CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) など）が必要な場合に、基底クラスとしても利用できます。

  メニューには、[&#x200B; メニュー項目 &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) または一般的な [&#x200B; コンポーネント &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を含めることができます。

* `menubaseitem`

  [CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニューにレンダリングするすべてのアイテムの基本クラス。BaseItem は、すべてのメニューコンポーネントで共有される、デフォルトのレンダリング、アクティベートされた状態の管理、基本設定オプションを提供します。

* `menucheckitem`

  [CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  デフォルトでチェックボックス（ラジオグループの一部である可能性もあります）を含むメニュー項目が追加されます。

* `menuitem`

  [CQ.Ext.menu.Item](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニュー関連の機能（サブメニューなど）を必要とし、静的表示アイテムではないすべてのメニューアイテムの基底クラス。Item は、メニュー専用のアクティベーションとクリック処理を追加することで、[CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の基本機能を拡張します。

* `menuseparator`

  [CQ.Ext.menu.Separator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニューに区切りバーを追加します。区切りバーは、メニュー項目を論理的なグループに分けるために使用されます。 通常は、add （）を呼び出す際に「–」を使用するか、直接作成するのではなく項目設定で「–」を使用して追加します。

* `menutextitem`

  [CQ.Ext.menu.TextItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  見出しまたはグループ区切りとして使用される静的テキスト文字列をメニューに追加します。

* `metadata`

  [CQ.dam.form.Metadata](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Metadata` には、例えばアセットエディターページで使用されるメタデータフィールドに必要な情報を決定するための一連のフィールドが用意されています。

  以下のフィールドを提供します。

* `multifield`

  [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  複数値のプロパティを編集するための編集可能なフォームフィールドのリストが `MultiField` に表示されます。

* `mvt`

  [CQ.form.MVT](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  多変量分析テストコンポーネントは、バナーの代わりに表示される画像のセットを定義および編集するのに使用されます。クリックスルー率の統計はバナーごとに収集されます。

* `notificationinbox`

  [CQ.wcm.NotificationInbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `NotificationInbox` を使用すると、ユーザーは WCM アクションをサブスクライブし、通知を管理できます。

* `numberfield`

  [CQ.Ext.form.NumberField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  自動でのキーストロークのフィルター処理および数値の検証を提供する数値テキストフィールド。

* `offlineimporter`

  [CQ.wcm.OfflineImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OfflineImporter` は、Microsoft® Word ドキュメントをAEM ページに読み込んで変換するツールです。 この機能により、ワード プロセッサを使用してオフラインでコンテンツを編集することができます。

* `ownerdraw`

  [CQ.form.OwnerDraw](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OwnerDraw` には、カスタム HTML コードを含めることができます（直接入力するか、URL から取得します）。

* `paging`

  [CQ.Ext.PagingToolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  レコードの量が増えるにつれて、ブラウザーでレンダリングするのに要する時間も増えます。Paging は、クライアントとやり取りするデータの量を減らすために使用されます。

* `panel`

  [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `panel` は、特定の機能と構造コンポーネントを備えたコンテナで、アプリケーション指向のユーザーインターフェイスに最適な構築ブロックです。

  パネルは、その継承により、[CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) から取得されます。

* `paragraphreference`

  [CQ.form.ParagraphReference](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  段落の参照フィールドでは、ページを閲覧したり、段落の 1 つを選択したりできます。トリガーフィールドおよび関連する段落の参照ダイアログボックスで構成されます。

* `password`

  [CQ.form.Password](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Password` は [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) に似ていますが、ユーザーが機密データを入力できるように、値を非公開に保ちます。

* `pathcompletion`

  [CQ.form.PathCompletion](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **非推奨：代わりに [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用してください。**

* `pathfield`

  [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PathField` は、パス完了を含むパス用に設計された入力フィールドと、サーバーリポジトリを参照するための [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を開くためのボタンです。 高度なリンク作成のために、ページの段落を参照することもできます。

* `progress`

  [CQ.Ext.ProgressBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  更新可能な進行状況バーコンポーネント。進行状況バーは、手動と自動の 2 つの異なるモードをサポートします。

  手動モードでは、独自のコードから必要に応じて進行状況バーを表示、更新（[updateProgress](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用）、削除する必要があります。この方法は操作の間中、進行状況を表示する必要がある場合に最も適しています。

* `propertygrid`

  [CQ.Ext.grid.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  開発 IDE によくあるような従来型のプロパティグリッドを模した、専用のグリッドの実装。グリッドの各列には、いくつかのオブジェクトのプロパティが表示され、このデータは [CQ.Ext.grid.PropertyRecord](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) に名前／値のペアのセットとして格納されます。

* `propgrid`

  [CQ.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PropertyGrid` は、オブジェクトのプロパティを表示および編集するために使用される汎用グリッドです。

* `quicktip`

  [CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `@xtype quicktip` - マークアップで指定され、グローバル [CQ.Ext.QuickTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) インスタンスによって自動的に管理されるツールチップのための専用のツールチップクラス。 その他の使用方法の詳細と例については、QuickTips クラスのヘッダーを参照してください。

* `radio`

  [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  単一の `radio` フィールド。 チェックボックスと同じですが、入力の種類が自動的に設定されるので便利です。グループ内の各ラジオボタンに同じ名前を付けると、ブラウザーによってラジオボタンが自動的にグループ化されます。


* `radiogroup`

  [CQ.Ext.form.RadioGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

   [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) コントロールのグループ化コンテナ。

* `referencesdialog`

  [CQ.wcm.ReferencesDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `ReferencesDialog` は、ページ上に参照を表示するためのダイアログボックスです。

* `restoretreedialog`

  [CQ.wcm.RestoreTreeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RestoreTreeDialog` は、ツリーの以前のバージョンを復元するためのダイアログボックスです。

* `restoreversiondialog`

  [CQ.wcm.RestoreVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  RestoreVersionDialog は、ページの以前のバージョンを復元するためのダイアログボックスです。

* `richtext`

  [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RichText` には、スタイル設定されたテキスト情報（リッチテキスト）を編集するためのフォームフィールドが用意されています。

  `RichText` コンポーネントは、現在、次の機能を提供しています。

* `rolloutplan`

  [CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  RolloutPlan は、ページロールアウトの進行状況を監視するためのダイアログボックスを提供します。 [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) が RolloutPlan を開始します。

* `rolloutwizard`

  [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RolloutWizard` は、ページをロールアウトするためのウィザードを提供します。 RolloutWizard は、[CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を開始します。

* `searchfield`

  [CQ.form.SearchField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SearchField` には「検索」フィールドがあります。このフィールドでは、結果がドロップダウンリストに表示され、リポジトリの検索に使用できます。

* `selection`

  [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Selection` を使用すると、ユーザーは複数のオプションの中から選択できます。 オプションは、設定の一部にすることも、JSON 応答から読み込むこともできます。 選択は、ドロップダウン（選択）またはコンボボックス（選択してフリーテキストエントリを追加）のいずれかでレンダリングできます。

* `sidekick`

  [CQ.wcm.Sidekick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Sidekick` は、ページ編集のための一般的なツールをユーザーに提供するフローティングヘルパーです。

* `siteadmin`

  [CQ.wcm.SiteAdmin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteAdmin` は、WCM 管理機能を提供するコンソールです。

* `siteimporter`

  [CQ.wcm.SiteImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteImporter` を使用すると、ユーザーは完全な web サイトを読み込み、最初のプロジェクトを作成できます。

* `sizefield`

  [CQ.form.SizeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SizeField` を使用すると、ユーザーは幅と高さを入力できます（画像の場合など）。

* `slider`

  [CQ.Ext.Slider](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  垂直方向または水平方向、キーボードの調節、設定可能なスナップ、軸のクリックおよびアニメーションをサポートする Slider。任意のコンテナに項目として追加できます。 例：使用法：...

* `slideshow`

  [CQ.form.Slideshow](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  スライドショーコンポーネントを使用すると、一連の画像および画像タイトルを定義して編集できます。 ユーザーは、このセットをスライドショーとして表示できます。

  Slideshow コンポーネントは、[CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) コンポーネントをベースとします。

* `smartfile`

  [CQ.form.SmartFile](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartFile はインテリジェントファイルアップローダーです。

  Flash のプラグイン（バージョン 9 以上）がインストールされている場合、アップロードは、アップロードの便利な処理方法を提供する SWFupload ライブラリを使用して実行されます。

* `smartimage`

  [CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartImage はインテリジェント画像アップローダーです。アップロードされた画像を処理するツールを提供します。画像マップや画像のトリミングを定義するツールを提供します。

  このコンポーネントは、別のダイアログボックスのタブで使用するように設計されています。

* `spacer`

  [CQ.Ext.Spacer](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  レイアウトでサイズ変更可能なスペースを提供するために使用されます。

* `spinner`

  [CQ.form.Spinner](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Spinner` は、数値、日付、または時刻値のトリガーフィールドです。 この値は、提供された上下トリガー、スクロールホイールまたはキーを使用して増減させることができます。

* `splitbutton`

  [CQ.Ext.SplitButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ボタンのデフォルトのクリックイベントとは別に、イベントを発生させることのできる組み込みのドロップダウン矢印を提供する `splitbutton` ール。 通常は、プライマリボタンのアクションに追加のオプションを提供するドロップダウンメニューの表示に使用されますが、カスタムハンドラーによって `arrowclick` 実装を提供できます。

* `static`

  [CQ.Static](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Static` は、任意のテキストまたはHTMLを表示するために使用できます。

* `statistics`

  [CQ.wcm.Statistics](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Statistics` は、ページインプレッション数をグラフとして表示します。 このウィジェットでは、統計を表示する期間を選択できます。

* `store`

  [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Store` クラスは、[GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) などのコンポーネントの入力データを提供する [Record](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) オブジェクトのクライアントサイドキャッシュをカプセル化します。

* `suggestfield`

  [CQ.form.SuggestField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SuggestField` は、入力に基づいた候補をユーザーに提供します。

* `switcher`

  [CQ.Switcher](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Switcher` は、コンソール内のヘッダーバー用のボタングループを提供し、web サイト、デジタルAssets、ツール、ワークフローおよびセキュリティを切り替えることができます。

* `tableedit`

  [CQ.form.TableEdit](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **非推奨：代わりに [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用してください。**

* `tableedit2`

  [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  この `TableEdit2` は、テーブルを作成するためのウィジェットを提供します。

* `tabpanel`

  [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本のタブコンテナ。TabPanel は、レイアウトを目的として、標準の [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) と同じように使用できますが、子コンポーネントを含めるための特別なサポートもあります（[`items`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)）。

* `tags`

  [CQ.tagging.TagInputField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ```
  CQ.tagging.TagInputField
  ```

   は、タグを入力するためのフォームウィジェットです。既存のタグから選択できるポップアップメニューを備えており、オートコンプリートなどの機能もあります。

* `textarea`

  [CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  multiline（テキストフィールド）従来の `textarea` フィールドの直接の置き換えとして使用できるほか、自動サイズ設定のサポートが追加されます。

* `textbutton`

  [CQ.TextButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TextButton` は、[CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の機能を備えたテキストリンクを提供します。

* `textfield`

  [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本テキストフィールド。従来のテキスト入力と直接置き換えて使用できます。また、より高度な入力コントロール（[CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) など）の基底クラスとして使用できます。

* `thumbnail`

  [CQ.form.Thumbnail](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `timefield`

  [CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  時間ドロップダウンと自動時刻検証機能を備えた時間入力フィールドが用意されています。 使用例：...

* `tip`

  [CQ.Ext.Tip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype tip は、[CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) と [CQ.Ext.Tooltip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の基底クラスであり、すべてのヒントベースのクラスで必要な基本のレイアウトと配置を提供します。このクラスは、静的に配置されたシンプルなヒントに直接使用できます。

* `titleseparator`

  [CQ.menu.TitleSeparator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニューに区切りバーを追加します。区切りバーは、メニュー項目を論理的なグループに分けるために使用されます。 このセパレーターには、タイトルを追加することもできます。

* `toolbar`

  [CQ.Ext.Toolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本の `Toolbar` クラス。 ツールバーの [`defaultType`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) は [`button`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) ですが、ツールバー要素（ツールバーコンテナの子アイテム）には、ほとんどのタイプのコンポーネントを使用できます。 Toolbar の要素は、そのコンストラクターを使用して明示的に作成できます。

* `tooltip`

  [CQ.Ext.ToolTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ターゲット要素をポイントしたときに追加情報を提供するための標準 `tooltip` 実装。 @xtype tooltip。

* `treegrid`

  [CQ.tree.TreeGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype `treegrid`

* `treepanel`

  [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TreePanel` は、ツリー構造のデータをツリー構造 UI として表示できます。

  [&#x200B; に追加さ &#x200B;](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) た `TreePanel`TreeNode には、アプリケーションで使用されるメタデータをそれぞれ [attributes](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) プロパティに含めることができます。

* `trigger`

  [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  クリック可能なトリガーボタン（デフォルトでは、コ `TextFields` ボボックスに似ています）を追加する便利なラッパーを提供します。 トリガーにはデフォルトのアクションが設定されていないので、[onTriggerClick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を上書きすることで、トリガークリックハンドラーを実装するための関数を割り当てる必要があります。コンボボックスと同じようにレンダリングされるので、`TriggerField` を直接作成できます。

* `uploaddialog`

  [CQ.UploadDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `UploadDialog` を使用すると、ユーザーはリポジトリにファイルをアップロードでき、新しい UploadDialog を作成します。

* `userinfo`

  [CQ.UserInfo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  現在のユーザー名を表示するツールバーアイテムであり、ユーザーがプロパティや権限借用の編集などの操作を行えるようにします。

* `viewport`

  [CQ.Ext.Viewport](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  表示可能なアプリケーションの領域（ブラウザービューポート）を表す専用のコンテナ。

  `Viewport` はドキュメントの本文に合わせて自動的にレンダリングされ、ブラウザーのビューポートのサイズに合わせて自動的にサイズ調整され、ウィンドウのサイズ変更を管理します。 作成できるビューポートは 1 つだけです。

* `window`

  [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  アプリケーションウィンドウとして使用するための専用のパネル。デフォルトでは、ウィンドウはフローティング表示され、[サイズ変更可能](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)かつ[ドラッグ可能](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)です。ウィンドウは、ビューポートいっぱいまで[最大化](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、前のサイズを復元、および[最小化](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)できます。

* `xmlstore`

  [CQ.Ext.data.XmlStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  XML データからの [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)s の作成を容易にする小さなヘルパークラス。 `XmlStore` は、[CQ.Ext.data.XmlReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) で自動的に設定されます。

  `cqinclude` - リポジトリ内の別のパスのウィジェットの定義を含む疑似 xtype。 ページダイアログボックスで最も一般的に使用されます。 実際には、この xtype の JavaScript ウィジェットクラスは存在しません。`CQ.Util` クラスは、`formatData()` 関数を使用して処理します。
