---
title: ContextHub UI モジュールタイプのサンプル
description: ContextHub には、ソリューションで利用できる UI モジュールのサンプルが用意されています。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Personalization
role: Developer
exl-id: 523d8bf9-b925-4c09-8452-bb3a31489dd1
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 100%

---

# ContextHub UI モジュールタイプのサンプル {#sample-contexthub-ui-module-types}

ContextHub には、ソリューションで使用できるいくつかのサンプル UI モジュールが用意されています。次の情報が提供されます。

* UI モジュールの主な機能。
* 学習目的で開くことのできるソースコードの場所。
* UI モジュールの設定方法。

ContextHub への UI モジュールの追加について詳しくは、[UI モジュールの追加](ch-configuring.md#adding-a-ui-module)を参照してください。UI モジュールの開発について詳しくは、[ContextHub UI モジュールタイプの作成](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types)を参照してください。

## contexthub.base UI モジュールタイプ {#contexthub-base-ui-module-type}

contexthub.base UI モジュールタイプは、他のすべての UI モジュールタイプのベースタイプです。したがって、ストアデータをレンダリングするための汎用機能を提供します。

次の機能を使用できます。

* **タイトルとアイコン：** UI モジュールのタイトルとアイコンを指定します。アイコンは、URL または Coral UI アイコンライブラリから参照できます。
* **ストアデータ：**&#x200B;データの取得元となる 1 つ以上のストアを特定します。
* **コンテンツ：** UI モジュールに表示されるコンテンツを、ContextHub ツールバーに表示される通りに指定します。
* **ポップオーバーのコンテンツ：** UI モジュールをクリックまたはタップした際にポップオーバーに表示されるコンテンツを指定します。
* **全画面表示モード：**&#x200B;全画面モードを許可するかどうかを制御します。

ソースコードは、/libs/granite/contexthub/code/ui/container/js/ContextHub.UI.BaseModuleRenderer.js にあります。

### 設定 {#configuration}

JSON 形式の JavaScript オブジェクトを使用して、contexthub.base UI モジュールを設定します。UI モジュールの機能を設定するには、次のいずれかのプロパティを含めます。

* **image：**&#x200B;アイコンとして表示する画像への URL。
* **icon：** [Coral UI アイコン](https://helpx.adobe.com/jp/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html)クラスの名前。icon プロパティと image プロパティの両方に値を指定した場合は、image が使用されます。

* **title：** UI モジュールのタイトル。タイトルは、ポインターを UI モジュールアイコンに合わせると表示されます。
* **fullscreen：** UI モジュールが全画面モードをサポートするかどうかを示すブール値。全画面をサポートする場合は `true`、全画面モードを許可しない場合は `false` を使用します。

* **template：** ContextHub のツールバーにレンダリングするコンテンツを指定する [Handlebars](https://handlebarsjs.com/) テンプレート。最大 2 つの `<p>` タグを使用します。

* **storeMapping：**&#x200B;キーとストアのマッピング。Handlebar テンプレートでキーを使用して、関連付けられている ContextHub ストアデータにアクセスします。
* **list：** UI モジュールをクリックしたときに、ポップオーバーにリストとして表示する項目の配列。この項目を含める場合は、popoverTemplate を含めないでください。値は、次のキーを持つオブジェクトの配列です。

   * タイトル：この項目に対して表示するテキスト
   * 画像：（オプション）左側に表示する画像への URL
   * アイコン：（オプション）左側に表示する CUI アイコンクラスで、画像が指定されている場合は無視されます
   * 選択済み：（オプション）この項目を選択された状態で表示するかどうかを指定する Boolean 値（true=selected）。デフォルトでは、選択した項目が太字フォントで表示されます。その他の外観を設定するには、`listType` プロパティを使用します（以下を参照）。

* **listType：**&#x200B;ポップオーバーリスト項目に使用するスタイル。次のいずれかの値を使用します。

   * チェックマーク
   * チェックボックス
   * ラジオ

* **popoverTemplate：** UI モジュールをクリックしたときにポップオーバーにレンダリングするコンテンツを指定する Handlebars テンプレート。この項目を含める場合は、`list` 項目を含めないでください。

### 例 {#example}

次の例では、[contexthub.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) ストアからの情報を表示するように contexthub.base UI モジュールを設定しています。`template` 項目は、`storeMapping` 項目が作成するキーを使用することによって、このストアからデータを取得する方法を示しています。

```xml
{
   "icon": "coral-Icon--move",
    "title": "Screen Resolution",
    "storeMapping": {
      "emulator": "emulators"
    },
    "template": "<p>{{{ i18n \"Resolution\"}}}</p><p>{{{emulator.currentDevice.width}}} x {{{emulator.currentDevice.height}}}</p>"
}
```

![chlimage_1-76](assets/chlimage_1-76a.png)

## contexthub.browserinfo UI モジュールタイプ {#contexthub-browserinfo-ui-module-type}

contexthub.browserinfo UI モジュールは、クライアント web ブラウザーとオペレーティングシステムに関する情報を表示します。情報は、[contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) ストア候補をベースとする surferinfo ストアから取得されます。

![chlimage_1-77](assets/chlimage_1-77a.png)

この UI モジュールのソースコードは、/libs/granite/contexthub/components/modules/browserinfo にあります。contexthub.browserinfo は contexthub.base UI モジュールを拡張したものですが、追加の関数を上書きまたは提供しません。この実装は、ブラウザー情報をレンダリングするためのデフォルトの設定を提供します。

### 設定 {#configuration-1}

contexthub.browserinfo UI モジュールのインスタンスには、詳細設定用の値は必要ありません。次の JSON テキストは、モジュールのデフォルトの設定を表しています。

```xml
{
   "icon":"coral-Icon--globe",
   "title":"Browser/OS Information",
   "storeMapping":{"surferinfo":"surferinfo"},
   "template":"<p>{{surferinfo.browser.family}} {{surferinfo.browser.version}}</p><p>{{surferinfo.os.name}} {{surferinfo.os.version}}</p>"
}
```

## contexthub.datetime UI モジュールタイプ {#contexthub-datetime-ui-module-type}

contexthub.datetime UI モジュールは、[contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) ストア候補をベースとする、datetime という名前のストアに格納されている日時を表示します。

![chlimage_1-78](assets/chlimage_1-78a.png)

このモジュールは、ストア内の日時を変更できるポップオーバーフォームを提供します。

contexthub.datetime UI モジュールのソースは、/libs/granite/contexthub/components/modules/datetime にあります。

### 設定 {#configuration-2}

contexthub.datetime UI モジュールのインスタンスには、詳細設定用の値は必要ありません。次の JSON テキストは、モジュールのデフォルトの設定を表しています。

```xml
{
   "icon":"coral-Icon--clock",
   "title":"DATE&TIME",
   "clickable":true,
   "storeMapping":{"d":"datetime"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Date&Time\"}}</p><p class=\"contexthub-module-line2\">{{d.formatted.locale.date}} {{d.formatted.locale.time}}</p>",
   "popoverTemplate":"<div class=\"datetime center\"><div class=\"coral-DatePicker-calendar\" data-init=\"datepicker\"><input class=\"coral-Textfield\" type=\"datetime\" value=\"{{d.formatted.iso}}\"><button class=\"coral-Button coral-Button--secondary coral-Button--square\" title=\"{{i18n \"Datetime picker\"}}\"><i class=\"coral-Icon coral-Icon--calendar coral-Icon--sizeS\"></i></button></div></div>"
}
```

## contexthub.location UI モジュールタイプ {#contexthub-location-ui-module-type}

contexthub.location UI モジュールは、クライアントの緯度と経度を表示します。このモジュールは、クリックして現在の位置を変更できる Google マップを表示するポップオーバーを提供します。このモジュールは、[contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) ストア候補をベースとする、geolocation という名前の ContextHub ストアから情報を取得します。

![chlimage_1-80](assets/chlimage_1-80a.png)

この UI モジュールのソースは、/etc/cloudsettings/default/contexthub/geolocation にあります。

### 設定 {#configuration-4}

contexthub.location UI モジュールのインスタンスには、詳細設定用の値は必要ありません。次の JSON テキストは、モジュールのデフォルトの設定を表しています。

```xml
{
 "icon":"coral-Icon--compass",
 "title":"Location",
 "clickable":true,
 "editable":{"key":"/geolocation","disabled":[],"hidden":["/geolocation/generatedThumbnail","/geolocation/city","/geolocation/country"]},
 "fullscreen":true,
 "storeMapping":{"g":"geolocation"},
 "template":"<p>{{i18n \"Location\"}}</p><p>{{g.address.postalCode}} {{g.address.city}}{{#if g.address.city}}{{#if g.address.region}},{{/if}}{{/if}} {{g.address.region}}</p>",
 "list":[
  {"title":"Basel, Switzerland",
  "data":{"longitude":7.58929,"latitude":47.554746,"city":"Basel","country":"Switzerland"}},
  {"title":"Melbourne, Australia",
  "data":{"longitude":144.96328,"latitude":-37.814107,"city":"Melbourne","country":"Australia"}},
  {"title":"Beijing, China",
  "data":{"longitude":116.407526,"latitude":39.90403,"city":"Beijing","country":"China"}},
  {"title":"New York, NY, USA",
  "data":{"longitude":-74.005973,"latitude":40.714353,"city":"New York","country":"United States"}},
  {"title":"Paris, France",
  "data":{"longitude":2.352222,"latitude":48.856614,"city":"Paris","country":"France"}},
  {"title":"Rio de Janeiro, Brazil",
  "data":{"longitude":-43.20071,"latitude":-22.913395,"city":"Rio","country":"Brazil"}},
  {"title":"San Jose, CA, USA",
  "data":{"longitude":-121.894955,"latitude":37.339386,"city":"San Jose","country":"United States"}},
  {"title":"Tokyo, Japan",
  "data":{"longitude":139.691706,"latitude":35.689487,"city":"Shinjuku","country":"Japan"}}
 ],
 "listType":"checkmark"
}
```

## contexthub.screen-orientation UI モジュールタイプ {#contexthub-screen-orientation-ui-module-type}

contexthub.screen-orientation UI モジュールは、クライアントの現在の画面の向きを表示します。デフォルトでは無効になっていますが、このモジュールは向きを選択できるポップオーバーを提供します。このモジュールは、[granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) ストア候補をベースとする、emulators という名前の ContextHub ストアから情報を取得します。

![chlimage_1-81](assets/chlimage_1-81a.png)

この UI モジュールのソースは、/libs/granite/contexthub/components/modules/screen-orientation にあります。

### 設定 {#configuration-5}

contexthub.screen-orientation UI モジュールのインスタンスには、詳細設定用の値は必要ありません。次の JSON テキストは、モジュールのデフォルトの設定を表しています。`clickable` プロパティは、デフォルトで `false` です。デフォルトの設定を上書きして `clickable` を `true` に設定した場合、このモジュールをクリックするとポップアップが表示され、向きを選択できます。

```xml
{
   "icon":"coral-Icon--rotateRight",
   "title":"Screen Orientation",
   "clickable":false,
   "storeMapping":{"emulator":"emulators"},
   "template":"<p>{{{ i18n \"Screen Orientation\" }}}</p><p>{{{ emulator.currentDevice.orientation }}}",
   "listReference":"/emulators/orientations",
   "listType":"checkmark"
}
```

## contexthub.tagcloud UI モジュールタイプ {#contexthub-tagcloud-ui-module-type}

contexthub.tagcloud UI モジュールは、タグに関する情報を表示します。UI モジュールのツールバーにはタグの数が表示されます。ポップアップには、タグクラウドと新しいタグを追加するためのテキストボックスが表示されます。この UI モジュールは、[contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) ストア候補をベースとする、tagcloud という名前の ContextHub ストアから情報を取得します。

![chlimage_1-82](assets/chlimage_1-82a.png)

この UI モジュールのソースは、/libs/granite/contexthub/components/modules/tagcloud にあります。

### 設定 {#configuration-6}

contexthub.tagcloud UI モジュールのインスタンスには、詳細設定用の値は必要ありません。次の JSON テキストは、モジュールのデフォルトの設定を表しています。

```xml
{
   "icon":"coral-Icon--tag",
   "title":"TagCloud",
   "clickable":true,
   "storeMapping":{"t":"tagcloud"},
   "maxTags":20,
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"TagCloud\"}}</p><p class=\"contexthub-module-line2\">{{stats.total}} {{i18n \"Tags\"}}</p>",
   "popoverTemplate":"<div class=\"contexthub-popover-content center\"><p class=\"stats\">{{stats.total}} {{i18n \"Tags\"}} | {{stats.hits}} {{i18n \"Hits\"}} | {{i18n \"Last tag\"}}: {{#if stats.recent}}{{stats.recent}}{{else}}{{i18n \"Unknown\"}}{{/if}}</p><p class=\"tagcloud\">{{#each tags}}<span class=\"tag{{this.weight}}\">{{this.name}}</span> {{/each}}</p><div class=\"coral-InputGroup\"><input type=\"text\" class=\"coral-InputGroup-input coral-Textfield tag-name\" placeholder=\"{{i18n \"Add a namespace:my/tag\"}}\" pattern=\"^[A-Za-z0-9_\\-]+(:[A-Za-z0-9_\\-\\/]+)?$\" title=\"{{i18n \"namespace:my/tag\"}}\"><span class=\"coral-InputGroup-button\"><button class=\"coral-Button coral-Button--secondary coral-Button--square contexthub-new-tag\" type=\"button\" title=\"{{i18n \"increment\"}}\"><i class=\"coral-Icon coral-Icon--sizeS coral-Icon--add\"></i></button></span></div></div>"
}
```

## granite.profile UI モジュールタイプ {#granite-profile-ui-module-type}

granite.profile ContextHub UI モジュールは、現在のユーザーの表示名を表示します。ポップアップにはユーザーのログイン名が表示され、表示名の値を変更できます。この UI モジュールは、[granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) ストア候補をベースとする、profile という名前の ContextHub ストアから情報を取得します。

![chlimage_1-83](assets/chlimage_1-83a.png)

この UI モジュールのソースは、/libs/granite/contexthub/components/modules/profile にあります。

### 設定 {#configuration-7}

contexthub.profile UI モジュールのインスタンスには、詳細設定用の値は必要ありません。次の JSON テキストは、モジュールのデフォルトの設定を表しています。

```xml
{
   "icon":"coral-Icon--user",
   "title":"Profile",
   "clickable":true,
   "editable":{
      "key":"/profile",
      "disabled":["/profile/authorizableId"],
      "hidden":["/profile/avatar","/profile/path"]},
   "storeMapping":{"p":"profile"},
   "template":"<p class=\"contexthub-module-line1\">{{i18n \"Persona\"}}</p><p class=\"contexthub-module-line2\">{{p.displayName}}</p>",
   "listType":"checkmark"
}
```
