---
title: Acrobat Reader DC Extensionsで使用される証明書の種類
description: Acrobat Reader DC Extensionsで使用される証明書の種類について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: ca919915-c37b-4793-b5e2-21a464c5dcdf
source-git-commit: 103250f3442cf7c2793c51a95b1bf4fbaff71463
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 65%

---

# Acrobat Reader DC Extensionsで使用される証明書の種類 {#certificate-types-used-by-acrobat-reader-dc-extensions}

証明書ビューアでは、証明書に関する次の情報を参照できます。

* 証明書のわかりやすい名前
* 証明書プロファイル
* 有効期間
* Acrobat Reader DC Extensionsの使用権限

## 証明書のわかりやすい名前 {#certificate-friendly-name}

Acrobat Reader DC Extensions証明書の「フレンドリー」名は、次の例に示すように、証明書のプロパティを説明する文字列です。

ARE 2D Barcode Full Production V6.1 P8 0002054

この文字列には、次の要素が含まれています。

**証明書の種類：** 証明書によってアクティベートされる AEM Forms モジュール、およびアクティベートのレベル（ARE 2D Barcode Full など）が記述されています。 使用可能な証明書の種類の一覧については、証明書プロファイルの表の種類の列を参照してください。

**デプロイメントの種類：** 実稼働などの、証明書の使用目的を示します。 値は、Evaluation（評価）または Production（実稼働環境）のどちらかです。 証明書の各種類に関連付けられているデプロイメントの種類の一覧については、証明書プロファイルの表のデプロイメントの種類の列を参照してください。

**使用権限バージョン：**&#x200B;証明書を使用できる使用権限アルゴリズム（V6.1など）のバージョンを示します。 このバージョンは、AcrobatまたはAcrobat Reader DC Extensionsのバージョンを示すものではありません。

**プロファイルコード：** プロファイルコードは、完全な証明書プロパティの簡単な説明です（P8 など）。 ファイルの各種類に関連付けられているプロファイルコードの一覧については、証明書プロファイルの表のプロファイルコードの列を参照してください。

**シリアル番号：** シリアル番号は、アドビによって発行される証明書ごとにアサインされます（0002054 など）。 アドビの販売代理店または営業担当者は、このシリアル番号を使用して、特定の製品注文または OEM 関係まで証明書を追跡できます。

## 証明書プロファイル {#certificate-profiles}

次の表に、Acrobat Reader DC Extensions証明書を分析する際に発生する可能性のある証明書プロファイルを示します。

<table>
 <thead>
  <tr>
   <th><p>プロファイルコード</p></th>
   <th><p>タイプ</p></th>
   <th><p>有効期間</p></th>
   <th><p>デプロイメントの種類</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>SAP 実稼動環境</p></td>
   <td><p>終了日</p></td>
   <td><p>本番</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>SAP 内部テスト</p></td>
   <td><p>2 年</p></td>
   <td><p>評価およびテスト</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Acrobat Reader DC Extensions、実稼動環境</p></td>
   <td><p>終了日</p></td>
   <td><p>本番</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Acrobat Reader DC Extensions、内部Adobe使用状況</p></td>
   <td><p>2 年</p></td>
   <td><p>本番</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Acrobat Reader DC Extensions、パートナー統合</p></td>
   <td><p>2 年</p></td>
   <td><p>評価およびテスト</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Acrobat Reader DC Extensions，評価</p></td>
   <td><p>60 日</p></td>
   <td><p>評価</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms、実稼動環境</p></td>
   <td><p>終了日</p></td>
   <td><p>本番</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x、実稼動環境</p></td>
   <td><p>終了日</p></td>
   <td><p>本番</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms; OEMはFormsを使用できます</p></td>
   <td><p>終了日</p></td>
   <td><p>実稼動環境および評価</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms; OEMはFormsを使用できます。</p></td>
   <td><p>終了日</p></td>
   <td><p>実稼動環境および評価</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>署名のみ。OEMは署名のみを使用できます</p></td>
   <td><p>終了日</p></td>
   <td><p>実稼動環境および評価</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>オフラインコメントのみ。OEMはオフラインコメントを使用できます</p></td>
   <td><p>終了日</p></td>
   <td><p>実稼動環境および評価</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>コメントのみ：OEMはコメントのみを使用できます</p></td>
   <td><p>終了日</p></td>
   <td><p>実稼動環境および評価</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>完全な権限。OEMは完全な権限を使用できます</p></td>
   <td><p>終了日</p></td>
   <td><p>実稼動環境および評価</p></td>
  </tr>
 </tbody>
</table>

## 有効期間 {#validity-period}

評価用証明書は、製品のサンプルアプリケーションを評価および開発できるようにするために、顧客および開発者に対して発行されます。 この証明書の有効期間は 60～90 日です。 イシューデータの後2か月目に有効期限が切れます。

パートナー統合証明書は、アドビのビジネスパートナーに対して、ソフトウェアの開発、統合、プロトタイピングおよびデモンストレーションをサポートするために発行されます。 これらの証明書は、発行日から 2 年間有効です。

Adobe内部使用証明書は、ソフトウェアの開発、統合、プロトタイピング、およびデモをサポートするために、Adobe内で使用されます。 これらの証明書は、発行日から 2 年間有効です。

実稼動証明書は、Acrobat Reader DC Extensionsを購入したお客様に発行されます。 この種の証明書は、認証局（CA）によって許可された最長期間有効です（証明書プロファイルの表では、「*最大値*」と示されています）。

## Acrobat Reader DC Extensionsの使用権限 {#acrobat-reader-dc-extensions-usage-rights}

証明書ビューアでAcrobat Reader DC Extensions証明書を確認する際に、「詳細」タブ（設定されている場合）から使用権限の項目を選択できます。 証明書で有効にできるAdobe Reader使用権限の項目別リストが表示されます。 特定の文書で有効になっている使用権限は、証明書で有効になっている使用権限のサブセットである可能性があります。

コラボレーションのない環境でオンラインコメントが必要な場合は、アドビサポートにお問い合わせください。 Mode プロパティはデプロイメントの種類と一致し、「*実稼動環境*」または「*評価*」になります。

許可されているAcrobat Reader DC Extensionsの使用権限は、1つ以上の特定の要素で構成されています。 これらの要素を異なる組み合わせで使用することにより、ライセンスされている製品の様々な機能を使用できるようになります。

<table>
 <thead>
  <tr>
   <th><p>使用権限の要素</p></th>
   <th><p>Adobe Reader で有効になる機能（使用権限を付与された PDF ドキュメントを表示する場合）</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>フォームフィールドに入力し、ファイルをローカルに保存します。</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>データを FDF、XFDF、XML または XDP ファイルとして読み込んだり書き込んだりする。</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>PDF フォームのフィールドおよびフィールドプロパティを追加したり、変更したり、削除したりする。</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>サーバーがブラウザーセッションで実行されていないときに、メールまたはオフラインでデータをサーバーに送信する。</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>同じ PDF フォーム内のテンプレートページからページを作成する。</p></td>
  </tr>
  <tr>
   <td><p>署名</p></td>
   <td><p>PDF ドキュメントに電子署名して保存したり、電子署名を消去したりする。</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>コメントなどのドキュメント注釈を作成したり変更したりする。</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>コメントなどの注釈を別のデータファイルに保存したり、ファイルからコメントを読み込んだりする。</p></td>
  </tr>
  <tr>
   <td><p>BarcodePlaintext</p></td>
   <td><p>デコードするためにライセンスされたサーバーソフトウェアを必要としない非暗号化形式でバーコード化されたフォームデータを含むドキュメントを印刷する。</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>コメントなどの注釈を、オンラインドキュメントレビューおよびコメントサーバーにアップロードしたり、サーバーからダウンロードしたりする。</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>PDF フォーム内で定義されている Web サービスまたはデータベースに接続する。</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>PDF ドキュメントに関連付けられた埋め込みファイルオブジェクトを変更する。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Acrobat Reader DC Extensionsの使用権限は、Adobeからライセンスを取得できるのは、連携している特定の組み合わせのみです。 これらの機能を個別にライセンスすることはできません。 使用権限の可能な組み合わせについては、AEM Forms の営業担当者にお問い合わせください。
