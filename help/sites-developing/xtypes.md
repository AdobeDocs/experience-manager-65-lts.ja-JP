---
title: xtypeの使用（クラシック UI）
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
source-wordcount: '6205'
ht-degree: 73%

---

# xtypeの使用（クラシック UI）{#using-xtypes-classic-ui}

このページでは、Adobe Experience Manager（AEM）で利用できるすべての xtype について説明します。

ExtJS 言語では、xtype はクラスに付与されるシンボル名です。 xtype とその使用方法について詳しくは、[ExtJS 2 の概要](https://docs.sencha.com/)の「Component XTypes」の段落を参照してください。

AEMで使用可能なすべてのウィジェットについて詳しくは、[widget API ドキュメント ](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を参照してください。

特定のxtypeがAEMで使用されているコンポーネントを調べるには、CRXDEで次の`Xpath` クエリを使用できます。 「checkbox」を興味のあるxtypeに置き換えるだけです：

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

  `Annotation`は特別なウィンドウです。 本文にフォームがあり、フッターにボタングループがあります。 通常はコンテンツの編集に使用されますが、単に情報のみを表示するために使用されることもあります。

* `arraystore`

  [CQ.Ext.data.ArrayStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  以前は`SimpleStore`と呼ばれていました。

  配列データから[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を簡単に作成するための小さなヘルパークラス。 `ArrayStore`は、[CQ.Ext.data.ArrayReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)で自動的に設定されます。

* `asseteditor`

  [CQ.dam.AssetEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Asset Editor`はDAM管理者で使用されています。

* `assetreferencesearchdialog`

  [CQ.wcm.AssetReferenceSearchDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `AssetReferenceSearchDialog`は、ページがアセットまたはタグを参照する場合にポップアップ表示されるダイアログボックスです。

* `blueprintconfig`

  [CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BlueprintConfig`には、ブループリントのライブコピーを表示し、このブループリントプロパティを編集するためのパネルが用意されています（同期トリガーと同期アクション）。

* `blueprintstatus`

  [CQ.wcm.msm.BlueprintStatus](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BlueprintStatus は、ブループリントとライブコピーの関係を表示および編集できるパネルを提供します。 [CQ.wcm.msm.BlueprintStatus.Tree](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用してブラウジングし、[CQ.wcm.msm.BlueprintConfig](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) および [CQ.wcm.msm.LiveCopyProperties](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用して編集します。

* `box`

  [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [コンポーネント](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)の基底クラスであり、幅と高さを使用して、ボックスとしてサイズを変更します。

  BoxComponent は、サイズと位置を自動的に調整するボックスモデルを提供し、コンポーネントのレンダリングモデルで正常に動作します。

* `browsedialog`

  [CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BrowseDialog により、ユーザーはパスを選択するためにリポジトリを参照できます。 通常は、[BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) で使用されます。

* `browsefield`

  [CQ.form.BrowseField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **非推奨：代わりに [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用してください。**

* `bulkeditor`

  [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `BulkEditor`には、検索結果を編集するための検索エンジンとグリッドが用意されています。

  `BulkEditor`はHTML フォームに挿入する必要があります（読み込み機能で必要）。 [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) で適切に動作します。

* `bulkeditorform`

  [CQ.wcm.BulkEditorForm](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  BulkEditorForm は、HTML フォームで囲まれた [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を提供します。 [CQ.wcm.BulkEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)のスタンドアロン バージョン。 「読み込み」ボタンにはHTML フォームが必要です。

* `button`

  [CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  シンプルな Button クラス

* `buttongroup`

  [CQ.Ext.ButtonGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ボタングループのためのコンテナ。

* `chart`

  [CQ.Ext.chart.Chart](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  CQ.Ext.chart パッケージは、Flash ベースのグラフを使用したデータの視覚化を実現します。 各グラフは、CQ.Ext.data.Store に直接バインドされ、グラフの自動更新が可能になります。 グラフの外観を変更するには、[chartStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) および [extraStyle](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の設定オプションを確認します。

* `checkbox`

  [CQ.Ext.form.Checkbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  単一チェックボックスフィールド。 従来のチェックボックスフィールドにそのまま置き換えて使用できます。

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

  色を選択するためのシンプルなカラーパレットクラス。 パレットはどのコンテナにもレンダリングできます。

* `combo`

  [CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  オートコンプリート、リモートローディング、ページングなど、その他多くの機能をサポートするコンボボックスコントロール。

  ComboBox は、従来の HTML &lt;select>フィールドと同じように動作します。 相違点として、[valueField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を送信するために、非表示の入力フィールドを作成する [hiddenName](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を指定する必要があります。

* `component`

  [CQ.Ext.Component](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  すべての`Ext` コンポーネントの基本クラス。 コンポーネントのすべてのサブクラスは、[Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) クラスが提供する作成、レンダリング、破棄の自動`Ext` コンポーネントライフサイクルに参加できます。 コンポーネントは、コンテナ作成時に、[items](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 設定オプションでコンテナに追加されます。

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

  その他のコンポーネントを含められる [CQ.Ext.BoxComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の基底クラス。 コンテナは、アイテムの格納の基本動作（アイテムの追加、挿入、削除など）を処理します。

  最もよく使用される Container クラスは、[CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) および [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) です。

* `contentfinder`

  [CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinder は、左に実際のコンテンツファインダー、右にコンテンツフレームを含む、2 列の専用の[ビューポート](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)です。

* `contentfindertab`

  [CQ.wcm.ContentFinderTab](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ContentFinderTab は、[CQ.wcm.ContentFinder](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) のタブパネルで使用される機能を提供する専用のパネルです。 通常は、検索フォーム（クエリボックス）と、検索を表示するデータビューが用意されています。

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

  CustomContentPanelは、[CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)で使用するための特別なパネルです。そのコンテンツは、ダイアログボックスの他のフィールドとは異なるURLから取得され、送信されます。

* `cycle`

  [CQ.Ext.CycleButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 要素のメニューを含む専用の SplitButton。 ボタンは、クリックごとに各メニュー項目を自動的に切り替え、ボタンの[change](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) イベントを上げます（または、ボタンの[changeHandler](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)関数を呼び出す場合は、指定します）。

* `dataview`

  [CQ.Ext.DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  カスタムレイアウトテンプレートと書式設定を使用してデータを表示するメカニズム。 DataView は、内部テンプレートのメカニズムとして [CQ.Ext.XTemplate](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用し、[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) にバインドされます。ストア内のデータが変更されると、ビューは変更を反映して自動的に更新されます。

* `datefield`

  [CQ.Ext.form.DateField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.DatePicker](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) ドロップダウンと自動日付検証を使用して、日付入力フィールドを提供します。

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

  ダイアログは特別なウィンドウです。 本文にフォームがあり、フッターにボタングループがあります。 通常はコンテンツの編集に使用されますが、単に情報のみを表示するために使用されることもあります。

* `dialogfieldset`

  [CQ.form.DialogFieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  DialogFieldSet は、[Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) で使用される [FieldSet](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) です。

* `directstore`

  [CQ.Ext.data.DirectStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.data.DirectProxy](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)と[CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)で構成された[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を作成するための小さなヘルパークラスは、[CQ.Ext.Direct](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) サーバーサイド [ プロバイダー](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)との対話を容易にします。

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

  このクラスは、[GridPanel クラス](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を拡張し、選択した[列](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)でセルを編集できるようにします。 編集可能な列は、[列の設定](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)で[エディター](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を提供することで指定されます。

* `editrollover`

  [CQ.wcm.EditRollover](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  EditRollover は、ユーザーがダブルクリックすることでコンテンツを編集できるようにし、コンテキストメニューを通じてさらに編集操作を提供します。 編集可能な領域は、マウスがコンテンツにロールオーバーされたときに、フレームによって示されます。

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

  FileUploadDialogButtonは、FileUploadFieldを介してファイルをアップロードするための新しいダイアログボックスを開くボタンを作成します。 アップロードが別のフォームで行われる必要がある編集ダイアログボックス内で使用できます。

* `fileuploadfield`

  [CQ.form.FileUploadField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FileUploadField は、ユーザーがアップロードする単一のファイルを選択できるようにします。

* `findreplacedialog`

  [CQ.wcm.FindReplaceDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  FindReplaceDialogは、ページとその子ページ内のトークンを検索して置換するためのダイアログボックスです。

* `flash`

  [CQ.Ext.FlashComponent](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `grid`

  [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  このクラスは、行と列の表形式でデータを表示する、コンポーネントをベースにしたグリッドコントロールのプライマリインターフェイスを表示します。

* `groupingstore`

  [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  利用可能なフィールドの 1 つでレコードをグループ化できるようにする、専用のストア実装。 [CQ.Ext.grid.GroupingView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)と共に使用して、グループ化されたGridPanelのデータモデルを証明します。

* `heavymovedialog`

  [CQ.wcm.HeavyMoveDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HeavyMoveDialogは、ページとその子ページを移動するためのダイアログボックスで、以前にアクティブ化されたページの再アクティブ化（「重い」移動）も検討します。

* `hidden`

  [CQ.Ext.form.Hidden](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  フォームの送信で渡す必要があるフォーム内の非表示の値を格納するための、基本的な非表示フィールド。

* `historybutton`

  [CQ.HistoryButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  HistoryButtonは、戻るボタンと進むボタンを簡単に提供するための小さなヘルパークラスです。 通常、2 つの関連インスタンスが必要になります。進むボタンのインスタンスは、履歴を処理する戻るボタンのインスタンスに関連付けられたシンプルなボタンです。

* `htmleditor`

  [CQ.Ext.form.HtmlEditor](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  軽量なHTML エディターコンポーネントを提供します。 Safariでは、一部のツールバー機能がサポートされていないため、必要に応じて自動的に非表示になります。 必要に応じて、設定オプションに注意してください。

  エディターのツールバーボタンには、[buttonTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) プロパティで定義されたツールチップがあります。

* `iframedialog`

  [CQ.IframeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  iframeの内容を表示し、iframe内のフォームを許可するプレーンダイアログボックス。

* `iframepanel`

  [CQ.IframePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  iframe を含むパネル。 iframeの簡単な作成、iframeの読み込みイベント、およびiframeのコンテンツへの簡単なアクセスを提供します。

* `inlinetextfield`

  [CQ.form.InlineTextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  InlineField は、フォーカスされていないときにラベルとして表示されるテキストフィールドです。

* `jsonstore`

  [CQ.Ext.data.JsonStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  JSON データから[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を簡単に作成するための小さなヘルパークラス。 JsonStore には自動的に [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) が設定されます。

* `label`

  [CQ.Ext.form.Label](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本ラベルフィールド。

* `languagecopydialog`

  [CQ.wcm.LanguageCopyDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  LanguageCopyDialogは、言語ツリーをコピーするためのダイアログボックスです。

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

  ブーリアン型のデータフィールドをレンダリングする Column 定義クラスです。 詳しくは、[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 設定オプションを参照してください。

* `lvcolumn`

  [CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  このクラスは、[ListView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の初期化に使用される列設定データをカプセル化します。

* `lvdatecolumn`

  [CQ.Ext.list.DateColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  デフォルトのロケールまたは設定された[形式](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)に従って渡された日付をレンダリングする Column 定義クラスです。 詳しくは、[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 設定オプションを参照してください。

* `lvnumbercolumn`

  [CQ.Ext.list.NumberColumn](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [形式](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)の文字列に従って数値データフィールドをレンダリングする Column 定義クラスです。 詳しくは、[CQ.Ext.list.Column](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の [xtype](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) 設定オプションを参照してください。

* `mediabrowsedialog`

  [CQ.MediaBrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **非推奨：代わりに[コンテンツファインダー](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を使用して、メディアを参照してください。**

  MediaBrowseDialogは、メディアライブラリを参照するためのダイアログボックスです。

* `menu`

  [CQ.Ext.menu.Menu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニューオブジェクト。 メニュー項目を追加できるコンテナ。 メニューは、別のコンポーネント（[CQ.Ext.menu.DateMenu](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)など）に基づく専用メニューを必要とする場合にも、基本クラスとして機能します。

  メニューには、[ メニュー項目](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)または一般[ コンポーネント ](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)のいずれかを含めることができます。

* `menubaseitem`

  [CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニューにレンダリングするすべてのアイテムの基本クラス。 BaseItem は、すべてのメニューコンポーネントで共有される、デフォルトのレンダリング、アクティベートされた状態の管理、基本設定オプションを提供します。

* `menucheckitem`

  [CQ.Ext.menu.CheckItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  デフォルトではチェックボックスを含むメニュー項目が追加されますが、ラジオグループの一部にすることもできます。

* `menuitem`

  [CQ.Ext.menu.Item](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニュー関連の機能（サブメニューなど）を必要とし、静的表示アイテムではないすべてのメニューアイテムの基底クラス。 Item は、メニュー専用のアクティベーションとクリック処理を追加することで、[CQ.Ext.menu.BaseItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の基本機能を拡張します。

* `menuseparator`

  [CQ.Ext.menu.Separator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニュー項目の論理グループを分割するために使用されるメニューにセパレーターバーを追加します。 通常、add （）の呼び出しまたはitems設定で&quot;-&quot;を使用して、直接作成するのではなく、1つを追加します。

* `menutextitem`

  [CQ.Ext.menu.TextItem](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニューに静的なテキスト文字列を追加し、見出しまたはグループ区切り記号として使用します。

* `metadata`

  [CQ.dam.form.Metadata](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Metadata`には、アセットエディターページなどで使用されるメタデータフィールドに必要な情報を決定するための一連のフィールドが用意されています。

  以下のフィールドを提供します。

* `multifield`

  [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `MultiField`は、複数値のプロパティを編集するためのフォームフィールドの編集可能なリストです。

* `mvt`

  [CQ.form.MVT](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  多変量分析テストコンポーネントは、バナーの代わりに表示される画像のセットを定義および編集するのに使用されます。 クリックスルー率の統計はバナーごとに収集されます。

* `notificationinbox`

  [CQ.wcm.NotificationInbox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `NotificationInbox`を使用すると、ユーザーはWCM アクションを購読し、通知を管理できます。

* `numberfield`

  [CQ.Ext.form.NumberField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  自動でのキーストロークのフィルター処理および数値の検証を提供する数値テキストフィールド。

* `offlineimporter`

  [CQ.wcm.OfflineImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OfflineImporter`は、Microsoft® Word ドキュメントを読み込み、AEM ページに変換するためのツールです。 この機能により、ワード プロセッサを使用してオフラインでコンテンツを編集することができます。

* `ownerdraw`

  [CQ.form.OwnerDraw](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `OwnerDraw`には、カスタム HTML コードを含めることができます（直接入力するか、URLから取得するか）。

* `paging`

  [CQ.Ext.PagingToolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  レコードの量が増えるにつれて、ブラウザーでレンダリングするのに要する時間も増えます。 Paging は、クライアントとやり取りするデータの量を減らすために使用されます。

* `panel`

  [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `panel`は、アプリケーション指向のユーザーインターフェイスに最適な構成要素となる、特定の機能と構造コンポーネントを持つコンテナです。

  パネルは、継承により、[CQ.Ext.Container](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)から取得されます。

* `paragraphreference`

  [CQ.form.ParagraphReference](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  段落の参照フィールドでは、ページを閲覧したり、段落の 1 つを選択したりできます。 トリガーフィールドおよび関連する段落の参照ダイアログボックスで構成されます。

* `password`

  [CQ.form.Password](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Password`は[CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)に似ていますが、その値は非公開のままであるため、ユーザーは機密データを入力できます。

* `pathcompletion`

  [CQ.form.PathCompletion](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **非推奨：代わりに [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用してください。**

* `pathfield`

  [CQ.form.PathField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PathField`は、パス補完を持つパス用に設計された入力フィールドであり、サーバーリポジトリを参照するために[CQ.BrowseDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を開くボタンです。 高度なリンク作成のために、ページの段落を参照することもできます。

* `progress`

  [CQ.Ext.ProgressBar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  更新可能な進行状況バーコンポーネント。 進行状況バーは、手動と自動の 2 つの異なるモードをサポートします。

  手動モードでは、独自のコードから必要に応じて進行状況バーを表示、更新（[updateProgress](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用）、削除する必要があります。 この方法は操作の間中、進行状況を表示する必要がある場合に最も適しています。

* `propertygrid`

  [CQ.Ext.grid.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  開発 IDE によくあるような従来型のプロパティグリッドを模した、専用のグリッドの実装。 グリッドの各列には、いくつかのオブジェクトのプロパティが表示され、このデータは [CQ.Ext.grid.PropertyRecord](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) に名前／値のペアのセットとして格納されます。

* `propgrid`

  [CQ.PropertyGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `PropertyGrid`は、オブジェクトのプロパティを表示および編集するために使用される汎用グリッドです。

* `quicktip`

  [CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `@xtype quicktip` - マークアップで指定でき、グローバル [CQ.Ext.QuickTips](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) インスタンスによって自動的に管理される、ツールヒント専用のツールチップクラスです。 その他の使用方法の詳細と例については、QuickTips クラスのヘッダーを参照してください。

* `radio`

  [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  単一の`radio` フィールド。 チェックボックスと同じですが、入力の種類が自動的に設定されるので便利です。 ブラウザーは、グループ内の各ラジオボタンが同じ名前を使用する場合、ラジオボタンを自動的にグループ化します。


* `radiogroup`

  [CQ.Ext.form.RadioGroup](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  [CQ.Ext.form.Radio](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) コントロールのグループ化コンテナ。

* `referencesdialog`

  [CQ.wcm.ReferencesDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `ReferencesDialog`は、ページ上の参照を表示するためのダイアログボックスです。

* `restoretreedialog`

  [CQ.wcm.RestoreTreeDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RestoreTreeDialog`は、ツリーの以前のバージョンを復元するためのダイアログボックスです。

* `restoreversiondialog`

  [CQ.wcm.RestoreVersionDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  RestoreVersionDialogは、ページの以前のバージョンを復元するためのダイアログボックスです。

* `richtext`

  [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RichText`には、スタイル設定されたテキスト情報（リッチテキスト）を編集するためのフォームフィールドが用意されています。

  現在、`RichText` コンポーネントには次の機能があります。

* `rolloutplan`

  [CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ロールアウトプランには、ページのロールアウトの進行状況を確認するためのダイアログボックスが表示されます。 [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)がRolloutPlanを開始します。

* `rolloutwizard`

  [CQ.wcm.msm.RolloutWizard](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `RolloutWizard`には、ページをロールアウトするためのウィザードが用意されています。 RolloutWizard は、[CQ.wcm.msm.RolloutPlan](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を開始します。

* `searchfield`

  [CQ.form.SearchField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SearchField`には、リポジトリの検索に使用できるドロップダウンリストの結果を提供する検索フィールドが用意されています。

* `selection`

  [CQ.form.Selection](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Selection`では、ユーザーは複数のオプションを選択できます。 オプションは、設定の一部にすることも、JSON応答から読み込むこともできます。 選択範囲は、ドロップダウン（選択）またはコンボボックス（選択+自由テキストエントリ）としてレンダリングできます。

* `sidekick`

  [CQ.wcm.Sidekick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Sidekick`は、ユーザーにページ編集用の共通ツールを提供するフローティング ヘルパーです。

* `siteadmin`

  [CQ.wcm.SiteAdmin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteAdmin`は、WCM管理機能を提供するコンソールです。

* `siteimporter`

  [CQ.wcm.SiteImporter](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SiteImporter`を使用すると、ユーザーは完全なweb サイトを読み込み、最初のプロジェクトを作成できます。

* `sizefield`

  [CQ.form.SizeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SizeField`を使用すると、ユーザーは幅と高さを入力できます（例：画像の場合）。

* `slider`

  [CQ.Ext.Slider](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  垂直方向または水平方向、キーボードの調節、設定可能なスナップ、軸のクリックおよびアニメーションをサポートする Slider。 任意のコンテナにアイテムとして追加できます。 例えば、使用状況：...

* `slideshow`

  [CQ.form.Slideshow](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  スライドショーコンポーネントを使用すると、一連の画像と画像タイトルを定義および編集できます。 ユーザーは、セットをスライドショーとして表示できます。

  Slideshow コンポーネントは、[CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) コンポーネントをベースとします。

* `smartfile`

  [CQ.form.SmartFile](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartFile はインテリジェントファイルアップローダーです。

  Flash のプラグイン（バージョン 9 以上）がインストールされている場合、アップロードは、アップロードの便利な処理方法を提供する SWFupload ライブラリを使用して実行されます。

* `smartimage`

  [CQ.form.SmartImage](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  SmartImage はインテリジェント画像アップローダーです。 アップロードされた画像を処理するツールを提供します。画像マップや画像のトリミングを定義するツールを提供します。

  コンポーネントは、別のダイアログボックスタブで使用するように設計されています。

* `spacer`

  [CQ.Ext.Spacer](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  レイアウトでサイズ変更可能なスペースを提供するために使用されます。

* `spinner`

  [CQ.form.Spinner](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Spinner`は、数値、日付または時刻の値のトリガーフィールドです。 指定された上下トリガー、スクロールホイール、またはキーを使用することで、値を増減できます。

* `splitbutton`

  [CQ.Ext.SplitButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ボタンの既定のクリック イベントとは別にイベントを起動できる組み込みのドロップダウン矢印を提供する`splitbutton`です。 通常は、プライマリボタンアクションに追加のオプションを提供するドロップダウンメニューを表示するために使用されますが、任意のカスタムハンドラーで`arrowclick`実装を提供できます。

* `static`

  [CQ.Static](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Static`は、任意のテキストまたはHTMLの表示に使用できます。

* `statistics`

  [CQ.wcm.Statistics](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Statistics`は、ページのインプレッションをグラフとして表示します。 このウィジェットでは、統計を表示する期間を選択できます。

* `store`

  [CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Store` クラスは、[GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[DataView](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)などのコンポーネントに入力データを提供する[Record](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) オブジェクトのクライアント側キャッシュをカプセル化します。

* `suggestfield`

  [CQ.form.SuggestField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `SuggestField`は、ユーザーの入力に基づいて提案をユーザーに提供します。

* `switcher`

  [CQ.Switcher](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `Switcher`には、Web サイト、デジタル Assets、ツール、ワークフロー、セキュリティを切り替えるためのヘッダーバーのボタングループがコンソールに用意されています。

* `tableedit`

  [CQ.form.TableEdit](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  **非推奨：代わりに [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を使用してください。**

* `tableedit2`

  [CQ.form.TableEdit2](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TableEdit2`には、テーブルを作成するためのウィジェットが用意されています。

* `tabpanel`

  [CQ.Ext.TabPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本のタブコンテナ。 TabPanel は、レイアウトを目的として、標準の [CQ.Ext.Panel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) と同じように使用できますが、子コンポーネントを含めるための特別なサポートもあります（[`items`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)）。

* `tags`

  [CQ.tagging.TagInputField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ```
  CQ.tagging.TagInputField
  ```

  は、タグを入力するためのフォームウィジェットです。 既存のタグから選択するためのポップアップメニューがあり、自動補完やその他の多くの機能が含まれています。

* `textarea`

  [CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  multiline（テキストフィールド） 従来の`textarea` フィールドの直接置き換えとして使用できるほか、自動サイズ変更のサポートも追加されています。

* `textbutton`

  [CQ.TextButton](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TextButton`は、[CQ.Ext.Button](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)の機能を備えたテキストリンクを提供します。

* `textfield`

  [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本テキストフィールド。 従来のテキスト入力と直接置き換えて使用できます。また、より高度な入力コントロール（[CQ.Ext.form.TextArea](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、[CQ.Ext.form.ComboBox](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) など）の基底クラスとして使用できます。

* `thumbnail`

  [CQ.form.Thumbnail](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

* `timefield`

  [CQ.Ext.form.TimeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  時間ドロップダウンと自動時間検証を備えた時間入力フィールドを提供します。 使用例：...

* `tip`

  [CQ.Ext.Tip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype tip は、[CQ.Ext.QuickTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) と [CQ.Ext.Tooltip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) の基底クラスであり、すべてのヒントベースのクラスで必要な基本のレイアウトと配置を提供します。 このクラスは、静的に配置されたシンプルなヒントに直接使用できます。

* `titleseparator`

  [CQ.menu.TitleSeparator](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  メニュー項目の論理グループを分割するために使用されるメニューにセパレーターバーを追加します。 このセパレーターには、タイトルを追加することもできます。

* `toolbar`

  [CQ.Ext.Toolbar](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  基本`Toolbar` クラス。 ツールバーの[`defaultType`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)は[`button`](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)ですが、ツールバー要素（ツールバーコンテナの子アイテム）は、ほぼすべてのタイプのコンポーネントにすることができます。 Toolbar の要素は、そのコンストラクターを使用して明示的に作成できます。

* `tooltip`

  [CQ.Ext.ToolTip](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  ターゲット要素にカーソルを合わせたときに追加情報を提供するための標準の`tooltip`実装。 @xtype tooltip。

* `treegrid`

  [CQ.tree.TreeGrid](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  @xtype `treegrid`

* `treepanel`

  [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `TreePanel`は、ツリー構造化データのツリー構造化UI表現を提供します。

  `TreePanel`に追加された[TreeNode](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)sには、アプリケーションで使用されているメタデータをそれぞれ[属性](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) プロパティに含めることができます。

* `trigger`

  [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  クリック可能なトリガーボタンを追加する`TextFields`の便利なラッパーを提供します（デフォルトではコンボボックスのように見えます）。 トリガーにはデフォルトのアクションが設定されていないので、[onTriggerClick](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) を上書きすることで、トリガークリックハンドラーを実装するための関数を割り当てる必要があります。 コンボボックスとまったく同じようにレンダリングされるので、`TriggerField`を直接作成できます。

* `uploaddialog`

  [CQ.UploadDialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  `UploadDialog`を使用すると、ユーザーはリポジトリにファイルをアップロードできます。新しいUploadDialogを作成します。

* `userinfo`

  [CQ.UserInfo](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  現在のユーザー名を表示するツールバーアイテムであり、ユーザーがプロパティや権限借用の編集などの操作を行えるようにします。

* `viewport`

  [CQ.Ext.Viewport](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  表示可能なアプリケーションの領域（ブラウザービューポート）を表す専用のコンテナ。

  `Viewport`はドキュメント本文にレンダリングされ、ブラウザーのビューポートのサイズに合わせて自動的にサイズ調整し、ウィンドウのサイズ変更を管理します。 作成できるビューポートは 1 つだけです。

* `window`

  [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  アプリケーションウィンドウとして使用するための専用のパネル。 デフォルトでは、ウィンドウはフローティング表示され、[サイズ変更可能](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)かつ[ドラッグ可能](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)です。 ウィンドウは、ビューポートいっぱいまで[最大化](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)、前のサイズを復元、および[最小化](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)できます。

* `xmlstore`

  [CQ.Ext.data.XmlStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)

  XML データから[CQ.Ext.data.Store](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)を簡単に作成するための小さなヘルパークラス。 `XmlStore`は、[CQ.Ext.data.XmlReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html)で自動的に設定されます。

  `cqinclude` - リポジトリ内の別のパスからのウィジェット定義を含む疑似xtype。 これは、ページダイアログボックスで最もよく使用されます。 実際には、この xtype の JavaScript ウィジェットクラスは存在しません。 `CQ.Util` クラスは`formatData()`関数を使用して処理します。
