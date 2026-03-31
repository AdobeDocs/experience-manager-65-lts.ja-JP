---
title: Adobe Experience Manager 6.5 LTS、SP2の現在のリリースノート
description: Adobe Experience Manager 6.5 LTS、サービスパック 2 の最新のリリース情報について説明します。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: b5a8f555-c061-4fe2-a100-cc01335959cb
source-git-commit: a3d1ebd3e1c4adba80fb63f0138d662a6d056cc6
workflow-type: tm+mt
source-wordcount: '6403'
ht-degree: 20%

---

# Adobe Experience Manager 6.5 LTS、SP2の現在のリリースノート {#release-notes}

## リリース情報 {#release-information}

| 製品 | [!DNL Adobe Experience Manager] 6.5 LTS |
|---|---|
| バージョン | サービスパック 2 （SP2） <!-- UPDATE FOR EACH NEW RELEASE --> |
| タイプ | サービスパックのリリース |
| 日付 | 2026年2月19日<!-- UPDATE FOR EACH NEW RELEASE --> |
| ダウンロード URL | [ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack-lts/cq-quickstart-6.6.2.jar) |


<!-- UPDATE ABOVE FOR EACH NEW RELEASE -->

>[!IMPORTANT]
>
> **必須のホットフィックス** - SP2をインストールする際のオフラインのコンパクションに関するSNFE （SegmentNotFoundException）の問題を回避するには、[既知の問題 – オンラインのコンパクション中のリポジトリの破損](#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146)に記載されているホットフィックスをインストールします。

## [!DNL Adobe Experience Manager] 6.5 LTS、SP2に含まれるもの {#what-is-new}

<!-- UPDATE EACH RELEASE -->

[!DNL Experience Manager] 6.5 LTS、SP2には、新機能、顧客が要求する主な機能強化、バグ修正が含まれています。 また、2025年3月の 6.5 LTS の公開当初以降にリリースされたパフォーマンス、安定性、セキュリティの改善も含まれています。6.5 LTS で[このサービスパックをインストール](#install-update)します。

## 主な機能と機能強化

**AEM Sites**

AEM 6.5 LTS SP2には、[&#x200B; コンテンツフラグメントとモデル管理](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/65lts/)および[&#x200B; ローンチ &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/stable/sites/launches/)のOpenAPIが含まれるようになりました。 これらのAPIは、コンテンツフラグメントへのアクセスと、オーサリングとスケジューリングのためのローンチを提供します。 AEM as a Cloud Serviceと同じ最新のOpenAPIを使用しています。


<!-- UPDATE THE EACH RELEASE -->

## 6.5 LTS、サービスパック 2 で修正された問題 {#fixed-issues}

### [!DNL Sites]{#sites-65-LTS-SP2}

#### アクセシビリティ {#sites-accessibility-65-lts-sp2}

* 作成者が編集中にコンポーネントブラウザーにアイテムをホバーすると、テキストコンポーネントはキーボードフォーカスを失いました。 これは入力を混乱させ、WCAG 3.2.1下でのアクセシビリティの失敗を引き起こしました。この修正により、ホバーのスタイル設定がフォーカスの移動を防ぎ、コンポーネントブラウザーのインタラクション中にテキストコンポーネントがフォーカスされたままになります。 （SITES-35370）
* 「説明」リッチテキストフィールドのフォーカス管理が修正され、タブキーで進むナビゲーションがブロックされるようになりました。 コンポーネントが非標準のキーボードコマンドを使用してフォーカスを移動し、想定していたダイアログボックスのナビゲーションが壊れたため、ユーザーがRTEで行き詰まるようになりました。 この変更により、標準のキーボード操作が適用され、ダイアログボックス全体で論理タブの順序が維持されます。 （SITES-35228）
* サイトエディターで、ページオーサリング中に想定される動作が中断され、コンポーネントのインタラクションに一貫性がなくなった問題を修正しました。 作成者は、信頼性の低いUI応答を経験し、標準的な編集タスクを妨げ、ワークフロー効率が低下しました。 このアップデートにより、基礎となるエディターロジックが改良され、影響を受けるコンポーネント間で安定した予測可能なインタラクションが復元されます。 （SITES-35227）
* ページエディターのアセットセレクターが破損し、特定のページ編集シナリオで読み込まれなかったリグレッション。 作成者は、ページの編集中にアセットを選択または参照する際に、通常どおりアセットセレクターを開いて使用できるようになりました。 この変更により、読み込みエラーが中断したアセット選択ワークフローへの一貫したアクセスが復元されます。 （SITES-35226）
* ページのインタラクション中に一貫性のない動作を引き起こし、標準オーサリングワークフローが中断するサイトエディターの問題を修正しました。 この欠陥により、コンポーネントの設定やコンテンツの更新を妨げる予期しないUI応答が発生しました。 このアップデートにより、影響を受ける機能が安定し、ページ間の編集アクションの信頼性の高い実行が復元されます。 （SITES-35225）
* ページ編集中に一貫性のない動作を引き起こし、通常のワークフローに影響を及ぼすSites オーサリングインターフェイスの欠陥を排除しました。 作成者は、コンポーネントのインタラクションとコンテンツの更新を妨げる予期しないUI応答に遭遇しました。 更新により、影響を受ける機能が安定し、編集シナリオ全体で信頼性の高い予測可能な動作が復元されます。 （SITES-35224）
* AEM Sitesでは、ADAおよびWCAGの要件を満たすために、画像に`alt`個のテキストがサポートされるようになりました。 ページ出力で`alt`属性が省略されなくなったため、スクリーンリーダーは正しい代替テキストを受け取ります。 （SITES-27153）
* `Note Add` ツールバーのレイアウトを修正し、追加ボタンがビューポート幅320 ピクセルのタイトルと重ならなくなりました。 小さな画面のリフローが改善され、400% ズーム中もコントロールを読みやすく使用できるようになりました。 （SITES-25376）
* リンク選択ダイアログボックスのエラーに関するスクリーンリーダーの通知が見つからない問題を修正しました。 UIがステータスメッセージコンテナを通じてエラーテキストを公開するようになったので、NVDAはメッセージが表示されるとすぐにメッセージを読み取ります。 （SITES-25368）
* サイドレールのアセットリストからARIA グリッドとグリッドセルの役割を削除しました。 標準リストのセマンティクスとキーボードのフォーカス順序を復元し、スクリーンリーダーのナビゲーションを改善し、追加のタブストップを減らしました。 （SITES-25361）
* サイドレール Assetsのフォーカス シーケンスを修正しました。 キーボードユーザーは、一貫したタブパスを通じて、編集を含むあらゆるアセットアクションにリーチできるようになりました。 （SITES-25360）
* Search Assets モーダルのビューポート幅が320 pxのレイアウト オーバーフローを修正しました。 モーダルコンテンツがリフローされ、読みやすくなったため、コントロールがダイアログボックスに重なったり、オーバーランしたりしなくなります。 （SITES-25330）
* 「編集」ボタンのNVDA出力を修正しました。 NVDAは、「プレビューボタンが押された」のではなく、編集アクションを通知するようになりました。 （SITES-25320）
* 無音または汎用スクリーンリーダー出力の原因となる名前のないデモグラフィックツールバーテキスト入力を修正しました。 各入力には、明確なラベルベースのアクセス可能な名前が表示され、キーボードとアシスタントテクノロジーのナビゲーションが改善されました。 （SITES-25316）
* レイアウトプレビューナビゲーション時のデモグラフィックツールバーのキーボードフォーカス順序を修正しました。 タブナビゲーションが、セカンダリツールバーにスキップすることなく、デモグラフィックボタンからツールバーコントロールに直接移動するようになりました。 （SITES-25305）
* 「レイアウトを編集」ルーラーの「小さいScreens」および「タブレット」ラベルの誤ったアナウンス順序を修正しました。 スクリーンリーダーは、ページレイアウトと一致する適切な定規マーカーでこれらのラベルを読み上げるようになりました。 （SITES-25291）
* 200%のズームで編集レイアウトツールバーのオーバーフローを修正しました。 コンテンツはビューポート内に残り、スクロールしても到達できるようになりました。 （SITES-25288）
* 注釈オーバーレイのフォーカス順序が正しくなくなりました。 キーボードタブで、オーバーレイコントロールと注釈項目を順に切り替えられるようになりました。 親ページは、オーバーレイの後ろからフォーカスを受けなくなりました。 （SITES-25282）
* 固定スウォッチポップオーバーフォーカス処理。 ダイアログボックスが明確な見出しにフォーカスを移動し、そのエントリポイントでスクリーンリーダー出力を開始するようになりました。 NVDAは、ダイアログボックス全体のコンテンツをシーケンスから読み取らなくなりました。 （SITES-25275）
* 日付選択のクローズ後のタイムワープモーダルフォーカス処理を修正しました。 `Escape`が日付選択ボタンにフォーカスを返すようになりました。 日付選択では、日付選択コントロールの横にある入力フィールドにフォーカスが置かれるようになり、フォーカスの損失とバックグラウンドページへのアクセスが防止されました。 （SITES-25264）
* 注釈を削除ダイアログボックスのキーボードフォーカス処理を修正しました。 キャンセルは、16進値の確認コントロールではなく、ダイアログボックスを開いた`Delete` コントロールにフォーカスを返すようになりました。 キャンセル後に、スクリーンリーダーが無関係なダイアログボックスのコンテンツを通知しなくなりました。 （SITES-25258）
* 注釈モーダルダイアログボックスのフォーカス処理を修正しました。 ダイアログボックスを開くと、ダイアログボックスの見出しにフォーカスが設定され、NVDAがカンバスコンテンツと無関係なダイアログボックスのテキストを読み取れなくなります。 キーボードナビゲーションは、閉じるまでダイアログボックス内に留まるようになりました。 （SITES-25257）
* 320 px幅での検索モーダルレイアウトの問題を修正しました。 モーダルコンテンツがクリーンにリフローされ、ツリーディレクトリとの重複が回避されるようになりました。 ユーザーは結果を表示し、コントロールが見えにくくすることなくディレクトリを移動できます。 （SITES-25246）
* テキストの間隔を広げた後でモーダルテキストを検索しても、クリップが表示されなくなりました。 ツリーのディレクトリレイアウトが明確に分離されるようになったため、ラベルとエントリが読みやすくなりました。 ユーザーは、テキストの重複やカットオフを回避しながら、検索とナビゲーションを完了できます。 （SITES-25245）
* 「注釈を終了」ボタンではなく、キーボードフォーカスを注釈コンテンツに移動するようになりました。 タブの順序は論理的な順序に従い、リバースナビゲーションなしで関連するコントロールに到達できます。 （SITES-25241）
* 日付と終了の設定タイムワープリンクには、キーボードナビゲーション中に表示されるフォーカスインジケーターがありませんでした。 UIでコントラストの高い明確なフォーカススタイルがレンダリングされ、アクティブリンクを一目で特定できるようになりました。 （SITES-25232）
* ティーザーモーダルヘッダーは、キーボードユーザーがダイアログを移動するのをブロックしなくなりました。 キーボードコントロールで操作をピックアップ、移動、ドロップできるようになり、スクリーンリーダーの使いやすさと全体的な操作性が向上しました。 （SITES-25226）
* AEMでは、「ティーザーモーダル情報」ボタンに意味のあるアクセシブルラベルが使用されるようになりました。 スクリーンリーダーは、デフォルトのアイコンの代替テキスト文字列ではなく、明確なアクション名を表示します。 （SITES-25223）
* ユーザーが「編集」ボタンをアクティブ化すると、スクリーンリーダーに正しいアクションが通知されるようになりました。 NVDAは、「プレビューボタンが押された」という報告を行わなくなり、キーボードナビゲーション中に誤解を招くフィードバックと混乱が発生しました。 （SITES-25208）
* 左レールを展開すると、キーボードのフォーカスが最初の左レール コントロールに移動するようになりました。 タブシーケンスがセカンダリツールバーにジャンプしたり、ミッドライストに移動したりしなくなったため、キーボードユーザーは逆ナビゲーションなしで左レールコンテンツに到達できるようになりました。 （SITES-24998）
* デバイスエミュレーターバーのコンテンツが、320 px ビューポート幅で完全に表示されたままになりました。 ツールバーのテキストとコントロールは、切り捨てではなく回り込みになり、重なりを減らし、読みやすさを向上させます。 （SITES-24953）
* AEMでは、エミュレーターツールバーにiPhone デバイスラベルが表示されるようになりました。 テキストがデフォルトの幅で切り捨てられなくなり、読みやすさとデバイス選択の明瞭性が向上しました。 （SITES-24952）
* リスト表示テーブルヘッダーで、ARIAを通じてソート状態が公開されるようになりました。 列の並べ替えアクションの後に、スクリーンリーダーが昇順または降順をアナウンスします。 （SITES-24943）
* AEMで、テキスト間隔の変更時にカードビューで「その他のアクション」メニューラベルの表示が保持されるようになりました。 メニューオプションは、クイック公開を含む完全なテキストを保持し、WCAG テキスト間隔の設定中もメニューは読み取り可能です。 （SITES-24941）
* カードのアクション メニューバーで、アクセス可能な名前がカード表示で表示されるようになりました。 スクリーンリーダーはメニューバーの目的を明確に伝え、音声コントロールはコントロールを名前でターゲティングできます。 （SITES-24938）
* カードビューは、スクリーンリーダーの動作を混乱させるARIA グリッドセマンティクスに依存しなくなりました。 UIに、カードの内容とカードアクションバーに対して意味のある役割とラベルが提供されるようになりました。これにより、キーボード使用時に見逃したコントロールを減らすことができます。 （SITES-24933）
* ユーザーがツールヒント アイコンにカーソルを合わせるたびに、`Delete Modal` ツールヒントが表示されるようになりました。 フォーカスアクションに同じツールチップテキストが表示されるようになり、マウスとキーボードユーザーの繰り返しアクセスが改善されました。 （SITES-24778）
* 左側のレールのナビゲーションが、ユーザーがレールを設定した後に予想されるキーボードフォーカス順序に従うようになりました。 タブフォーカスは、画面読み上げナビゲーションの明瞭性を向上させるスイッチ表示ではなく、選択した左レール領域に表示されます。 （SITES-24754）
* ユーザー環境設定モーダルのカラースウォッチ ナビゲーション時の誤ったNVDA フィードバックを修正しました。 NVDAは、フォーカスを受け取るスウォッチのラベルを読み取り、誤解を招くようなカラー出力を削除するようになりました。 スウォッチセットで、一貫したキーボードナビゲーションとクリアな選択確認がサポートされるようになりました。 （SITES-24739）
* `Spin` コントロールの詳細なNVDA出力が減少しました。 入力ラベルが重複する冗長なグループラベルが削除され、NVDAは制御名を1回発表しました。 キーボードとスクリーンリーダーのナビゲーションで、1つの明確なアナウンスが提供されるようになりました。 （SITES-24725）
* カルーセルダイアログボックスでは、「アイテム」タブではなく、ダイアログボックスの見出しにフォーカスが置かれるようになりました。 キャンセルしてEscを実行すると、ダイアログボックスを起動したコントロールにフォーカスが復元され、詳細なNVDA出力が減少します。 （SITES-24716）
* リンク選択ダイアログで、最終レベルのツリー項目のプログラマティックラベルと画面上のラベルが整列するようになりました。 矢印キーによるナビゲーションは、各項目に対して信頼性の高いスクリーンリーダーのアナウンスをトリガーし、誤解を招くラベル出力を排除します。 （SITES-24710）
* 320 ピクセルのビューポートで、開いている選択ダイアログボックスをリンクすると、正しく表示されるようになりました。 コンテンツがモーダルや切り捨てをオーバーランしなくなり、モーダルに水平スクロールバーが表示されなくなりました。 （SITES-24709）
* 選択範囲を開いたダイアログボックスをリンクすると、閉じる、またはキャンセルした後に、キーボードフォーカスがダイアログボックストリガーに戻るようになりました。 フォーカスがリンク入力にジャンプしなくなり、スクリーンリーダーのコンテキストが安定し、追加のナビゲーションが減少しました。 （SITES-24707）
* 画像モーダルダイアログが論理的なフォーカスシーケンスに従うようになりました。 フォーカスは、キャンセル後にページのランドマークで以前のコントロールをスキップまたはドロップしなくなり、ユーザーは終了時に「設定」ボタンにフォーカスを戻します。 （SITES-24693）
* 参照レールモーダルダイアログボックスで、キーボードフォーカスがトラップされるようになりました。 Tab キーとShift キーを押しながらTab キーを押すと、ダイアログボックスコントロール内に留まり、フォーカスがページコンテンツにエスケープされなくなります。 スクリーンリーダーは、ダイアログボックスの内容のみを通知します。 （SITES-24683）
* ハイパーリンクパス選択モーダルは、開いているダイアログボックスの見出しにフォーカスを設定するようになりました。 「キャンセル」を選択すると、ダイアログボックスが閉じ、「選択ダイアログボックスを開く」ボタンにフォーカスが戻ります。これにより、フォーカスの損失とスクリーンリーダーの出力の冗長さを防ぐことができます。 （SITES-24672）
* 検索フィールドで、プレースホルダーテキストの代わりに永続的な画面上ラベルが使用されるようになりました。 ラベルは入力中も表示されたままになり、キーボード、スクリーンリーダー、および音声ユーザーの明瞭性が向上します。 （SITES-24529）
* ティーザーモーダルダイアログボックスが、開いているダイアログボックスの見出しにフォーカスを設定するようになりました。 ダイアログボックスを閉じると、`Configure` コントロールにフォーカスが戻るので、フォーカスの損失やスクリーンリーダーの出力が過剰になるのを防ぐことができます。 （SITES-24522）
* サイドレールのAssets パネルに閉じるコントロールが含まれるようになりました。 閉じると、キーボードのフォーカスがサイドレールの切替スイッチに戻り、パネルのコンテンツを強制的にタブ移動できなくなります。 （SITES-24489）
* キーボードタブが、管理テーブル内のボタンやリンクに到達するようになりました。 ユーザーは、矢印キーによるセルナビゲーションを使用してインタラクティブなコントロールを見つけることができなくなりました。 （SITES-24285）
* 画像コンポーネントダイアログボックスで、装飾的なヘルプとフルスクリーンアイコンが画像として表示されなくなりました。 スクリーンリーダーは現在、これらのアイコンをスキップして、実用的なコントロールとフィールドコンテンツに注目しています。 （SITES-2940）
* Sites管理者は、フォルダーサムネールアイコンから画像の役割を削除するようになりました。 支援テクノロジーでは、これらの装飾的な要素をスキップして、フォルダー名とアクションに注目します。 （SITES-2852）
* コンテンツツリーで、キーボードフォーカスがアクティブなツリー項目または最初のツリー項目にルーティングされるようになりました。 ツリーコンテナが空のタブ停止として機能しなくなり、Shift + Tab フォーカスのトラップが防止されます。 （SITES-1577）

#### 管理ユーザーインターフェイス{#sites-adminui-65-lts-sp2}

サイトコンソールのリスト表示設定に、リスト表示に表示される列が反映されませんでした。 ダイアログボックスが開き、チェックボックスがオフになり、選択した列の数が正しく表示されません。 修正ダイアログボックスの状態がアクティブなグリッド列と同期され、実際の列の表示と一致するようにカウンターが更新されます。 （SITES-38576）

#### クラシックユーザーインターフェイス{#sites-classicui-65-lts-sp2}

アップグレード後にリッチテキストではなく、生のHTML タグを表示するクラシック UI テキストコンポーネントの編集。 Service Pack 2は、クラシック UI RTE （リッチテキストエディター）のレンダリングを修正し、エディターに書式設定されたコンテンツが表示され、保存されたマークアップが保持されるようにします。 この修正により、繰り返し編集および保存中にマークアップの拡張も停止します。 （SITES-38709）

#### [!DNL Content Fragments]{#sites-contentfragments-65-lts-sp2}

ヘッドレスイベントのサポートでは、6.5 LTSのコンテンツフラグメントとモデルに必要なOSGi イベントが不足していました。 このアップデートでは、イベントバンドルと必要な依存関係が追加され、6.5 LTS ビルドが含まれています。 コンテンツフラグメントとモデルイベントが正しく起動し、Launches API ワークフローをサポートするようになりました。 （SITES-35329）

#### [!DNL Content Fragments] - 管理者{#sites-admin-65-lts-sp2}

* ページの更新中に不規則な動作を停止するように、Sites オーサリングインターフェイスのコンポーネント処理を調整しました。 この欠陥により、編集者の予測不可能な回答が生じ、日常的なコンテンツの変更が妨げられ、ワークフロー効率が低下しました。 このアップデートにより、エディターロジックが期待されるインタラクションパターンに合わせて調整され、オーサリングアクティビティ中に信頼できるパフォーマンスが提供されます。 （SITES-35078）重大

* リグレッションにより、コンテンツフラグメントのAssets コンソールのリストビューが壊れ、リストのレンダリング中にエラーが発生しました。 このアップデートは、プレビュー情報の削除後にリスト表示ロジックを修正し、安定したリスト出力を復元します。 コンソールに失敗せずにコンテンツフラグメントが表示され、リストのインタラクションが使用可能な状態に保たれます。 （SITES-38683）
* コンテンツフラグメントエディターで、タグラベルがローカライズされるようになりました。 エディターはコレクションラベルもローカライズするので、UI テキストは選択したロケールと一致します。 （SITES-977）


#### [!DNL Content Fragments] - フラグメントエディター{#sites-fragments-editor-65-lts-sp2}

* リファクタリング後も機能トグルを無効のままにすると、コンテンツフラグメントのバリエーションのタグが消えてしまいます。 この修正により、トグルがオフのままでもバリエーションのタグのサポートが復元されます。 作成者は、コンテンツフラグメントエディターでバリエーションタグを再度追加して表示できます。 （SITES-38682）重大
* 編集済みコンテンツフラグメントエディターから作成者が戻った後、Assets コンソールリストから編集されたコンテンツフラグメントが消えました。 ブラウザーのキャッシュで古いリストが返され、更新されたフラグメントは手作業による更新まで非表示にされました。 この修正により、エディターのリターンパスにキャッシュコントロール処理が追加され、リストが正しくリロードされ、編集されたフラグメントが表示されたままになります。 （SITES-35374）重大

* コンテンツフラグメント RTEには、最近のUI スタイル変更後のレイアウトとビジュアルの問題が表示されました。 Service Pack 2では、ツールバーと編集可能な領域が正しくレンダリングされ、読み取り可能なままになるように、RTE スタイルが調整されます。 コンテンツフラグメントエディターが、ページエディターの外観と動作に合うようになりました。 （SITES-38684）
* Polaris アセットセレクターからIMS スコープを削除すると、コンテンツフラグメントと配信エンドポイントの統合が壊れました。 作成者は、リモートアセットセレクターを開いてアセットを選択すると、エラーが発生する。 このアップデートにより、必要なIMS スコープが再追加され、安定した配信層アクセスが復元されます。 （SITES-35837）
* 関連するコンテンツパネルで、ハードコードされた「未定義」プレースホルダーがレンダリングされなくなりました。 コンテンツフラグメントエディターは、ローカライゼーションリソースを通じてそのテキストを解決するようになり、エディターは翻訳されたUI テキストを確認できるようになりました。 （SITES-33675）
  <!-- REMOVED FROM BUG LIST FEBRUARY 13, 2026 * Preview error messaging now uses localized strings instead of raw `Cannot print fragment's Json` text. The Content Fragment Editor now shows translated output across locales during GraphQL endpoint resolution failures. (SITES-33666)-->
* コンテンツフラグメントエディターに、翻訳された一般タブラベルがロケールをまたいで表示されるようになりました。 エディターは、ローカライズされていないタブテキストを置き換え、タブタイトルから内部IDを削除します。 （SITES-30715）
* コンテンツフラグメントエディターに、許可されたアセットタイプの翻訳済み名前が表示されるようになりました。 作成者がコンテンツ参照の制限を設定する際に、ピッカーリストに内部文字列と英語専用ラベルが混在することがなくなりました。 （SITES-29699）

#### [!DNL Content Fragments] - GraphQL API {#sites-graphql-api-65-lts-sp2}

* フィルター実行エラーによるデプロイメントエラーを停止するために、GraphQL クエリの検証処理を調整しました。 この欠陥は、アプリケーションの起動時に例外を生成し、影響を受ける環境での正常なロールアウトをブロックしました。 このリビジョンは、一貫した検証動作を保証し、ランタイムクエリ検証の中断なしでスムーズなデプロイメントを可能にします。 （SITES-34301）重大

* GraphQL エンドポイントを編集ダイアログボックスに、ローカライズされたUI文字列が表示されるようになりました。 ダイアログボックスに「GraphQL スキーマが設定から取得されました」などの英語専用テキストが表示されなくなり、関連するラベルがロケール間で正しくレンダリングされるようになりました。 （SITES-34018）

#### [!DNL Content Fragments] - GraphQL クエリエディター{#sites-graphql-query-editor-65-lts-sp2}

* フィルター実行エラーによるデプロイメントエラーを停止するために、GraphQL クエリの検証処理を調整しました。 この欠陥は、アプリケーションの起動時に例外を生成し、影響を受ける環境での正常なロールアウトをブロックしました。 このリビジョンは、一貫した検証動作を保証し、ランタイムクエリ検証の中断なしでスムーズなデプロイメントを可能にします。 （SITES-35529）
* 設定ブラウザー名にCJK文字が含まれている場合に、GraphQL Explorerが失敗しなくなりました。 エンドポイントの作成と保存されたクエリへのアクセスは正常に機能し、GraphQL クエリエディターページでエラーが発生しなくなります。 （SITES-31616）

#### [!DNL Content Fragments] - モデル エディター{#sites-model-editor-65-lts-sp2}

* リファクタリングで機能が無効な切り替えスイッチに関連付けられたときに、ネストされたコンテンツフラグメントモデルが機能しなくなった。 この修正により、切り替えの変更を必要とせずに、ネストされたモデルのサポートが復元されます。 作成者は、モデルエディターでネストされたモデルを再度作成して使用できます。 （SITES-38681）重大

* コンテンツフラグメントモデルのフィルターパネルで、ローカライズされていない文字列が表示されなくなりました。 AEMでは、ローカライズされたフィルターラベルとローカライズされたステータス値がすべてのロケールに表示されるようになりました。 （SITES-30863）
* コンテンツフラグメントモデルエディターが、ロック警告ダイアログボックスのローカライズされた文字列をレンダリングするようになりました。 UIは、ローカライズされていない英語のメッセージを、サポートされている言語のロケールリソースに置き換えます。 （SITES-28592）

#### [!DNL Content Fragments] - REST API{#sites-restapi-65-lts-sp2}

AEM ヘッドレスでは、メインラインビルドとの依存関係やバンドルバージョンの競合を避けるために、専用のリリースブランチが必要でした。 このアップデートでは、リリース/6.5lts ヘッドレスブランチが追加され、依存関係セットとバンドルバージョンが調整されます。 Jenkinsは、バージョンの競合なしでヘッドレスコードベースをクリーンに構築するようになりました。 （SITES-36585）

<!-- #### Component console{#sites-component-console-65-lts-sp2} -->

#### コンテンツ API{#sites-content-api-65-lts-sp2}

機能切り替え機能の欠陥により、ページ管理APIのステータスが誤って報告されました。 このアップデートでは、専用のイネーブルメントフラグが追加され、既存のトグルと一緒に評価されます。 ページ管理APIに安定したステータスが表示されるようになりました。 サイト管理APIは実験的なままです。 （SITES-39284）

#### コアバックエンド{#sites-core-backend-65-lts-sp2}

* 標準ページ編集ワークフローを中断する一貫性のない動作を解決するためのSites オーサリングエクスペリエンスの変更。 作成者は、コンポーネントのインタラクション中に予期しない結果が発生し、コンテンツの更新が妨げられ、信頼性が低下しました。 この変更により、安定したエディター動作が復元され、影響を受けるシナリオ間でオーサリングアクションが一貫して実行されます。 （SITES-35162）重大

* コンポーネントのインタラクション中にページ編集が中断され、結果に一貫性がない問題を解決するために、Sites オーサリングの動作を調整しました。 コンテンツの更新を妨げ、ワークフローの信頼性を低下させる予期しないUI応答が発生しました。 この変更により、安定したエディター状態の管理が復元され、影響を受けるシナリオをまたいでオーサリングアクションが予測可能に実行されます。 （SITES-34499）

<!--
#### Core Components{#sites-core-components-65-lts-sp2}

#### Campaign integration{#sites-campaign-integration-65-lts-sp2}

#### Experience Fragments{#sites-experiencefragments-65-lts-sp2}

#### Foundation Components (Legacy){#sites-foundation-components-legacy-65-lts-sp2}
-->

#### ローンチ{#sites-launches-65-lts-sp2}

* Sites タイムラインに、ローンチのプロモーション中にハードコードされた英語テキストが表示されました：「ローンチを促進する前にバージョンを作成しました…」 この更新により、ハードコードされた文字列がローカライズされたメッセージ処理に置き換えられます。 タイムラインにローカライズされたテキストが表示され、AEMの標準的なローカライズ動作にエントリが整列するようになりました。 （SITES-39157）
* 作成者が「現在のページとサブページを昇格」を使用してサブセクションを昇格すると、ローンチの昇格範囲がドリフトされます。 AEMでは、無関係なページもプロモーションされ、ライブサイトの予期しない変更が生じました。 この修正により、選択したサブツリーのみがプロモートされるように、ローンチ範囲の計算が修正されます。 （SITES-38315）
* ローンチ内のコンテンツフラグメントは`damAssetLucene` インデックスに参加せず、検索結果とクエリの効率が制限されました。 この変更により、ローンチコンテンツフラグメントのパスがインデックス定義に追加されます。 検索とカスタムクエリで、`/content/launches`の下にコンテンツフラグメントが見つかるようになりました。 （SITES-35634）
* 製品がタッチ UIでコンテンツフラグメントの起動を公開しなくても、起動UIにコンテンツフラグメントの起動コントロールが表示される。 この変更により、コンテンツフラグメント Launch コードのパスがcq-launches-contentから削除され、Launch リストのフィルタリングが調整されます。 作成者は、コンテンツフラグメントの起動エントリを使用せずに、ページの起動オプションを一貫して確認できるようになりました。 （SITES-35633）
* AEM 6.5 LTS クイックスタートには、必要なローンチバンドルと前提条件が不足しており、Launches OpenAPIの有効化がブロックされていました。 このアップデートでは、Launch バンドルと、指標のサポート、DAM-cfm アップデート、キュー設定などの必要な依存関係が追加されます。 ローンチ APIは、必要なランタイムコンポーネントが存在する6.5 LTS クイックスタートで実行されるようになりました。 （SITES-35297）
* CF Launchでは、新しい依存関係バージョンと不要なGraphQL ライブラリがパッケージ化され、AEM 6.5 LTSの統合が複雑になりました。 この変更により、依存関係のバージョンがAEM 6.5 LTS ベースラインと一致し、未使用のGraphQLの依存関係が削除されます。 バンドルの解決が一貫し、CF Launchesの起動が安定したままになりました。 （SITES-35295）
* AEM Launchesで、6.5 LTS ブランチ用の専用のJenkins パイプラインが実行されるようになりました。 パイプラインは夜間に実行され、失敗アラートを電子メールで送信します。 これにより、テストの範囲を拡大し、リグレッションを早期に捉えることができます。 （SITES-35293）
* AEM 6.5 LTSには、調整されたアーティファクトバージョンを含む更新されたLaunches API バンドルが付属するようになりました。 バンドルは、プライマリコード行を追跡しながら、正しい6.5 LTS リリースバージョンを維持します。 このアップデートにより、6.5 LTS スタック全体でLaunch APIの使用が安定します。 （SITES-35292）
* AEM 6.5 LTSに、調整された依存関係バージョンを含む更新されたローンチコアバンドルが含まれるようになりました。 このアップデートでは、フラグメント UUIDと参照UUID データタイプに対するローンチコア処理が追加されます。 ローンチ処理が、ローンチとコンテンツフラグメントのワークフロー全体で一貫した動作を維持するようになりました。 （SITES-35290）
* 通常のページオーサリングワークフローを妨げる一貫性のない動作を解決するために、サイトエディターを調整しました。 コンテンツの更新を妨げ、編集の信頼性を低下させる予期しないコンポーネントの操作が作成者に発生しました。 この変更により、一貫したUI状態の管理が復元され、影響を受けるシナリオをまたいでオーサリングアクションが予測可能に実行されます。 （SITES-35138）
* ローカライズされたエラーテキストが、ハードコードされた`Provided path is not a launch`文字列の代わりに表示されるようになりました。 エディターが無効な起動パスを受信したときに、UIが翻訳されたメッセージを言語をまたいでレンダリングするようになりました。 （SITES-33360）
* AEM 6.5 LTSには、Launches OpenAPI サイドポート作業が含まれるようになりました。 このアップデートにより、Launch API バンドル、コンテンツパッケージ、必要なクイックスタートアーティファクトがパリティに追加され、コンテンツフラグメントは安定したCI検証を使用してOpenAPI シナリオを起動できるようになります。 （SITES-32050）
* ローンチ UIで、オーバーライドされたテンプレートラベルがローカライズされるようになりました。 テンプレートの上書きの詳細に、英語のみの文字列ではなく、翻訳されたテキストが表示されるようになりました。 （SITES-29525）
* AEMは、**Sites** > **ローンチ** > **編集**&#x200B;で見つからないローカライゼーションキーを解決しました。 ユーザーに、生の「ローンチソースリストを更新できません」という文字列ではなく、翻訳されたエラーメッセージが表示されるようになりました。 （SITES-21499）
* ローカライズされたステータスラベルとアクションが、ローカライズされたプロモーション UIに表示されるようになりました。 プレビュー領域には、英語の生の文字列ではなく、**削除済み**、**新規**、**表示**&#x200B;の翻訳テキストが表示されます。 （SITES-13540）
* ローカライズされたエラーメッセージがローカライズされたローンチ作成に表示されるようになりました。 UIに、`Unable to create launch page`、`Source root resource is not a page`、`Mandatory parameter is missing`などの生の英語文字列が表示されなくなりました。 （SITES-13085）


<!-- #### Link Checker{#sites-link-checker-65-lts-sp2} -->


#### MSM - ライブコピー{#sites-msm-live-copies-65-lts-sp2}

* 管理者は、コンテンツの変更中にMSM プッシュオン変更処理に関する可視性が制限されていました。 この修正により、MSM イベントの受信とロールアウト実行に関する詳細なログ記録が追加されます。 デバッグ出力に、実行されたイベント、変更されたコンテンツパス、変更のトリガーが表示されるようになりました。 （SITES-38029）
* AEMは、ブループリントロールアウト日フィールドのローカライゼーションレイアウトの問題を修正しました。 日付プロンプトがコントロールに適合し、`fr_FR`を含むサポートされている言語で読み取り可能な状態になりました。 （SITES-14961）

<!-- #### Page editor{#sites-pageeditor-65-lts-sp2} -->

#### レプリケーション{#sites-replication-65-lts-sp2}

ページエディターの公開で、セレクターまたはサフィックスを含むURLが処理されるようになりました。 公開されたリクエストは、セレクターまたはサフィックス URL文字列ではなくJCR ページパスを送信するようになったため、アクティベーションが完了し、コンテンツが公開されます。 レプリケーションはエラー時にエラーステータスを返すようになり、偽の「公開開始」メッセージを防ぐことができます。 （NPR-43288）

<!-- #### Rich Text Editor{#sites-rte-65-lts-sp2} -->

#### テンプレートエディター{#sites-template-editor-65-lts-sp2}

一部のロケールでは、**ツール** > **一般** > **テンプレート**&#x200B;にテンプレートのステータス テキストが垂直方向に表示されます。 「古い」ラベルがレイアウトを壊し、文字の列として読み取りました。 この修正により、テンプレートステータスのスタイルが修正され、ラベルが1本の水平線にレンダリングされます。 （SITES-36797）

#### ユニバーサルエディター {#sites-universal-editor-65-lts-sp2}

* OSGiの既定の設定が`preview=true`に設定され、ユニバーサルエディターがプレビューモードで開始されました。 このアップデートは、デフォルト値を修正し、標準の実稼動エントリ動作を復元します。 管理者がプレビューモードを明示的に有効にしない限り、ユニバーサルエディターが実稼動モードで開くようになりました。 （SITES-37193）
* ユニバーサルエディターを開くコマンドのデフォルト設定は、開発環境とステージング環境のプレビューモードです。 このコマンドはpreview=trueを追加します。これにより、作成者のチェックとプレビューコンテキストの整合性が維持され、誤って実稼動環境が開くことを回避できます。 （SITES-33839）

### [!DNL Assets]{#assets-65-lts-sp2}

Assets Relateは、スペースを含むファイル名で機能するようになりました。 更新されたRelate クライアントロジックは、スペースを含むパスを正しく処理し、リレーションの選択中に`undefined` ソースエラーを回避するようになりました。 関連ダイアログボックスが開き、UIのハングやスピナーを使用せずにリレーションを保存できるようになりました。 DAM利用者は、ファイル名を変更することなく、アセットを関連付け、導き出し、関連付けを解除することができます。 （Assets-56418）

#### [!DNL Dynamic Media]{#assets-dm-65-lts-sp2}

* 新しいDynamic Media ビデオプレーヤーの統合（ロールアウト制限） - AEM 6.6 クイックスタートで、新しいDynamic Media ビデオプレーヤーのエクスペリエンスが利用可能になりました。 この機能強化は、現在、制御されたロールアウトの一部として、初期のお客様に対してのみ有効になっています。 （Assets-60165）
* ビデオプロパティダイアログボックスの「サムネールを選択」オプションがアセットピッカーを開かず、ユーザーがビデオアセットのカスタムサムネールを選択する機能が復元される問題を解決しました。 （Assets-58926）
* Dynamic Media ビデオでは、字幕とオーディオトラックの言語ドロップダウンリストでアラビア語を選択するためのサポートが追加され、作成者はAEMでアラビア語の字幕を直接管理できるようになりました。 （Assets-61771）

<!-- #### [!DNL Dynamic Media] - Hybrid Mode {#assets-dm-hybrid-65-lts-sp2} -->

<!--
#### Forms Designer-->

### [!DNL Forms]{#forms-65-lts-sp2}


#### Forms

* JBoss EAP 8上のAEM Forms 6.5 LTS クラスターのデプロイメントでは、`domain/configuration/domain_oracle.xml`には、無効なXMLを引き起こし、Domain Controllerの起動を妨げる重複した`<security>` タグが含まれなくなりました。 （FORMS-24687）
* ターンキーアップグレードモードでは、`lc_turnkey.xml`のデータベースポートの更新がアップグレード中に正しく適用され、古いポート値を参照しなくなりました。 （FORMS-24689）
* LinuxでJBoss EAP 8.0を設定する際に、Windowsで変更されたシェルスクリプトが、CRLFの行の終了によって`/bin/sh^M: bad interpreter or $'\r': command not found` エラーを引き起こすことがなくなりました。 （FORMS-24688）
<!--
#### Forms JEE 

#### Forms Captcha {#forms-captcha-65-lts-sp2}

#### XMLFM {#forms-xmlfm-65-lts-sp2}

#### [!DNL Adaptive Forms] {#adaptive-forms-65-lts-sp2}

#### [!DNL Forms Designer] {#forms-designer-65-lts-sp2}

#### Forms Designer

#### AdaptIve Forms

#### Forms Captcha

#### Forms Management UI
-->


### 基盤 {#foundation-65-lts-sp2}

#### Apache Felix {#foundation-apachefelix-65-lts-sp2}

* Sling Resource Access Securityがバージョン 1.1.2で実行されるようになりました。複数のResourceAccessGateHandler サービスが登録されたときに、ResourceAccessSecurityImplが初期化中にClassCastExceptionをスローしなくなりました。 初期化が確実に完了し、複数のハンドラーを持つ環境での起動エラーを回避できるようになりました。 （NPR-42750）
* JMX コンソールとWeb コンソールは、コンソール CSS リソース用に`Content-Type: text/css header`を送信するようになりました。 厳格なMIME チェックによってスタイルシートの読み込みがブロックされなくなったため、`/system/console/jmx` UIは通常のスタイルでレンダリングされます。 （GRANITE-63677）
* AEMは、生成された`contributor`の`WEB-INF/resources/provisioning/model.txt` グループに対する重複したACL エントリを回避するようになりました。 WAR出力に1つの一貫したACL ブロックが含まれるようになり、レビュー中に権限の相違が混乱するのを防ぐことができます。 （GRANITE-63269）
* AEMは、バンドルの更新中にシリアル化解除ファイアウォールの設定とブロックリストをクリアしなくなります。 更新されたフィルター登録ロジックにより、アクティブなファイアウォールインスタンスが保存された設定に合わせて維持されるため、再起動しなくても保護が有効のままになります。 （GRANITE-61382）
* `NullPointerException` アクセス中にFelix Web コンソールで断続的な`/system/console` エラーがスローされなくなりました。 更新されたServiceTracker処理は、null トラッカー状態を防ぎます。 コンソールのログインとナビゲーションは、繰り返しリクエストおよび自動検証の間も安定したままです。 （GRANITE-61042）

<!--
#### Campaign{#foundation-campaign-65-lts-sp2}

#### Cloud Services{#foundation-cloudservices-65-lts-sp2}

#### Communities {#foundation-communities-65-lts-sp2}

#### Content distribution{#foundation-content-distribution-65-lts-sp2}
-->

#### CRX {#foundation-crx-65-lts-sp2}

Service Packのアップグレード後にJSP ファイルを開いたときに、CRXDE Liteに空白のタブが表示されなくなりました。 AEMには、CodeMirror コアとアドオンコードに一致するコードが同梱されるようになりました。これにより、致命的なブラウザーエラーを防ぎ、エディターを使用できます。 （GRANITE-64333）

#### Granite{#foundation-granite-65-lts-sp2}

式セキュリティバリデーターで、空またはnullのOSGi設定値が処理されるようになりました。 安全なデフォルトを適用し、空の配列を無視し、明確なログを記録します。これにより、NullPointerExceptionと予測不可能な検証結果を防ぐことができます。 （NPR-43163）

<!-- #### HTL{#foundatoin-htl-5-lts-sp2} -->

#### 統合{#foundation-integrations-65-lts-sp2}

開始日と終了日が存在する場合でも、AEMでAdobe Target アクティビティが同期されるようになりました。 Target ペイロードで、アクティビティの日付が、秒、ミリ秒、タイムゾーンを含む完全なISO 8601 タイムスタンプとして書式設定されるようになりました。 Targetは`InvalidJson.Json`様とのリクエストを拒否しなくなりました。 スケジュールされたアクティビティは、同期を解除せずに同期状態に移行するようになりました。 （CQ-4360733）

<!--
#### Jetty{#foundation-jetty-65-lts-sp2}

#### Localization{#foundation-localization-65-lts-sp2} 



#### Omnisearch{#foundation-omnisearch-65-lts-sp2}

#### Platform{#foundation-platform-65-lts-sp2}

#### Projects{#foundation-projects-65-lts-sp2}
-->

#### Oak {#foundation-oak-65-lts-sp2}

AEM 6.5 LTS サービスパック 2には、S3 コネクタ 1.60.10以降が必要です。 S3 データストア設定に`crossRegionAccess`と`mode`が含まれるようになり、管理者は必要に応じてクロスリージョンバケットアクセスを有効にし、ストレージをGCPに切り替えることができます。 `s3EndPoint`は、`s3Region`に整列された領域を想定しています。または、ドライバーがエンドポイントを生成するように空のままです。 （GRANITE-64873）


#### クイックスタート{#foundation-quickstart-65-lts-sp2}

* Slingは、包括的な用語と新しい設定のPIDを使用するように、管理ログインの許可リストを更新します。 この変更は、Sling JCR Base 3.2.0と一致しています。 （GRANITE-63756）

  **影響**

   * SlingはこれらのPIDを非推奨（廃止予定）にするため、設定から削除する必要があります。
      * ファクトリ PID: `org.apache.sling.jcr.base.internal.LoginAdminWhitelist.fragment`
      * グローバル PID: `org.apache.sling.jcr.base.internal.LoginAdminWhitelist`
これらの古い設定では、`whitelist.name`や`whitelist.bundles`などのプロパティを使用します。

   * Slingは、非推奨のPIDに対する部分的な後方互換性を提供しますが、新しい設定には使用しないでください。 代わりに、新しい`LoginAdminAllowList.*`個のPIDを使用してください。
   * 非推奨の設定と新しい設定の許可リストに加えるを同時に実行しないでください。 構成が混在すると、曖昧さが生じ、意図しない動作が生じる可能性があります。 AEM 6.5 LTS SP2に移行する場合は、非推奨のPIDを完全に削除します。

  **何をすべきか**

   1. `LoginAdminWhitelist*`個のPIDを使用する許可リスト設定を検索します。
   1. それらを適切な新しいPIDに置き換えます。

      * ファクトリ PID: `org.apache.sling.jcr.base.LoginAdminAllowList.fragment`
      * グローバル PID: `org.apache.sling.jcr.base.LoginAdminAllowList`

      詳しくは、[管理者用ログインのバンドルを許可リストに加えるするための非推奨のアプローチ &#x200B;](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html#deprecated-approach-to-allowlist-bundles-for-administrative-login)を参照してください。

* AEM 6.5 LTS SP2は、Sling、Oak、およびFelix用の基盤レイヤーバンドルセットを更新します。 これらのアップグレードにより、コアランタイムの安定性が強化され、プラットフォーム全体の依存バージョンが調整されます。 （GRANITE-61874）

<!--
#### Security{#foundation-security-65-lts-sp2}

AEM now prevents NullPointerException errors when a logged-in user lacks read access for some groups and opens the Groups tab. The tab now hides groups without access and renders group membership details without a blank or unresponsive UI. (NPR-43311) -->

#### Sling{#foundation-sling-65-lts-sp2}

AEMにSling Engine 2.16.6が追加されました。この変更により、セキュリティツールによってフラグ付けされたXSS違反が排除され、コアレンダリングの安全性と安定性が向上します。 （NPR-43105）

<!--
#### Translation{#foundation-translation-65-lts-sp2}

#### User interface{#foundation-ui-65-lts-sp2}
-->

#### WCM{#foundation-wcm-65-lts-sp2}

XLIFF形式の問題により、Java 17またはJava 21でAEM翻訳が失敗しなくなりました。 エクスポートパイプラインで、翻訳プロバイダーが受け入れる標準準拠のXLIFFが生成されるようになりました。 この変更により、翻訳ジョブの中断が取り除かれ、AEMと翻訳サービス間の予測可能なハンドオフが復元されます。 翻訳ワークフローが、サポートされているJava ランタイム間で安定した状態を維持するようになりました。 （CQ-4360217）

#### ワークフロー{#foundation-workflow-65-lts-sp2}

EmailNotificationService-Processorは、ワークフロー通知の処理中に「セグメントが見つかりません」エラーを繰り返しトリガーしなくなりました。 更新された例外処理は、SegmentNotFoundExceptionを検出し、無効な読み取りを続行する代わりに処理ループを停止します。 ワークフローの実行は安定したままであり、受信トレイや作業項目へのアクセス中にノイズがドロップするのをログに記録します。 （GRANITE-62635）




## [!DNL Experience Manager Foundation] について {#experience-manager-foundation}

[!DNL Adobe Experience Manager] 6.5 LTS のプラットフォームは、アップデートバージョンの OSGi ベースのフレームワーク（Apache Sling および Apache Felix）と Java™ コンテンツリポジトリの Apache Jackrabbit Oak 1.68.x 上に構築されています。

クイックスタートのサーブレットエンジンとして Eclipse Jetty 11.0.x が使用されます。

### Java™ サポート  {#java-support}

* Java™ 17 および Java™ 21 のサポート。
* 最適なパフォーマンスを得るには、デフォルトの GC 値を他の値に置き換えてください。詳しくは、[インストールとアップデート](/help/sites-deploying/custom-standalone-install.md)の節を参照してください。
* アドビでは、Oracle から公開されていない場合、AEM 関連プロジェクトで顧客が使用できるように Java™ 17 および Java™ 21 のメンテナンスアップデートを配布します。

### Uberjar パッケージ {#uber-jar-packaging}

UberJar for AEM 6.5 LTS SP2では、AEM 6.5 LTS UberJar バージョン 6.6.2が使用されています。対応するUberJar アーティファクトは、Maven中央リポジトリから取得できます。 AEM 6.5とは異なり、AEM 6.5 LTSでは、公開APIと非推奨APIを2つの異なるアーティファクトに分離しています。

パブリック APIに対してコンパイルするには、次のコマンドを使用します。

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.2</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

コードが非推奨のAPIにも依存している場合は、次を追加します。

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.6.2</version>
    <classifier>deprecated-apis</classifier>
    <scope>provided</scope>
</dependency>
```

[AEM Uber Jar バージョンの更新](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)も参照してください。

### アップグレード {#upgrade}

* アップグレードの手順について詳しくは、 [アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。
* アップグレード手順について詳しくは、[JEE上のAEM Forms 6.5 LTS SP1のアップグレードガイド &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-65-lts/content/forms/upgrade-aem-forms/upgrade)を参照してください

#### AEM 6.5 LTS サービスパックのアップグレードに関するベストプラクティス

<!-- THE INFORMATION UNDER THIS HEADING CAME FROM CQDOC-23078 -->

**環境**
適用対象：AEM 6.5 LTS （オンプレミス）のお客様によるService Pack 2 （SP2）のインストール。 SP2はクイックスタート JARとして配信されます。

**なぜこれが重要なのか**
AEM 6.5 LTS用のSP2には、パッケージ マネージャーを介してインストールするZIP ファイルではなく、クイックスタート JARとして同梱されます。 オンプレミスのお客様は、クイックスタート JAR を置き換え、解凍して再起動することでアップグレードできます。この方法は、アドビのインプレースアップグレード手順と一致しています。

**推奨アップグレードフロー（オーサーまたはパブリッシュ）**

1. AEM 6.5 LTS インスタンスが正常でアクセス可能であることを確認します。
1. ソフトウェア配布からクイックスタート JAR （例：`cq-quickstart-6.6.x.jar`）をダウンロードします。
1. 実行中のインスタンスを停止します。
1. AEM インストールディレクトリ（`crx-quickstart/`外）で、以前のクイックスタート JARをSP2 JARに置き換えます。
1. JAR を解凍します。

   ```java
   java -jar cq-quickstart-6.6.x.jar -unpack
   ```

   （必要に応じてヒープフラグを調整します。）

1. 解凍された JAR の名前を、役割とポートに一致するように変更します（例：`cq-author-4502.jar` または `cq-publish-4503.jar`）。
1. AEM を起動し、UI（ヘルプ／バージョン情報）とログでアップグレードを確認します。

**良好なハイジーン**

* 実稼動前に、下位／テスト環境でアップグレードを実行します。
* 開始する前に、完全で復元可能なバックアップ（リポジトリと外部データストア）を作成します。
* アドビのインプレースアップグレードガイダンスと技術要件（LTS の場合は Java 17/21 を推奨）を確認します。

>[!NOTE]
>
>上記のファイル名（例：`cq-quickstart-6.6.x.jar`）は、このLTS リリースで観察されたクイックスタートのアーティファクトの命名規則を反映しています。ソフトウェア配布からダウンロードしたファイル名と同じものを常に使用してください。

## インストールとアップデート{#install-update}

設定要件について詳しくは、[インストール手順](/help/sites-deploying/custom-standalone-install.md)を参照してください。

>[!NOTE]
>
> 古い6.5 SPからLTS SP1に直接アップグレードする場合は、6.5から6.5 LTS GA [&#x200B; アップグレード &#x200B;](/help/sites-deploying/upgrade.md)の指示に従ってください。


手順について詳しくは、[アップグレードドキュメント](/help/sites-deploying/upgrade.md)を参照してください。

>[!NOTE]
>
> AEM 6.5 LTS の新規インストールの場合、インデックス定義を個別にインストールする必要があります。 詳しくは、[このページ](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#index-definitions)を参照してください。

## AEM Forms アドオンのインストールとアップデート {#install-update-aem-forms-add-on}

手順について詳しくは、[インプレースアップグレードの実行](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/release-notes/aem-forms-current-service-pack-installation-instructions)を参照してください。


## サポートされているプラットフォーム {#supported-platforms}

サポートしているプラットフォーム（サポートレベルを含む）の完全な一覧表は、[AEM 6.5 LTS の技術要件](/help/sites-deploying/technical-requirements.md)を参照してください。

>[!NOTE]
>
>AEM 6.5 LTS で使用するバージョンとしては、Java™ 17／Java™ 21 をお勧めします。


## 廃止される機能および削除された機能 {#deprecated-and-removed-features}

<!-- CARRY OVER EACH RELEASE -->

Adobeでは、従来型の機能を近代化または置き換えることで、より大きな顧客価値を提供するために、製品の能力を継続的にレビューおよび進化させています。 これらの変更は、後方互換性を考慮して慎重に実装されます。

透明性を確保し、適切な計画を立てるために、AdobeはAdobe Experience Manager（AEM）の非推奨プロセスに従います。

* 非推奨が最初に発表されます。 非推奨（廃止予定）の機能は引き続き利用できますが、強化はされていません。
* 削除は、次のメジャーリリースより前に行われます。 削除スケジュールは個別にお知らせします。
* 機能が削除される前に、お客様がサポート対象の代替案に移行するために、最低1回のリリースサイクルが提供されます。

### 廃止される機能 {#deprecated-features}

この節では、AEM 6.5 LTS で廃止される機能の一覧を示します。通常、アドビでは今後のリリースで機能を削除する前に機能を非推奨（廃止予定）にし、代替手段を提供します。

現在のデプロイメントでその機能を利用しているかどうかを確認し、提示される代替手段を使用するように実装を変更するための計画を立てることをお勧めします。

| 領域 | 機能 | 代替手段 | バージョン（SP） |
| --- | --- | --- | --- |
| クイックスタート | Mongo API | Mongo APIは非推奨（廃止予定）となり、今後のリリースで削除される予定です。 | 6.5 TS SP2 |
| Sites | AEM Assets REST APIでのコンテンツフラグメントのサポート | AEM 6.5 LTS SP2では、コンテンツフラグメントとモデル管理用の最新のOpenAPIが提供されているため、AEM Assets REST APIの古いコンテンツフラグメントサポートエンドポイントは非推奨になりました。<br>Adobeでは、これらの古いエンドポイントを提供終了のお知らせまで利用できる予定です。 Adobeでは、非推奨のエンドポイントに対する機能強化は計画していません。 | 6.5 LTS SP2 |
| Sites | [SPA Editor](/help/sites-developing/spa-overview.md) | AEM でヘッドレスコンテンツの管理に推奨されるエディターは次のとおりです。<br>- ビジュアル編集用の[ユニバーサルエディター](/help/sites-developing/universal-editor/introduction.md)。<br>- フォームベース編集用の[コンテンツフラグメントエディター](/help/assets/content-fragments/content-fragments-managing.md)。 | 6.5 LTS GA |
| [!DNL Foundation] | com.adobe.granite.oauth.server のサポート | Adobe IMS 統合 |  |

### 削除された機能 {#removed-features}

この節では、AEM 6.5 LTS から削除された機能の一覧を示します。以前のリリースでは、これらの機能は非推奨（廃止予定）としてマークされていました。

* CRX リポジトリの永続性に対するRDBMKのサポートが削除されました。
* クラスター環境では、MongoMKがリポジトリの永続性でサポートされる唯一のオプションになりました。

| 領域 | 機能 | 代替手段 | バージョン（SP） |
| --- | --- | --- | --- |
| Commerce | AEM CIF Classic はサポートされていません。 | [AEM CIF](/help/commerce/cif/migration.md) に移行します。 | 6.5 LTS GA |
| ソリューション | ソーシャル／コミュニティはサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Screens | Screens はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Assets | バンドルはソーシャルに依存しているので、`dam-pim` と `dam-rating` はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Assets | `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettings()` は削除されました。 | 追加された代替 API `com.day.cq.dam.scene7.api.model.Scene7ViewerConfig#getSettingsList()` を使用します。 | 6.5 LTS GA |
| ポータル | AEM Portal Director はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Granite | バンドル `com.adobe.granite.socketio` は削除されました。 | 代替手段はありません。 | 6.5 LTS GA |
| Granite | `com.adobe.granite.crx-explorer` はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Granite | `crx2oak` はサポートされていません。 | [Oak-upgrade](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-upgrade) の関連バージョンを選択します | 6.5 LTS GA |
| Adobe | `com.adobe.cq.cq-searchpromote-integration` はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| Guava | AEM では、すべての guava 依存関係が削除されたので、`com.adobe.granite.osgi.wrapper.guava-15.0.0-0002` バンドルは AEM の一部ではなくなりました。 | 顧客は、guava に依存している場合は独自に guava を追加したり、可能であれば guava コードを java コレクションまたはその他の代替手段に置き換えたりすることができます。 | 6.5 LTS GA |
| `We.Retail` | `We-retail` サンプルサイトはサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| オープンソース | `oak-solr-osgi` バンドルはサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| オープンソース | `org.apache.servicemix.bundles.abdera-parser`、`org.apache.servicemix.bundles.jdom`、`org.apache.sling.atom.taglib` はサポートされていません。 | 代替手段はありません。 | 6.5 LTS GA |
| オープンソース | `org.apache.commons.io` パッケージが `org.apache.commons.commons-io` から書き出されるようになりました。 | 変更は必要ありません。 | 6.5 LTS GA |
| オープンソース | `javax.mail` パッケージが `com.sun.javax.mail` バンドルから書き出されています。 | 変更は必要ありません。 | 6.5 LTS GA |
| オープンソース | `org.apache.jackrabbit.api` パッケージが `org.apache.jackrabbit.oak-jackrabbit-api` バンドルから書き出されるようになりました。 | 変更は必要ありません。 | 6.5 LTS GA |
| オープンソース | `com.github.jknack.handlebars` はサポートされていません | 関連[バージョン](https://mvnrepository.com/artifact/com.github.jknack/handlebars)を選択します | 6.5 LTS GA |


## 既知の問題 {#known-issues}

### AEM Forms

* **FORMS-24690:** Configuration Managerでは、モジュールが選択されていない場合、カスタム設定でAEM Forms 6.5 LTS JEEをターンキーモードで実行すると、ブートストラップ中にデータベースの初期化が失敗します。

* **FORMS-24692:** メールサービスがTLS ソケット接続の確立に失敗し、メール配信が失敗する可能性があります。

* **FORMS-24741:** Linux上のAEM Forms 6.5 LTS JEEでは、OSFileSetIntendedForが正しく設定されていない場合、Configuration Managerが失敗する可能性があります。 Configuration Managerを実行する前に、必要な設定ファイルでLinuxにアップデートします。

### オフラインコンパクション後のオンラインコンパクション中にリポジトリが破損する（GRANITE-65146） {#repository-corruption-during-online-compaction-after-offline-compaction-granite-65146}

オフラインコンパクションが以前にJCR リポジトリで実行されていた場合、オンラインコンパクション中にリポジトリの破損が発生する可能性があります。 このシナリオで`SegmentNotFoundException` （SNFE）が発生し、リポジトリの破損につながる可能性があります。

この問題を解決するには、[&#x200B; ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.2-hotfix-GRANITE-65388-1.0.zip)からホットフィックスをインストールしてください。 ホットフィックスには下位レベルの`oak-segment-tar` バンドルが含まれているため、インスタンスはインストール後に再起動します。

インスタンスを適用する際のダウンタイムを計画します。 オフラインコンパクションの場合は、ソフトウェア配布でも提供されている対応する[oak-run jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar)を使用します。

>[!NOTE]
>
> * oak-run操作には、[oak-run 1.88.1-B006 jar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/oak-run-1.88.1-B006.jar)を使用します。
>
> * システム プロパティ `oak.compaction.legacy=true`を設定してAEMを開始します。

### Sites ヘッドレス APIに必要なOak インデックスのインストール{#site-headless-api}

Sites ヘッドレスに移行した一部のAPIでは、すべての機能に対して追加のOak インデックスが必要です。

次の機能を使用するには、`cq-dam-cfm-indices` パッケージをインストールします。

* コンテンツフラグメントモデルのリスト
* コンテンツフラグメントのリスト
* 検索 API
* workflows

Adobe Software Distribution ポータルからインデックスパッケージ [cq-dam-cfm-indices](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/cq-dam-cfm-indices-1.1.2.zip)をダウンロードします。

### SSL のみの機能を使用した Dispatcher 接続の失敗（AEM 6.5 LTS SP1 以降で修正）{#ssl-only-feature}

>[!NOTE]
>
> この問題は、AEM 6.5 LTS GA リリースにのみ存在します。

AEM デプロイメントで SSL のみの機能を有効にすると、Dispatcher インスタンスと AEM インスタンス間の接続に影響を与える既知の問題があります。 この機能を有効にすると、ヘルスチェックが失敗し、Dispatcher インスタンスと AEM インスタンス間の通信が中断される場合があります。この問題は、お客様が `https + IP` 経由で Dispatcher から AEM インスタンスに接続しようとした場合に特に発生します。これは、SNI（Server Name Indication）検証の問題に関連しています。

**影響**

* HTTP 400 応答コードを使用したヘルスチェックの失敗
* Dispatcher インスタンスとAEM インスタンス間のトラフィックの破損
* Dispatcher 経由でコンテンツを適切に配信できない
* Dispatcher 設定で IP アドレスを指定して HTTPS を使用した際の接続の失敗
* HTTPS + IP 経由で接続した際の HTTP 400「無効な SNI」エラー

**影響を受ける環境**

* Dispatcher 設定を使用した AEM デプロイメント
* SSL のみの機能が有効になっているシステム
* AEM インスタンスへの `https + IP` 接続方法を使用した Dispatcher 設定

**解決策**

この問題が発生した場合は、Adobe カスタマーサポートにお問い合わせください。 この問題を解決するためのホットフィックス [cq-6.5.lts.0-hotfix-CQ-4359803](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq660/hotfixes/cq-6.5.lts.0-hotfix-CQ-4359803-1.0.2.zip) が使用可能です。必要なホットフィックスを適用するまで、SSL のみの機能を有効にしないでください。

## 含まれている OSGi バンドルとコンテンツパッケージ{#osgi-bundles-and-content-packages-included}

次のテキストドキュメントには、この [!DNL Experience Manager] 6.5 LTS、サービスパック 1 リリースに含まれている OSGi バンドルとコンテンツパッケージのリストが記載されています。

* [Experience Manager 6.5 LTS、サービスパック 1 に含まれている OSGi バンドルのリスト](/help/release-notes/assets/65lts_sp1_bundles.txt) <!-- UPDATE FOR EACH NEW RELEASE -->
* [Experience Manager 6.5 LTS、サービスパック 1 に含まれているコンテンツパッケージのリスト](/help/release-notes/assets/65lts_sp1_packages.txt) <!-- UPDATE FOR EACH NEW RELEASE -->

## 制限付き Web サイト{#restricted-sites}

以下の web サイトはお客様のみが参照できます。 アクセス権を必要とするお客様は、アドビのアカウントマネージャーにお問い合わせください。

* [licensing.adobe.com からの製品ダウンロード](https://licensing.adobe.com/)
* [アドビカスタマーサポートに連絡](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-customer-support-experience)。

