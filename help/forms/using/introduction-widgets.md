---
title: アダプティブフォームおよび HTML5 フォームの外観フレームワーク
description: Mobile Forms はフォームテンプレートを HTML5 フォームとしてレンダリングします。これらのフォームは jQuery、Backbone.js および Underscore.js ファイルを外観およびスクリプティングの有効化に使用します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Mobile Forms
role: User, Developer
exl-id: 9d80bc0a-f2b0-4b27-9417-639531cb8415
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 100%

---

# アダプティブフォームおよび HTML5 フォームの外観フレームワーク {#appearance-framework-for-adaptive-and-html-forms}

フォーム（アダプティブフォームと HTML5 フォーム）は、[jQuery](https://jquery.com/)、[Backbone.js](https://backbonejs.org/)および[Underscore.js](https://underscorejs.org/)ライブラリを外観とスクリプト作成のために使用します。このフォームはまた、フォーム内のすべての対話操作要素（例えばフィールドやボタン）に対して [jQuery UI](https://jqueryui.com/) **Widgets**&#x200B;アーキテクチャを使用します。このアーキテクチャは、フォーム開発者が Forms で豊富な使用可能な jQuery ウィジェットとプラグインのセットを利用できるようにします。また、ユーザーから leadDigits/trailDigits の制限やパターン形式文字列の実装などのデータを取得しながら、フォーム固有のロジックを実装することもできます。フォーム開発者はカスタム外観を作成して使用し、データ取得のエクスペリエンスを改善し、よりユーザーフレンドリーにすることができます。

この記事は jQuery と jQuery ウィジェットの知識が十分ある開発者向けです。外観フレームワークについての理解を深めたり、開発者がフォームフィールドに別の外観を作成するのに役立ちます。

外観フレームワークは、様々なオプション、イベント（トリガー）および機能に依存し、ユーザーのフォームとのやり取りを取得し、モデル変更に対応してエンドユーザーに通知します。さらに、次の点に注意してください。

* フレームワークは、フィールドの外観に一連のオプションを提供します。これらのオプションはキーと値のペアであり、一般的なオプションとフィールドタイプ固有のオプションの 2 つのカテゴリに分かれます。
* 外観はコントラクトの一部として、enter や exit などの一連の インベントのセットをトリガーします。
* 一連の関数を実装するには、外観が必要となります。その関数には一般的なものから、フィールドタイプ固有のものも含まれています。

## 一般的なオプション {#common-options}

グローバルオプションは次のとおりです。これらのオプションはすべてのフィールドで使用できます。

<table>
 <tbody>
  <tr>
   <th>プロパティ </th>
   <th>説明</th>
  </tr>
  <tr>
   <td>name</td>
   <td>スクリプト式でこのオブジェクトまたはイベントを指定するために使用される識別子です。例えば、このプロパティはホストアプリケーションの名前を指定します。</td>
  </tr>
  <tr>
   <td>value</td>
   <td>フィールドの実際の値。 </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>フィールドのこの値が表示されます。 </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>スクリーンリーダーはこの値を使用して、フィールドについての情報を読み上げます。フォームは値を提供し、その値を上書きできます。<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>フォームのタブシーケンスにおけるフィールドの位置フォームのデフォルトタブの順序を変更する場合にのみ、tabIndex を上書きします。</td>
  </tr>
  <tr>
   <td>role</td>
   <td>要素のロール（例：見出しやテーブル）。</td>
  </tr>
  <tr>
   <td>height</td>
   <td>ウィジェットの高さ。ピクセル単位で指定します。 </td>
  </tr>
  <tr>
   <td>width</td>
   <td>ウィジェットの幅。ピクセル単位で指定します。</td>
  </tr>
  <tr>
   <td>access</td>
   <td>サブフォームなど、コンテナオブジェクトのコンテンツへのアクセスに使用されるコントロール。</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>ウィジェットへの XFA 要素のパラプロパティ。</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>テキストの方向。使用可能な値は ltr （左から右）と rtl （右から左）です。</td>
  </tr>
 </tbody>
</table>

これらのオプションとは別に、フィールドのタイプによって異なるいくつかの他のオプションがフレームワークによって提供されます。フィールド固有のオプションの詳細は、以下に記載されています。

### フォームのフレームワークとのインタラクション {#interaction-with-forms-framework}

Forms のフレームワークとやりとりするために、ウィジェットはいくつかのイベントをトリガーし、フォームスクリプトが機能するように有効化します。ウィジェットがこれらのイベントをスローしない場合、そのフィールドのためにフォーム内に書かれたスクリプトの一部が機能していません。

#### ウィジェットによってトリガーされるイベント {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>イベント </th>
   <th>説明</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>このイベントはフィールドがフォーカスされるたびにトリガーされます。フィールドで「入力」スクリプトの実行を可能にします。イベントをトリガーするための構文：<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>このイベントはフィールドを離れるたびにトリガーされます。エンジンがフィールドの値を設定し、その「終了」スクリプトを実行することを可能にします。イベントをトリガーするための構文：<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>このイベントがトリガーされ、エンジンがフィールドに書かれた「変更」スクリプトを実行することが可能になります。イベントをトリガーするための構文：<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>このイベントはフィールドがクリックされるたびにトリガーされます。エンジンがフィールドに書かれた「クリック」スクリプトを実行することが可能になります。イベントをトリガーするための構文：<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### ウィジェットで実装された API {#apis-implemented-by-widget}

外観フレームワークはカスタムウィジェットで実装されたウィジェットの関数をいくつか呼び出します。ウィジェットは次の関数を実装する必要があります。

<table>
 <tbody>
  <tr>
   <th>Function</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>focus: function()</td>
   <td>フォーカスをフィールドに移します。</td>
  </tr>
  <tr>
   <td>click: function()</td>
   <td>フォーカスをフィールドに移し、XFA_CLICK_EVENT を呼び出します。</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>errorMessage: string </em>representing the error<br /> <em>errorType: string ("warning"/"error")</em></p> <p><strong>メモ</strong>：HTML5 フォームにのみ適用可能です。</p> </td>
   <td>エラーメッセージとエラータイプをウィジェットに送信します。ウィジェットはエラーを表示します。</td>
  </tr>
  <tr>
   <td><p>clearError: function()</p> <p><strong>メモ</strong>：HTML5 フォームにのみ適用可能です。</p> </td>
   <td>フィールドのエラーが修正された場合に呼び出されます。ウィジェットはエラーを非表示にします。</td>
  </tr>
 </tbody>
</table>

## フィールドのタイプに固有のオプション {#options-specific-to-type-of-field}

すべてのカスタムウィジェットは上記の仕様に準拠する必要があります。異なるフィールドの機能を使用するには、ウィジェットはその特定のフィールドのガイドラインに準拠する必要があります。

### TextEdit：テキストフィールド {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>オプション</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>multiLine</td>
   <td>フィールドが改行文字の入力をサポートする場合 true。サポートしない場合 false。</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>フィールドに入力できる最大文字数。</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>メモ</strong>：HTML5 フォームにのみ適用可能です。</p> </td>
   <td>テキストのウィジェットがウィジェットの幅を超えたときの、テキストフィールドの動作を指定します。</td>
  </tr>
 </tbody>
</table>

### ChoiceList: DropDownList,、ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>オプション</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>value<br /> </td>
   <td>選択された値の配列。<br /> </td>
  </tr>
  <tr>
   <td>item<br /> </td>
   <td>オプションとして表示されるオブジェクトの配列。各オブジェクトには 2 つのプロパティがあります。<br />save：保存する値、display：表示される値。<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>編集可能な状態で</p> <p><strong>メモ</strong>：HTML5 フォームにのみ適用可能です。<br /> </p> </td>
   <td>値が true の場合、ウィジェットでカスタムテキスト入力が有効。<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>表示される値の配列。<br /> </td>
  </tr>
  <tr>
   <td>multiselect<br /> </td>
   <td>複数の選択が許可される場合は true。許可されない場合は false。<br /> </td>
  </tr>
 </tbody>
</table>

#### API {#api}

<table>
 <tbody>
  <tr>
   <th>Function</th>
   <th>説明</th>
  </tr>
  <tr>
   <td><p>addItem:<em> function(itemValues)<br /> itemValues：display と save の値が含まれているオブジェクト <br /> {sDisplayVal: &lt;displayValue&gt;, sSaveVal: &lt;save Value&gt;}</em></p> </td>
   <td>アイテムをリストに追加します。</td>
  </tr>
  <tr>
   <td>deleteItem<em>: function(nIndex)<br /> nIndex：リストから削除する項目のインデックス<br /> </em><br /> <br /> </td>
   <td>リストからオプションを削除します。</td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>リストからすべてのオプションを消去します。</td>
  </tr>
 </tbody>
</table>

### NumericEdit、NumericField、DecimalField {#numericedit-numericfield-decimalfield}

| オプション | 説明 |
|---|---|
| dataType | フィールドのデータタイプ（整数／十進数）を示す文字列。 |
| leadDigits | 十進数で許可される小数点以上の最大桁数。 |
| fracDigits | 十進数で許可される小数点以下の最大桁数。 |
| zero | フィールドのロケールでのゼロの文字列表現。 |
| decimal | フィールドのロケールでの小数点の文字列表現。 |

### CheckButton: RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>オプション</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>値の配列（on／off／neutral)）。</p> <p>これは、checkButton のさまざまなステートのための値の配列です。values[0] はステートがオンのときの値です。values[1] はステートがオフのときの値です。<br /> values[2] はステートが中間のときの値です。値配列の長さは、state オプションの値と同じです。<br /> </p> </td>
  </tr>
  <tr>
   <td>states</td>
   <td><p>許可される状態の数。 </p> <p>アダプティブフォームの場合は 2 つ（オン、オフ）、HTML5 フォームの場合は 3 つ（オン、オフ、中間）です。</p> </td>
  </tr>
  <tr>
   <td>state</td>
   <td><p>要素の現在の状態です。</p> <p>アダプティブフォームの場合は 2 つ（オン、オフ）、HTML5 フォームの場合は 3 つ（オン、オフ、中間）です。</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit: (DateField) {#datetimeedit-datefield}

| オプション | 説明 |
|---|---|
| 日 | そのフィールドのローカライズされた曜日の名前。 |
| 月 | そのフィールドのローカライズされた月の名前。 |
| zero | 数字の 0 のローカライズされたテキスト。 |
| clearText | 「クリア」ボタンのローカライズされたテキスト。 |
