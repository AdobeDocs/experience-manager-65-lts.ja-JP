---
title: インタラクティブ通信とレターのインライン条件と繰り返し構造
description: インタラクティブ通信とレターでインライン条件と繰り返し構造を使用すると、コンテキストに応じて変化する、適切に構造化された通信を作成できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4
topic-tags: interactive-communications, correspondence-management
docset: aem65
feature: Correspondence Management
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 2d05a36e-c02e-41ef-a03d-2a799aa6eab3
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 100%

---

# インタラクティブ通信とレターのインライン条件と繰り返し構造{#inline-condition-and-repeat-in-interactive-communications-and-letters}

## インライン条件 {#inline-conditions}

AEM Forms では、テキストモジュール内でインライン条件を使用して、フォームデータモデル（インタラクティブ通信の場合）またはデータディクショナリ（レターの場合）に関連付けられたコンテキストやデータに依存するテキストを自動的にレンダリングすることができます。インライン条件には、true または false の条件評価に応じて特定のコンテンツが表示されます。

フォームデータモデル、データディクショナリ、またはエンドユーザーによって指定されたデータの値に基づき、インライン条件によって計算処理が実行されます。インライン条件を使用することにより、コンテキストに応じて変化するカスタマイズされたインタラクティブ通信とレターを短時間で作成し、人為的なエラーを減らすことができます。

詳しくは、次を参照してください。

* [インタラクティブ通信を作成](../../forms/using/create-interactive-communication.md)
* [Correspondence Management の概要](/help/forms/using/cm-overview.md)
* [インタラクティブ通信内のテキスト](../../forms/using/texts-interactive-communications.md)

### 例：ルールを使用してインタラクティブ通信内のインラインテキストに条件を設定する {#example-using-rules-to-conditionalize-inline-text-in-interactive-communication}

インタラクティブ通信内の文、段落、文字列に条件を設定するには、適切なテキストドキュメントフラグメントでルールを作成します。以下のリンクに記載されている例では、ルールを使用して、インタラクティブ通信を米国で受信するユーザーだけにフリーダイヤルの番号を表示しています。

詳しくは、[インタラクティブ通信内のテキスト](../../forms/using/texts-interactive-communications.md)の「テキスト内でルールを作成する」を参照してください。

この例では、テキストフラグメントをインタラクティブ通信に含めると、エージェントがエージェント UI を使用してインタラクティブ通信の準備をおこない、受信者用のフォームデータモデルのデータが評価され、米国の受信者だけにテキストが表示されます。

### 例：レターでインライン条件を使用して、適切な呼称をレンダリングする場合  {#example-using-inline-condition-in-a-letter-to-render-the-appropriate-address}

レターにインライン条件を挿入するには、適切なテキストモジュールにインライン条件を挿入します。次の例では、2 つの条件を使用して、DD 要素 Gender に基づいて適切な呼称（Sir または Ma&#39;am）を評価し、それをレターに表示しています。その他の条件も、同様の手順で作成できます。

>[!NOTE]
>
>既存のアセットに古い（6.2 SP1 CFP 4 より前の）条件式や繰り返し式が含まれている場合は、アセットに古い構文の条件や繰り返しが表示されます。ただし、古い条件や繰り返しも正常に機能します。新しい条件式／繰り返し式と古い条件式／繰り返し式は互換性があるため、新しい式と古い式を混在できます。

1. 関連するテキストモジュールで、条件を付けるテキスト部分を選択し、「**条件**」を選択します。

   ![1_selecttext](assets/1_selecttext.png)

   条件ダイアログボックスが開き、空の条件が表示されます。

   ![2_conditiondialog](assets/2_conditiondialog.png)

   >[!NOTE]
   >
   >空の条件式や無効な条件式は保存できません。条件式を保存するには、`${}` の内部に有効な条件式が必要です。

1. 次の手順を実行して、選択および条件付けしたテキストがレターに表示されるかどうかを評価するための条件を作成し、チェックマークを選択して式を保存します。

   DD 要素をダブルクリックして条件に挿入します。ダイアログボックスで適切な演算子を挿入し、以下の条件を作成します。

   ```javascript
   ${DD_creditcard_Gender=="Male"}
   ```

   式の作成について詳しくは、[式ビルダー](../../forms/using/expression-builder.md)の&#x200B;**式ビルダーによる式およびリモート関数の作成**&#x200B;を参照してください。式に指定する値は、データディクショナリ内の要素でサポートされている必要があります。詳しくは、[データディクショナリ](../../forms/using/data-dictionary.md)を参照してください。

   条件を挿入すると、条件の左側にあるハンドルにポインタを合わせたときに条件が表示されます。ハンドルを選択すると、条件のポップアップメニューが表示され、条件を編集または削除できます。

   ![3_hoverhandle](assets/3_hoverhandle.png) ![4_editconditionremoveconditionpopup](assets/4_editconditionremoveconditionpopup.png)

1. テキスト `Ma'am` を選択して、同様の条件を挿入します。

   ```javascript
   ${DD_creditcard_Gender == "Female"}
   ```

1. 関連するレターをプレビューして、インライン条件に従ってテキストがレンダリングされていることを確認します。次のファイルを使用して DD 要素 Gender の値を入力できます。

   * サンプルデータを含むレターのプレビュー中に関連するデータディクショナリに基づいて作成されたサンプル XML データファイル。
   * 関連するデータディクショナリに添付されている XML データファイル。

   詳しくは、[データディクショナリ](../../forms/using/data-dictionary.md)を参照してください。

   ![5_letteroutput](assets/5_letteroutput.png)

## 繰り返し {#repeat}

インタラクティブ通信とレターには、動的な情報を含めることができます。例えば、クレジットカードの取引明細書は、レターが生成されるたびに変化します。繰り返し構造を使用すると、テキストドキュメントフラグメント内で、こうした動的な情報の書式設定と構造化をおこなうことができます。

また、繰り返し構造内でルールや条件を指定して、インタラクティブ通信またはレター内でレンダリングされる情報やエントリに条件を設定することもできます。

### 例：インタラクティブ通信内で繰り返し構造を使用して、クレジットカードの取引情報リストの書式設定、構造化、表示をおこなう {#example-using-repeat-in-an-interactive-communication-to-format-structure-and-display-a-list-of-credit-card-transactions}

以下の例は、繰り返しを使用して、インタラクティブ通信内のクレジットカード取引情報を構造化しレンダリングする手順を示しています。

1. フォームデータモデルベースのテキストドキュメントフラグメント内に、関連するフォームデータモデルオブジェクトと、ラベルに必要な組み込みテキストを挿入します（以下の図を参照）。

   ![1_elementstext](assets/1_elementstext.png)

   >[!NOTE]
   >
   >繰り返し可能なコンテンツには、コレクションタイプのプロパティを 1 つ以上含める必要があります。

1. 繰り返し構造を適用するコンテンツを選択します。

   ![2_selection](assets/2_selection.png)

1. 「繰り返し」を選択します。

   繰り返しダイアログが表示されます。

   ![3_repeatdialog](assets/3_repeatdialog.png)

1. 必要に応じて、区切り文字として「改行」を選択し、「条件を追加」を選択してルールを作成します。テキストを区切り文字として使用し、区切り文字として使用するテキスト文字を指定することもできます。

   ルール作成ダイアログが表示されます。

1. 2018 年 2 月 28 日以降に発生した取引情報を表示し、2018 年 3 月中に発生した取引情報だけをインタラクティブ通信に含めるためのルールを作成します。

   >[!NOTE]
   >
   >この例では、エージェントが 2018年3月31日に取引明細情報を作成することを想定しています。これとは別のルールを作成し、2018年4月1日より前に発生した取引情報をインタラクティブ通信に含めて、2018年3月より後に発生した取引情報を除外することもできます。

   ![4_createrule](assets/4_createrule.png)

1. 条件またはルールを保存して、繰り返し構造を保存します。条件が設定された繰り返し構造が、選択したコンテンツに適用されます。

   ![5_onmouseoverconditionrule](assets/5_onmouseoverconditionrule.png)

   テキストドキュメントフラグメントにポインタを合わせると、コンテンツに適用された繰り返し構造内で使用されている条件と区切り文字が表示されます。

1. テキストドキュメントフラグメントを保存し、関連するインタラクティブ通信のプレビューを表示します。フォームデータモデル内のデータに応じて、要素に適用されている繰り返し構造により、取引明細情報が以下のプレビュー画面のようにレンダリングされます。

   ![screen_shot_2018-03-09at155516copy](assets/screen_shot_2018-03-09at155516copy.png)

### 例：レターで繰り返しを使用して、クレジットカード取引情報のリストの書式設定、構造化および表示を行う場合 {#example-using-repeat-in-a-letter-to-format-structure-and-display-a-list-of-credit-card-transactions}

次の例は、繰り返しを使用して、レター内のクレジットカード取引情報を構造化しレンダリングする手順を示しています。同じような手順を使用して、別のシナリオでも繰り返しを使用できます。

1. 繰り返されるデータや動的なデータをレンダリングする DD 要素を含む（作成中または編集中の）テキストモジュールを開き、DD 要素の周囲に必要なテキストを埋め込みます。例えば、クレジットカードでの取引の明細を作成するため、テキストモジュールに以下の DD 要素が含まれています。

   ```javascript
   {^DD_creditcard_TransactionDate^} {^DD_creditcard_TransactionAmount^}
   {^DD_creditcard_TransactionType^}
   ```

   これらの DD 要素は、以下の情報を使用して、クレジットカードで行われた取引のリストをレンダリングします。

   取引日、取引額および取引タイプ（デビットまたはクレジット）

1. 次のように DD 要素の内部にテキストを埋め込んで、明細を読みやすくします。

   ![1_repeat](assets/1_repeat.png)

   ```javascript
   Date: {^DD_creditcard_TransactionDate^} Amount (USD): {^DD_creditcard_TransactionAmount^} Transaction Type: {^DD_creditcard_TransactionType^}
   ```

   ただし、適切に書式設定された明細をレンダリングするジョブはまだ完成していません。ここまでの作業結果に基づいてレターをレンダリングすると、次のように表示されます。

   ![1_1renderwithoutrepeat](assets/1_1renderwithoutrepeat.png)

   DD 要素と共に静的テキストを繰り返すには、この後の手順に従って繰り返しを適用する必要があります。

1. 以下に示すように、繰り返す静的テキストを DD 要素と共に選択します。

   ![2_repeat_selecttext](assets/2_repeat_selecttext.png)

1. 「**繰り返し**」を選択します。繰り返しダイアログボックスが開き、空のインライン条件が表示されます。

   ![3_repeat_dialog](assets/3_repeat_dialog.png)

1. 必要に応じて、取引を選択的にレンダリングする（例えば、50 セントを超える取引額をレンダリングする）ための条件を挿入します。

   ```javascript
   ${DD_creditcard_TransactionAmount > 0.5}
   ```

   情報（ここでは取引）を選択的にレンダリングする必要がない場合は、ダイアログボックス内の `${}` を削除して条件を空にします。繰り返し式が保存されるのは、繰り返し式ウィンドウが空になっている（繰り返し式が不要で ${} がない）場合、または繰り返し式ウィンドウに有効な繰り返し条件が含まれている場合です。

1. 動的テキストを書式設定するための区切り文字を選択し、チェックマークを選択して保存します。

   * **改行**：出力されるレターの各取引エントリの後に改行を挿入します。
   * **テキスト**：出力されるレターの各トランザクションエントリの後に指定したテキスト文字を挿入します。

   条件を挿入すると、繰り返しを設定したテキストが赤色でハイライト表示され、その左側にハンドルが表示されます。繰り返しの左側のハンドルにポインタを合わせると、繰り返し構造が表示されます。

   ![4_repeat_hoverdetail](assets/4_repeat_hoverdetail.png)

   ハンドルを選択すると繰り返しのポップアップメニューが表示され、繰り返し構造を編集または削除できます。

   ![5_repeateditremove](assets/5_repeateditremove.png)

1. 関連するレターをプレビューし、繰り返しに従ってテキストがレンダリングされることを確認します。DD 要素の値を入力するには、次を使用します。

   * サンプルデータを含むレターのプレビュー中に関連するデータディクショナリに基づいて作成されたサンプル XML データファイル。
   * 関連するデータディクショナリに添付されている XML データファイル。

   詳しくは、[データディクショナリ](https://helpx.adobe.com/jp/aem-forms/6-2/data-dictionary.html)を参照してください。

   ![6_repeatoutputpreview](assets/6_repeatoutputpreview.png)

   取引の明細とともに静的テキストが繰り返されています。この手順でテキストに適用した繰り返しによって、静的テキストの繰り返しが円滑におこなわれます。${DD_creditcard_TransactionAmount > 0.5} の条件を使用すると、USD 0.5 未満のトランザクションがレターにレンダリングされなくなります。

   >[!NOTE]
   >
   >条件と繰り返しの挿入は、関連するテキストモジュールの作成または編集中にのみ可能です。レターをプレビューする際、テキストモジュールを編集することはできますが、条件を挿入したり、繰り返しを実行することはできません。

## インライン条件と繰り返しの使用 - 一部の使用例  {#using-inline-condition-and-repeat-some-use-cases}

### 条件内で繰り返し {#repeat-within-condition}

1 つの条件内で繰り返しを使用する必要が生じる場合があります。Correspondence Management では、インライン条件構成内で繰り返しを使用できます。

例えば、条件（緑色で書式設定）内での繰り返し（赤色で書式設定）を次に示します。

繰り返しによってクレジットカードトランザクションがレンダリングされる間、${DD_creditcard_nooftransactions > 0} の条件では、少なくとも 1 つのトランザクションが存在する場合にのみ繰り返し構造がレンダリングされます。

![repeatwitincondition](assets/repeatwitincondition.png)

同様に、必要に応じて、以下を作成できます。

* 条件内の 1 つまたは複数の条件
* 繰り返し内の 1 つまたは複数の条件
* 条件または繰り返し内の条件と繰り返しの組み合わせ

### 空のインライン条件 {#empty-inline-condition}

空のインライン条件を挿入し、後でテキストと DD の要素を埋め込む必要がある場合もあります。Correspondence Management では、これを実行できます。

![emptycondition](assets/emptycondition.png)

ただし、可能な場合は、最初に意図した書式設定（箇条書きなど）でテキストモジュールにテキストと DD 要素を挿入し、後でインライン条件を適用することをお勧めします。
