---
title: AEM Sites ページへのアダプティブフォームの作成または追加
description: アダプティブフォームを容易に作成したり、シームレスに AEM Sites ページに追加したりする方法を学びます。動的でカスタマイズ可能なフォームを web サイトに統合し、デジタルエクスペリエンスを最適化して最大限の効果を得るための手順とベストプラクティスについて説明します。
Keywords: AEM Forms in sites, AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
feature: Adaptive Forms,Foundation Components
solution: Experience Manager, Experience Manager Forms
role: User, Developer
exl-id: 6e69ca67-883f-4079-96e2-5b7a9c843ada
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '2884'
ht-degree: 100%

---

# AEM Sites ページへのアダプティブフォームの作成または追加 {#create-or-add-an-adaptive-form-to-aem-sites-page}

<span class="preview">[アダプティブフォームの新規作成](/help/forms/using/create-an-adaptive-form-core-components.md)または [AEM Sites ページへのアダプティブフォームの追加](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md)には、最新の拡張可能なデータキャプチャ[コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=ja)を使用することをお勧めします。これらのコンポーネントは、アダプティブフォームの作成における大幅な進歩を表し、ユーザーエクスペリエンスの向上を実現します。この記事では、基盤コンポーネントを使用してアダプティブフォームを作成する古い方法について説明します。</span>

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM 6.5 | この記事 |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html?lang=ja) |

AEM Forms を使用すれば、アダプティブフォームを web ページにシームレスに組み込むことができます。これにより、訪問者は、ページを離れることなく、フォームに簡単に入力して送信できます。これにより、web サイト上の他の要素とのやり取りを容易に行いながら、フォームを積極的に操作できます。

AEM ページエディターを使用すると、複数のフォームをすばやく作成して AEM Sites ページに追加できます。AEM ページエディターを使用すると、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームのコンポーネントを活用して、Sites ページ内にシームレスなデータ取得エクスペリエンスを作成できます。また、バージョン管理、ターゲティング、翻訳およびマルチサイトマネージャーなど、AEM Sites ページの様々な機能を使用できます。

AEM Forms にはアダプティブフォームコンテナとアダプティブフォーム（埋め込みコンポーネント）が用意されています。アダプティブフォームコンテナを使用して、エクスペリエンスフラグメントまたは AEM Sites ページでフォームを作成できます。アダプティブフォーム（埋め込みコンポーネント）では、既存のアダプティブフォームを追加したり、アダプティブフォームエディターを使用してフォームを作成したりできます。

![サイトページ内のアダプティブフォーム](/help/forms/using/assets/adaptive-form-in-sites-page.png)

## アダプティブフォームコンテナコンポーネントを AEM ページエディターまたはエクスペリエンスフラグメントで使用するメリット

AEM ページエディターでアダプティブフォームコンテナを使用すると、動的な動作、検証、データ統合、レコードのドキュメントの生成、ビジネスプロセスの自動化など、アダプティブフォームコンポーネントを活用して、Sites ページ内にシームレスなデータ取得エクスペリエンスを作成できます。また、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sites ページの様々な機能を使用して、フォームの全体的な作成と管理のエクスペリエンスを強化できます。次の機能の一部を見てみましょう。

* **バージョン管理：** AEM Sites ページは、[堅牢なバージョン管理機能](/help/sites-authoring/working-with-page-versions.md)を提供し、フォームの様々なバージョンを追跡および管理できます。これにより、必要に応じて以前のバージョンにロールバックする機能を維持しながら、フォームに変更や機能強化を加えることができます。バージョン管理により、フォームの開発と進化に対する制御可能で体系的なアプローチが実現します。
* **ターゲティング（Adobe Target との統合）：** AEM Sites ページのターゲティング機能を使用して、[様々なオーディエンス向けにフォームエクスペリエンスをパーソナライズします](/help/sites-administering/target.md)。ユーザーセグメントおよびターゲティング条件を使用することで、特定のユーザーグループに合わせてフォームのコンテンツ、デザインまたは動作を調整できます。これにより、パーソナライズされた関連性の高いフォームエクスペリエンスを提供し、エンゲージメント率とコンバージョン率を高めることができます。
* **翻訳：** AEM Sites [翻訳サービスとのシームレスな統合](/help/sites-administering/translation.md)を使用すると、フォームを複数の言語に簡単に翻訳できます。この機能により、ローカライゼーションプロセスが簡素化され、グローバルなオーディエンスがフォームに確実にアクセスできるようになります。AEM 翻訳プロジェクト内で翻訳を効率的に管理できるので、多言語フォームのサポートに必要な時間と労力を削減できます。翻訳について詳しくは、考慮事項の節を参照してください。
* **マルチサイト管理とライブコピー：** AEM Sites [は堅牢なマルチサイト管理およびライブコピー機能](/help/sites-administering/msm.md)を提供し、単一の環境内で複数の web サイトを作成および管理できます。この機能を使用すると、異なるサイト間でフォームを再利用できるようになり、一貫性を確保し、重複作業を減らすことができます。一元化された制御と管理により、複数の web サイトにわたってフォームの管理と更新を効率的に行うことができます。
* **テーマ：** AEM Sites ページには、複数の web ページをまたいで一貫したビジュアルスタイルをデザインし、維持するためのフレームワークが用意されています。これらは、web サイトの全体的なルックアンドフィールに貢献するカラー、フォント、スタイルシートおよびその他のビジュアル要素を定義します。[アダプティブフォームで AEM Sites ページ用に設計されたテーマを使用することで、時間と労力を節約できます](/help/sites-authoring/style-system.md)。
* **タグ付け：** AEM Sites ページでは、[ページ、アセットまたは他のコンテンツへのタグやラベルの割り当て](/help/sites-authoring/tags.md)の操作を実行できます。タグは、特定の条件に基づいてコンテンツを分類および整理する方法を提供するキーワードまたはメタデータラベルです。AEM 内のページやアセットまたはその他のコンテンツ項目にタグを 1 つ以上割り当てて、検索を改善し、アセットを分類できるようにします。
* **コンテンツのロックとロック解除：** AEM Sites でユーザーは[ページへのアクセスと変更の制御](/help/sites-authoring/editing-content.md#locking-a-page-locking-a-page)を AEM Sites 環境内で実行できます。ページがロックされている場合、他のユーザーによる不正な変更や編集から保護されています。コンテンツをロックしたユーザーまたは指定された管理者のみが、ロックを解除して変更を許可できます。


## アダプティブフォームを AEM ページエディターに追加するための様々なオプション

次のオプションを使用すると、この機能を最大限に活用できます。

* **[カスタムアダプティブフォームを AEM Sites ページに追加する：](#create-an-adaptive-form-in-sites-editor)** 要件やデザインの好みに合わせてカスタマイズし、新規フォームをゼロから作成します。

* **[エクスペリエンスフラグメントにカスタムアダプティブフォームを追加する：](#create-an-adaptive-form-in-experience-fragment)** AEM エクスペリエンスフラグメントにフォームを追加して、フォームのリーチを拡張し、複数のページやサイトでシームレスに再利用できます。

* **[アダプティブフォームをエクスペリエンスフラグメントに変換する：](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)** AEM Sites ページに追加されたアダプティブフォームをエクスペリエンスフラグメントに変換して、複数の AEM Sites ページでフォームを再利用します。

* **承認済みのテンプレートに基づいてフォームを作成し、AEM Sites ページに追加する：**&#x200B;事前に承認されたテンプレートを活用して、組織のブランディングガイドラインやデザイン標準に合ったフォームをすばやく作成できます。このオプションは、アダプティブフォームエディターまたはアダプティブフォーム - 埋め込みコンポーネントでのみで使用できます。

* **既存のフォームを AEM Sites ページに追加する：**&#x200B;作成済みのフォームを web サイトに簡単に統合し、訪問者が直接操作できるようにします。このオプションは、アダプティブフォームエディターまたはアダプティブフォーム - 埋め込みコンポーネントでのみで使用できます。

* **複数のフォームを AEM Sites ページまたはエクスペリエンスフラグメントに追加する：**&#x200B;複数のフォームをページに追加して、ユーザーの環境設定や要件に基づいて複数の選択肢をユーザーに提供します。新規フォームと既存フォームを組み合わせることができます。

## 検討事項 {#consideration}

* アダプティブフォームコンテナを使用してフォームを作成または追加する場合、フォームは AEM Sites 翻訳フローを通じて翻訳およびローカライゼーションが実行されます。言語ごとに、Sites ページと対応するフォームの個別のコピー（言語コピー）が生成され、コンテンツ作成者が親ページのフォームのルールを変更する場合は、全言語のフォームのコピーで同じ変更を行う必要があります。アダプティブフォームコンテナでは、AEM Sites ページの様々な機能（バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど）を使用できます。

* アダプティブフォーム - 埋め込みコンポーネントを使用してフォームを作成または追加する場合、そのフォームは AEM Forms の翻訳フローを使用して翻訳およびローカライゼーションが実行されます。この場合、単一のフォームが維持され、Sites ページのすべての言語コピーで参照されます。アダプティブフォーム - 埋め込みコンポーネントでは、バージョン管理、ターゲティング、翻訳、マルチサイトマネージャーなど、AEM Sites ページの様々な機能にアクセスできません。


## 事前準備 {#before-you-start}

+++  環境でのアダプティブフォームコアコンポーネントの有効化

[アダプティブフォームコアコンポーネントがお使いの環境で有効になっていることを確認します](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/quick-setup/enable-headless-adaptive-forms-and-core-components.html?lang=ja)。

+++

+++  AEM Sites ページおよびエクスペリエンスフラグメントページコンポーネントに、アダプティブフォームクライアントライブラリを追加

アダプティブフォームコンテナコンポーネントの完全な機能を有効にするには、デプロイメントパイプラインを使用して、Customheaderlibs および Customfooterlibs クライアントライブラリを AEM Sites ページに追加します。ライブラリを追加するには、次の手順を実行します。

1. AEM オーサーインスタンスにログインし、CRX DE を開きます。ローカルで実行されるオーサーインスタンスのデフォルト URL は `http://localhost:4502/crx/de` です。

1. `/apps/[your-sites-project]/components/page/customheaderlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. `/apps/[your-sites-project]/components/page/customfooterlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. `/apps/[your-sites-project]/components/xfpage/customheaderlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. `/apps/[your-sites-project]/components/customfooterlibs.html` ファイルを開き、次のコードをファイルに追加します。

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. 環境内のすべてのオーサーインスタンスとパブリッシュインスタンスで、上記の手順を繰り返します。

+++

+++ アダプティブフォームコンテナの有効化

テンプレートのポリシーで[!UICONTROL アダプティブフォームコンテナ]コンポーネントを有効にするには、次の手順を実行します。

1. AEM Sites ページまたはエクスペリエンスフラグメントを編集用に開きます。ページを編集用に開くには、ページを選択して「編集」をクリックします。
1. Sites ページまたはエクスペリエンスフラグメントページのテンプレートを開きます。テンプレートを開くには、[!UICONTROL ページ情報]に移動し、![ページ情報](/help/forms/using/assets/Smock_Properties_18_N.svg)／[!UICONTROL テンプレートを編集]を選択します。対応するテンプレートがテンプレートエディターで開きます。
1. 構造ビューで、メニューバーから「**[!UICONTROL ポリシー]**」![ポリシー](/help/forms/using/assets/Smock_FeedManagement_18_N.svg)アイコンをクリックします。**[!UICONTROL 許可されたコンポーネント]**&#x200B;リストで、**[AEM アーキタイププロジェクト名] - アダプティブフォーム**&#x200B;の下にある&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;チェックボックスを選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## アダプティブフォームを作成します {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

要件やデザインの環境設定に合わせて、AEM Sites ページまたはエクスペリエンスフラグメント内で直接新しいフォームを最初から作成できます。単一用途のフォームの場合は、AEM Sites ページへの直接オーサリングをお勧めします。一方、エクスペリエンスフラグメントは、web サイトの複数のページで再利用する必要があるフォームに最適です。

* [AEM Sites ページでフォームを作成](#create-an-adaptive-form-in-sites-editor)
* [エクスペリエンスフラグメント内にフォームを作成](#create-an-adaptive-form-in-experience-fragment)
* [AEM Sites ページ内のアダプティブフォームをエクスペリエンスフラグメントに変換](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### AEM Sites ページでフォームを作成 {#create-an-adaptive-form-in-sites-editor}

AEM ページエディターのアダプティブフォームコンテナコンポーネントを使用して、カスタムフォームを作成できます。このコンポーネントを使用すると、フォームコンポーネントをドラッグ＆ドロップしてフォームを作成できます。フォームコンポーネントは、コアコンポーネントに基づいています。これらは、組織の要件に応じて簡単にカスタマイズできます。

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Sites ページでアダプティブフォームを作成するには、次の手順を実行します。

1. AEM Sites ページを編集モードで開きます。
1. **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;コンポーネントをコンポーネントブラウザーから Sites ページにラッグ＆ドロップします。ページ上にフォーム用のスペースが作成されます。レイアウトモードを使用して、コンテナスペースのサイズを変更できます。
1. アダプティブフォームのコアコンポーネントをコンテナスペースにドラッグ＆ドロップしてフォームを作成します。
1. 「送信」ボタンを追加します。

次に、[送信アクションを設定](#configure-submit-action-for-form)し、詳細プロパティを設定します。

### エクスペリエンスフラグメントでフォームを作成 {#create-an-adaptive-form-in-experience-fragment}

フォームを AEM エクスペリエンスフラグメントに追加すると、フォームの範囲を拡張して、複数のページやサイトでシームレスに再利用できます。例えば、エクスペリエンスフラグメント内にニュースレターのサインアップフォームを含めることができます。これにより、web サイトの複数のページでフラグメントを簡単に再利用できるので、フォームを繰り返し再作成する必要がなくなります。エクスペリエンスフラグメント内のニュースレターサインアップフォームに加えた更新や変更は、同じフォームを使用しているすべてのページに自動的に反映されます。これにより、プロセスが合理化され、web サイトのフォームの管理をシンプル化しながら、ユーザーエクスペリエンスをシームレス化することができます。

エクスペリエンスフラグメント内にアダプティブフォームを作成するには、次の手順を実行します。

1. エクスペリエンスフラグメントを開きます。
1. **[!UICONTROL アダプティブフォームコンテナ]**&#x200B;コンポーネントを、コンポーネントブラウザーからエクスペリエンスフラグメントにドラッグ＆ドロップします。
1. アダプティブフォームコアコンポーネントをエクスペリエンスフラグメントのコンテナスペースにドラッグ＆ドロップして、フォームを作成します。
1. 「送信」ボタンを追加します。

次に、[送信アクションを設定](#configure-submit-action-for-form)し、詳細プロパティを設定します。

### AEM Sites ページ内のアダプティブフォームをエクスペリエンスフラグメントに変換 {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Sites ページエディター内にある既存のアダプティブフォームをエクスペリエンスフラグメントに変換すると、複数のページやサイトでフォームを再利用できます。

AEM Sites ページ内のアダプティブフォームをエクスペリエンスフラグメントに変換するには、次の手順を実行します。

1. アダプティブフォームを含む AEM Sites ページ（アダプティブフォームコンテナコンポーネント内）を編集モードで開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。
1. メニューバーで、![「エクスペリエンスフラグメントバリエーションに変換」アイコン](/help/forms/using/assets/Smock_FilingCabinet_18_N.svg)を選択します。「エクスペリエンスフラグメントバリエーションに変換」アイコン。
   ![Sites ページ内のフォームをエクスペリエンスフラグメントに変換](/help/forms/using/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   アダプティブフォームコンテナを新しいエクスペリエンスフラグメントに変換するか、既存のエクスペリエンスフラグメントに追加するためのダイアログボックスが表示されます。
1. エクスペリエンスフラグメントバリエーションに変換ダイアログボックスで、次のオプションの値を設定します。

   * **アクション：**&#x200B;新しいエクスペリエンスフラグメントを作成するか、既存のエクスペリエンスフラグメントに追加するかを選択します。
   * **親パス：**&#x200B;エクスペリエンスフラグメントをホストするフォルダーのパスを指定します。このオプションは、エクスペリエンスフラグメントを作成する場合にのみ使用できます。
   * **テンプレート：**&#x200B;エクスペリエンスフラグメントテンプレートのパスを指定します。エクスペリエンスフラグメントテンプレートがない場合は、[作成します](/help/sites-developing/experience-fragments.md)。このオプションは、アダプティブフォームを既存のエクスペリエンスフラグメントに追加する場合にのみ使用できます。
   * **フラグメントのタイトル：**&#x200B;エクスペリエンスフラグメントのタイトルを指定します。タイトルは、エクスペリエンスフラグメントを一意に識別します。


## フォームの送信アクションを設定 {#configure-submit-action-for-form}

送信アクションを使用すると、アダプティブフォーム経由で取り込んだデータの送信先を選択できます。送信アクションは、ユーザーがアダプティブフォームの「送信」ボタンをクリックするとトリガーされます。 アダプティブフォームには、すぐに使用できる送信アクションがいくつか含まれています。 デフォルトの送信アクションを拡張して、独自のカスタム送信アクションを作成することもできます。 フォームの送信アクションを設定するには、次の手順を実行します。

1. アダプティブフォームを含む、AEM ページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。
1. アダプティブフォームコンテナプロパティ（![アダプティブフォームコンテナプロパティ](/help/forms/using/assets/configure-icon.svg)アイコン）をクリックします。送信アクションを設定するための、アダプティブフォームコンテナダイアログボックスが開きます。
   ![アダプティブフォームコンテナ](/help/forms/using/assets/adaptive-forms-container.png)
1. 必要に応じて、送信アクションを選択して設定します。送信アクションについての詳細情報は、[アダプティブフォームの送信アクション](configuring-submit-actions.md)を参照してください。


## フォームのスキーマまたはフォームデータモデルを設定 {#configure-schema-or-data-model-for-form}

フォームデータモデルを使用してフォームをデータソースに接続し、ユーザーのアクションに基づいてデータを送受信することができます。また、フォームを JSON スキーマに接続して、送信されたデータを事前定義済みの形式で受信することもできます。

フォームをスキーマまたはフォームデータモデルに接続する前に

* [JSON スキーマの作成と環境へのアップロード](adaptive-form-json-schema-form-model.md)
* [フォームデータモデルを作成](create-form-data-models.md)

フォームの JSON スキーマまたはフォームデータモデルを設定するには、次の手順を実行します。

1. アダプティブフォームを含む、AEM ページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。
1. アダプティブフォームコンテナプロパティ（![アダプティブフォームコンテナプロパティ](/help/forms/using/assets/configure-icon.svg)アイコン）をクリックします。データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
   ![フォームデータモデルのアダプティブフォームコンテナ](/help/forms/using/assets/form-data-model-adaptive-forms-container.png)
1. 必要に応じて、JSON スキーマまたはフォームデータモデルを選択し、設定します。 送信アクションについて詳しくは、[アダプティブフォーム送信アクション](configuring-submit-actions.md)を参照してください。

   * 「**[!UICONTROL フォームモデル]**」オプションを選択する場合は、「**[!UICONTROL フォームデータモデルを選択]**」オプションを使用して、事前設定済みのフォームデータモデルを選択します。
   * 「**[!UICONTROL スキーマ]**」オプションを選択する場合は、「**[!UICONTROL スキーマ]**」オプションを使用して、フォームの JSON スキーマを選択します。

1. 「**[!UICONTROL 完了]**」をクリックします。

## フォームの事前入力サービスを設定 {#configure-prefill-service-for-form}

事前入力サービスを使用すると、既存のデータを使用してアダプティブフォームのフィールドに自動で入力することができます。ユーザーがフォームを開くと、これらのフィールドの値は事前入力されています。 以下の操作を実行できます。

* [カスタム事前入力サービスを作成](prepopulate-adaptive-form-fields.md)
* [フォームデータモデルの事前入力サービスを使用](#fdm-prefill-service)

### フォームデータモデルの事前入力サービスを使用 {#fdm-prefill-service}

フォームデータモデルの事前入力サービスを使用すると、設定済みのフォームデータモデルを使用してフォームのフィールドに事前入力できます。フォームデータモデルの事前入力サービスでは、[設定済みのフォームデータモデルのサービスを取得](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services)を使用して、データを取得します。アダプティブフォームでフォームデータモデルの事前入力サービスを使用するには、次の手順を実行します。

1. アダプティブフォームを含む、AEM ページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。
1. アダプティブフォームコンテナプロパティ（![アダプティブフォームコンテナプロパティ](/help/forms/using/assets/configure-icon.svg)アイコン）をクリックします。データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
   ![事前入力サービス FDM AEM Sites ページエディター](/help/forms/using/assets/prefill-service-fdm-aem-sites-page-editor.png)
1. フォームデータモデルを選択. 「**[!UICONTROL 基本]**」タブを開きます。事前入力サービスで、「**[!UICONTROL フォームポータルドラフト事前入力サービス]**」を選択します。
1. 「**[!UICONTROL 完了]**」をクリックします。

## フォーム送信時にユーザーを新しいユーザーにリダイレクトするか、お礼のメッセージを表示

フォームの送信時に、ユーザーを別の web ページまたはメッセージにリダイレクトできます。ユーザーをリダイレクトするか、お礼のメッセージを設定するには、次の手順を実行します。

1. アダプティブフォームを含む、AEM ページエディターまたはエクスペリエンスフラグメントを開きます。
1. コンテンツツリーを開き、アダプティブフォームをホストする&#x200B;**[!UICONTROL アダプティブフォームコンテナ]**&#x200B;を選択します。1 つの AEM Sites ページで複数のアダプティブフォームをホストできます。したがって、適切なアダプティブフォームコンテナを慎重に選択してください。
1. アダプティブフォームコンテナプロパティ（![アダプティブフォームコンテナプロパティ](/help/forms/using/assets/configure-icon.svg)アイコン）をクリックします。データモデルを設定するためのアダプティブフォームコンテナダイアログボックスが開きます。
1. 「**[!UICONTROL 送信]**」タブを開きます。

   * リダイレクト URL を設定するには、「送信」オプションで「URL にリダイレクト」オプションを選択し、AEM Sites ページの絶対アドレス、リダイレクト URL、または相対パスを指定します。

   * カスタムメッセージまたはお礼のメッセージを設定するには、「送信」オプションで「メッセージを表示」オプションを選択し、メッセージコンテンツボックスにメッセージを入力します。これはリッチテキストボックスで、全画面表示オプションを使用して、使用可能なすべてのリッチテキスト項目を表示できます。

## 関連トピック {#see-also}

* [スタンドアロンのコアコンポーネントベースのアダプティブフォームを作成](/help/forms/using/create-an-adaptive-form-core-components.md)
* [フォームのスタイルまたはテーマを作成](/help/forms/using/create-or-customize-themes-for-adaptive-forms-core-components.md)
