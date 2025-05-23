---
title: 'ContextHub でのセグメント化の設定 '
description: ContextHub でのセグメント化の設定方法について説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Administering,Personalization
role: Admin
exl-id: e024c456-1d50-4ff2-bfb6-aca1cca31632
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 100%

---

# ContextHub でのセグメント化の設定 {#configuring-segmentation-with-contexthub}

>[!NOTE]
>
>この節では、ContextHub を使用したセグメント化の設定について説明します。ClientContext 機能を使用する場合は、[ClientContext のセグメント化の設定](/help/sites-administering/campaign-segmentation.md)に関するドキュメントを参照してください。
>

キャンペーンを作成する場合、セグメント化を考えることが重要になります。セグメント化の仕組みと主な用語について詳しくは、[オーディエンスの管理](/help/sites-authoring/managing-audiences.md)を参照してください。

サイト訪問者についてこれまでに収集した情報と、達成する目標に応じて、ターゲットコンテンツに必要なセグメントと戦略を定義する必要があります。

このようなセグメントを使用して、訪問者に特定のターゲットコンテンツを提供します。このコンテンツは、web サイトの「[パーソナライズ機能](/help/sites-authoring/personalization.md)」セクションで管理されます。ここで定義した[アクティビティ](/help/sites-authoring/activitylib.md)は、任意のページに追加でき、専用のコンテンツを適用できる訪問者セグメントを指定できます。

AEM では、ユーザーエクスペリエンスを簡単にパーソナライズできます。また、セグメント定義の結果を検証することもできます。

## セグメントへのアクセス {#accessing-segments}

[オーディエンス](/help/sites-authoring/managing-audiences.md)コンソールは、ContextHub または ClientContext のセグメントを管理したり、Adobe Target アカウントのオーディエンスを管理したりする目的で使用します。このドキュメントでは、ContextHub のセグメントの管理について取り上げます。[ClientContext セグメント](/help/sites-administering/campaign-segmentation.md)および Adobe Target セグメントについては、それぞれ関連するドキュメントを参照してください。

セグメントにアクセスするには、設定を選択する必要があります。 グローバルナビゲーションで、**ナビゲーション／パーソナライズ機能／オーディエンス**&#x200B;を選択します。利用可能な設定が表示されます。

![オーディエンス - 設定](assets/segmentation-access-confs.png)

設定を選択して、セグメントを表示します（例： WKND サイト）。

![オーディエンス - セグメント](assets/segmentation-access-segments.png)

## セグメントエディター {#segment-editor}

**セグメントエディター**&#x200B;を使用すると、セグメントを簡単に変更できます。セグメントを編集するには、[セグメントリスト](/help/sites-administering/segmentation.md#accessing-segments)からセグメントを選択し、「**編集**」ボタンをクリックします。

![segmenteditor](assets/segmenteditor.png)

コンポーネントブラウザーを使用すると、**AND** および **OR** コンテナを追加してセグメントロジックを定義してから、別のコンポーネントを追加してプロパティや値を比較できます。また、スクリプトやその他のセグメントを参照して選択条件を定義する（[新しいセグメントの作成](#creating-a-new-segment)を参照）ことによって、セグメントの選択シナリオを正確に定義できます。

ステートメント全体が true と評価されると、セグメントは解決されます。複数の適用可能なセグメントがある場合、**ブースト**&#x200B;係数も使用されます。[ブースト係数](/help/sites-administering/campaign-segmentation.md#boost-factor)について詳しくは、「[新しいセグメントの作成](#creating-a-new-segment)」を参照してください。

>[!CAUTION]
>
>セグメントエディターは、循環参照をチェックしません。例えば、セグメント A が別のセグメント B を参照していて、そのセグメント B がセグメント A を参照している場合などです。このため、セグメントに循環参照が存在しないことを確認してください。

### コンテナ {#containers}

次のコンテナは標準で用意されており、比較や参照をグループ化してブーリアン評価を行うために使用できます。これらはコンポーネントブラウザーからエディターにドラッグできます。詳しくは、「[AND コンテナと OR コンテナの使用](/help/sites-administering/segmentation.md#using-and-and-or-containers)」の節を参照してください。

<table>
 <tbody>
  <tr>
   <td>コンテナ AND<br /> </td>
   <td>AND ブール演算子<br /> </td>
  </tr>
  <tr>
   <td>コンテナ OR<br /> </td>
   <td>OR ブール演算子</td>
  </tr>
 </tbody>
</table>

### 比較 {#comparisons}

次のセグメント比較は標準で用意されており、セグメントプロパティを評価するために使用できます。これらはコンポーネントブラウザーからエディターにドラッグできます。

<table>
 <tbody>
  <tr>
   <td>プロパティ - 値<br /> </td>
   <td>ストアのプロパティと定義済みの値を比較<br /> </td>
  </tr>
  <tr>
   <td>プロパティ - プロパティ</td>
   <td>ストアの 1 つのプロパティと別のプロパティを比較<br /> </td>
  </tr>
  <tr>
   <td>プロパティ - セグメントの参照</td>
   <td>ストアのプロパティと別の参照セグメントを比較<br /> </td>
  </tr>
  <tr>
   <td>プロパティ - スクリプトの参照</td>
   <td>ストアのプロパティとスクリプトの結果を比較<br /> </td>
  </tr>
  <tr>
   <td>セグメントリファレンス - スクリプトリファレンス</td>
   <td>参照セグメントとスクリプトの結果を比較<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>値の比較時に比較のデータタイプが設定されていない場合（つまり、自動検出に設定されている場合）、ContextHub のセグメント化エンジンでは、javascript と同じように値が比較されます。値が想定されたタイプにキャストされないので、誤解を招く結果となることがあります。例：
>
>`null < 30 // will return true`
>
>したがって、[セグメントの作成](/help/sites-administering/segmentation.md#creating-a-new-segment)時に比較対象の値のタイプがわかる場合は、常に&#x200B;**データタイプ**&#x200B;を選択してください。例：
>
>`profile/age` プロパティを比較する場合は、比較対象のタイプが&#x200B;**数値**&#x200B;であることが既にわかっているので、`profile/age` が設定されていなくても、`profile/age` が 30 より小さいという比較では、想定どおりに **false** が返されます。

### 参照 {#references}

次の参照は標準で用意されており、スクリプトや別のセグメントに直接リンクするために使用できます。これらはコンポーネントブラウザーからエディターにドラッグできます。

<table>
 <tbody>
  <tr>
   <td>セグメントの参照<br /> </td>
   <td>参照先セグメントを評価</td>
  </tr>
  <tr>
   <td>スクリプト参照</td>
   <td>参照先セグメントをします。詳しくは、次の「<a href="/help/sites-administering/segmentation.md#using-script-references">スクリプト参照の使用</a>」の節を参照してください。</td>
  </tr>
 </tbody>
</table>

## 新しいセグメントの作成 {#creating-a-new-segment}

新しいセグメントを定義するには、次の手順に従います。

1. [セグメントにアクセス](/help/sites-administering/segmentation.md#accessing-segments)した後、セグメントを作成する[フォルダーに移動](#organizing-segments)します。

1. 「作成」ボタンをクリックし、「**ContextHub セグメントを作成**」を選択します。

   ![chlimage_1-311](assets/chlimage_1-311.png)

1. 「**新しい ContextHub セグメント**」で、セグメントのタイトルと必要に応じてブースト値を入力し、「**作成**」をクリックします。

   ![chlimage_1-312](assets/chlimage_1-312.png)

   各セグメントには、重み付け係数として使用されるブーストパラメーターがあります。複数のセグメントが有効である場合、数値が小さいセグメントよりも、数値が大きいセグメントのほうが優先して選択されます。

   * 最小値：`0`
   * 最大値：`1000000`

1. 比較または参照をセグメントエディターにドラッグすると、デフォルトの AND コンテナに表示されます。
1. 新しい参照またはセグメントの設定オプションをダブルクリックして、特定のパラメーターを編集します。この例では、サンノゼの人物をテストしています。

   ![screen_shot_2012-02-02at103135am](assets/screen_shot_2012-02-02at103135ama.png)

   比較が適切に評価されるように、可能であれば常に&#x200B;**データタイプ**&#x200B;を設定します。詳しくは、[比較](/help/sites-administering/segmentation.md#comparisons)を参照してください。

1. 「**OK**」をクリックして定義を保存します。
1. 必要に応じてその他のコンポーネントを追加します。AND 比較および OR 比較のコンテナコンポーネントを使用して、ブーリアン式を作成できます（後述の [AND コンテナと OR コンテナの使用](/help/sites-administering/segmentation.md#using-and-and-or-containers)を参照）。セグメントエディターでは、不要になったコンポーネントを削除したり、コンポーネントをステートメント内の別の場所へドラッグしたりすることができます。

### AND コンテナと OR コンテナの使用 {#using-and-and-or-containers}

AND および OR コンテナコンポーネントを使用すると、AEM で複雑なセグメントを作成できます。これを行う際に、次の基本事項に留意してください。

* 定義の最上位レベルは必ず、最初に作成された AND コンテナになります。これは変更できませんが、他のセグメント定義には影響しません。
* コンテナのネストが意味のあるものになっていることを確認してください。コンテナは、ブール式の括弧として見ることができます。

次の例では、プライムエイジグループに属すると見なされる訪問者を選択しています。

30 才～ 59 才の男性

OR

30 才～ 59 才の女性

最初に、OR コンテナコンポーネントをデフォルトの AND コンテナ内に配置します。OR コンテナ内に 2 つの AND コンテナを追加し、それらの両方にプロパティまたは参照コンポーネントを追加できます。

![screen_shot_2012-02-02at105145am](assets/screen_shot_2012-02-02at105145ama.png)

### スクリプト参照の使用 {#using-script-references}

スクリプト参照コンポーネントを使用すると、セグメントプロパティの評価を外部スクリプトに委任できます。スクリプトが適切に設定されると、セグメント条件の他のコンポーネントと同じように使用できます。

#### 参照するスクリプトの定義 {#defining-a-script-to-reference}

1. `contexthub.segment-engine.scripts` クライアントライブラリにファイルを追加します。
1. 値を返す関数を実装します。例：

   ```
   ContextHub.console.log(ContextHub.Shared.timestamp(), '[loading] contexthub.segment-engine.scripts - script.profile-info.js');
   
   (function() {
       'use strict';
   
       /**
        * Sample script returning profile information. Returns user info if data is available, false otherwise.
        *
        * @returns {Boolean}
        */
       var getProfileInfo = function() {
           /* let the SegmentEngine know when script should be re-run */
           this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
           this.dependOn(ContextHub.SegmentEngine.Property('profile/givenName'));
   
           /* variables */
           var name = ContextHub.get('profile/givenName');
           var age = ContextHub.get('profile/age');
   
           return name === 'Joe' && age === 123;
       };
   
       /* register function */
       ContextHub.SegmentEngine.ScriptManager.register('getProfileInfo', getProfileInfo);
   
   })();
   ```

1. スクリプトを `ContextHub.SegmentEngine.ScriptManager.register` に登録します。

その他のプロパティに依存するスクリプトでは、`this.dependOn()` を呼び出す必要があります。例えば、スクリプトが `profile/age` に依存する場合は次のようになります。

```
this.dependOn(ContextHub.SegmentEngine.Property('profile/age'));
```

#### スクリプトの参照 {#referencing-a-script}

1. ContextHub セグメントを作成します。
1. **スクリプト参照**&#x200B;コンポーネントをセグメントの目的の場所に追加します。
1. **スクリプト参照**&#x200B;コンポーネントの編集ダイアログを開きます。スクリプトが[適切に設定](/help/sites-administering/segmentation.md#defining-a-script-to-reference)されていれば、**スクリプト名**&#x200B;ドロップダウンに表示されます。

## セグメントの整理 {#organizing-segments}

多数のセグメントがある場合は、フラットリストとして管理しにくくなる可能性があります。このような場合は、フォルダーを作成してセグメントを管理すると便利です。

### 新しいフォルダーの作成 {#create-folder}

1. [セグメントへのアクセス](#accessing-segments)後、「**作成**」ボタンをクリックし、「**フォルダー**」を選択します。

   ![フォルダーの追加](assets/contexthub-create-segment.png)

1. フォルダーの「**タイトル**」と「**名前**」を指定します。
   * **タイトル**&#x200B;は内容がわかるように付けます。
   * **名前**&#x200B;はリポジトリのノード名になります。
      * タイトルに基づいて自動的に生成され、[AEM の命名規則](/help/sites-developing/naming-conventions.md)に従って調整されます。
      * 必要に応じて調整できます。

   ![フォルダーを作成](assets/contexthub-create-folder.png)

1. 「**作成**」をクリックします。

   ![フォルダーの確認](assets/contexthub-confirm-folder.png)

1. フォルダーがセグメントのリストに表示されます。
   * 列の並べ替え方法によって、リスト内の新しいフォルダーの表示場所が異なります。
   * 列見出しをクリックすると、並べ替えを調整できます。
     ![新規フォルダー](assets/contexthub-folder.png)

### 既存のフォルダーの変更 {#modify-folders}

1. [セグメントへのアクセス](#accessing-segments)後、変更するフォルダーをクリックして選択します。

   ![フォルダーの選択](assets/contexthub-select-folder.png)

1. ツールバーの「**名前を変更**」をクリックして、フォルダーの名前を変更します。

1. 新しい「**フォルダーのタイトル**」を指定し、「**保存**」をクリックします。

   ![フォルダー名の変更](assets/contexthub-rename-folder.png)

>[!NOTE]
>
>フォルダー名を変更する場合は、タイトルのみ変更できます。名前は変更できません。

### フォルダーの削除

1. [セグメントへのアクセス](#accessing-segments)後、変更するフォルダーをクリックして選択します。

   ![フォルダーの選択](assets/contexthub-select-folder.png)

1. ツールバーで「**削除**」をクリックし、フォルダーを削除します。

1. 削除対象として選択したフォルダーのリストがダイアログに表示されます。

   ![削除の確認](assets/contexthub-confirm-segment-delete.png)

   * 「**削除**」をクリックして確認します。
   * 「**キャンセル**」をクリックして中止します。

1. 選択したフォルダーのいずれかにサブフォルダーまたはセグメントが含まれている場合は、それらの削除も確認する必要があります。

   ![子の削除の確認](assets/contexthub-confirm-segment-child-delete.png)

   * 「**削除を強制**」をクリックして確定します。
   * 「**キャンセル**」をクリックして中止します。

>[!NOTE]
>
>セグメントをフォルダー間で移動することはできません。

## セグメントの適用のテスト {#testing-the-application-of-a-segment}

セグメントを定義したら、**[ContextHub](/help/sites-authoring/ch-previewing.md)** を使用して、考えられる結果についてテストすることができます。

1. ページをプレビュー
1. ContextHub アイコンをクリックして ContextHub ツールバーを表示します。
1. 作成したセグメントと一致するペルソナを選択します。
1. ContextHub によって、選択したペルソナに適用できるセグメントが解決されます。

例えば、この例のプライムエイジグループに属するユーザーを識別するための単純なセグメント定義は、ユーザーの年齢と性別に基づいています。これらの条件に一致する特定のペルソナを読み込むと、次のようにセグメントが正常に解決されたかどうかがわかります。

![screen_shot_2012-02-02at105926am](assets/screen_shot_2012-02-02at105926am.png)

解決されていない場合は次のようになります。

![screen_shot_2012-02-02at110019am](assets/screen_shot_2012-02-02at110019am.png)

>[!NOTE]
>
>すべての特性がただちに解決されます。ただし、ほとんどの特性はページを再読み込みしたときにのみ変更されます。

このようなテストは、ターゲットコンテンツや関連する&#x200B;**アクティビティ**&#x200B;および&#x200B;**エクスペリエンス**&#x200B;と組み合わせて、コンテンツページでも実行できます。

前述のプライムエイジグループセグメントの例を使用してアクティビティおよびエクスペリエンスを設定した場合は、そのアクティビティを使用してセグメントを簡単にテストできます。アクティビティの設定について詳しくは、[ターゲットコンテンツのオーサリングに関するドキュメント](/help/sites-authoring/content-targeting-touch.md)を参照してください。

1. ターゲットコンテンツを設定したページの編集モードでは、ターゲットとなるコンテンツが矢印アイコンによって示されます。

   ![chlimage_1-313](assets/chlimage_1-313.png)

1. プレビューモードに切り替えてから、ContextHub を使用して、エクスペリエンスに設定されているセグメント化と一致しないペルソナに切り替えます。

   ![chlimage_1-314](assets/chlimage_1-314.png)

1. エクスペリエンスに設定されているセグメント化と一致するペルソナに切り替え、それに応じてエクスペリエンスが変化することを確認します。

   ![chlimage_1-315](assets/chlimage_1-315.png)

## セグメントの使用 {#using-your-segment}

これらのセグメントを使用すると、特定ターゲットオーディエンスに向けられた実際のコンテンツを制御できます。オーディエンスおよびセグメントについて詳しくは、[オーディエンスの管理](/help/sites-authoring/managing-audiences.md)を参照してください。オーディエンスおよびセグメントを使用したコンテンツのターゲティングについては、[ターゲットコンテンツのオーサリング](/help/sites-authoring/content-targeting-touch.md)を参照してください。
