---
title: '分析とレポートの設定 '
description: Adobe Analytics を設定して、アダプティブフォーム、アダプティブドキュメント、HTML5 フォームの使用時に発生するインタラクションのパターンやユーザーが直面する問題の検出方法について学びます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
feature: Adaptive Forms
exl-id: befc6b96-517b-4ca3-8007-2aa0fd6ed2cb
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 100%

---

# Cloud Service フレームワークを使用した Analytics {#analyticsusingcloudframework}

AEM Forms は Analytics と統合されており、公開中のフォームやドキュメントのパフォーマンス指標を取得およびトラックできます。これらの指標分析の意図は、フォームやドキュメントをさらに使いやすくするために必要な変更に関して、十分な情報に基づいた決定を行えるよう支援することです。

>[!NOTE]
>
>AEM Forms の分析機能は、AEM Forms のアドオンパッケージの一部として利用できます。アドオンパッケージのインストールについて詳しくは、[AEM Forms のインストールと設定](../../forms/using/installing-configuring-aem-forms-osgi.md)を参照してください。
>
>アドオンパッケージの他に、Adobe Analytics のアカウントと AEM インスタンスでの管理者権限が必要になります。解決方法について詳しくは、[Adobe Analytics](https://www.adobe.com/jp/solutions/digital-analytics.html) を参照してください。

Adobe Launch を使用して分析することもできます。 AEM Forms を Adobe Launch と統合する方法について詳しくは、[Adobe Launch を使用した分析](/help/forms/using/integrate-aem-forms-with-adobe-analytics.md)を参照してください。

## 概要 {#overview}

Adobe Analytics を使用して、アダプティブフォーム、HTML5 フォーム、インタラクティブ通信でユーザーが実行する操作のパターンを検出することができます。また、これらのフォームをユーザーが使用する場合の問題についても、特定することができます。初期設定では、Adobe Analytics は次のパラメーターに関する情報を追跡して保存します。

* **平均記入時間**：フォームの記入にかかった平均時間。
* **レンディション**：フォームが開かれた回数。
* **ドラフト**：ドラフト状態でフォームが保存される回数。
* **送信**：フォームが送信された回数。
* **中断**：ユーザーがフォームを完了せずに終了した回数。

Adobe Analytics をカスタマイズして、追加のパラメーターを追加または削除できます。上記の情報と共に、レポートには HTML5 およびアダプティブフォームのすべてのパネルに関する次の情報が含まれています。

* **時間**：パネルおよびパネルのフィールドで費やした時間。
* **エラー**：パネルおよびパネルのフィールドで発生したエラーの回数。
* **ヘルプ**：ユーザーがパネルおよびパネルのフィールドのヘルプを開いた回数。

## レポートスイートの作成 {#creating-report-suite}

分析データは、レポートスイートと呼ばれる顧客固有のリポジトリに保存されます。レポートスイートを作成して Adobe Analytics を使用するには、有効な Adobe Marketing Cloud アカウントが必要です。次の手順を実行する前に、有効な Adobe Marketing Cloud アカウントを保有していることを確認してください。

次の手順を実行して、レポートスイートを作成します。

1. [https://sc.omniture.com/login/](https://sc.omniture.com/login/) にログインします。
1. Marketing Cloud で、「**管理者**／**管理コンソール**／**レポートスイート**」の順に選択します。
1. Report Suite Manager で、**新規作成**／**レポートスイート**&#x200B;を選択します。

   ![新しいレポートスイートの作成](assets/newreportsuite_new.png)

   新しいレポートスイートの作成

1. 最初のドロップダウンリストを「**テンプレートから作成する**」に設定して、「**コマース**」を選択します。
1. **レポートスイート ID** フィールドを見つけ、新規レポートスイート ID を追加します（例：JJEsquire）。レポートスイート ID は、レポートスイート ID フィールドの下に表示されます。ID には自動でプレフィックスが追加されます。多くの場合、会社名が使用されます。
1. 新しい&#x200B;**サイトのタイトル**&#x200B;を追加します。例えば、JJEsquire Getting Started Suite とします。このタイトルは、Analytics UI 内で使用されます。コード内でレポートスイート ID を使用します。
1. ドロップダウンから「**タイムゾーン**」を選択します。このレポートスイートに含められるすべてのデータは、定義済みのタイムゾーンに基づいて記録されます。
1. **ベース URL** フィールドと&#x200B;**デフォルトページ**&#x200B;フィールドは空にしておきます。これら 2 つの値は、Adobe Marketing Cloud インターフェイスからのみ使用して、自分の web サイトにリンクします。
1. **Go Live 日**&#x200B;は today にしておきます。この Go Live 日で、レポートスイートがアクティベートされる日が決定されます。
1. 「**日別予想ページビュー数**」フィールドに、100 を入力します。このフィールドを使用して、web サイトの予想される日別のページビュー数を見積もります。この概算から Adobe は、収集していくデータを処理するために必要な適切な量のハードウェアを整備することができます。
1. ドロップダウンリストから「**ベース通貨**」を選択します。このレポートスイートに含められるすべての通貨データは、この通貨形式に変換されて保存されます。
1. 「**レポートスイートの作成**」をクリックします。レポートスイートが正常に作成されたことを通知するメッセージ付きのページ更新が表示されます。
1. 新規作成されたレポートスイートを選択します。**設定を編集**／**一般**／**一般的なアカウント設定**&#x200B;の順に移動します。

   ![一般的なアカウント設定](assets/geographic_settings.png)

   一般的なアカウント設定

1. 一般的なアカウント設定の画面で、「**地域レポート**」を有効化し、「**保存**」をクリックします。
1. **設定を編集**／**トラフィック**／**トラフィック変数**&#x200B;の順に移動します。
1. レポートスイートで、次のトラフィック変数を設定し、有効化します。

   * **formName**：アダプティブフォームの識別子。
   * **formInstance**：アダプティブフォームインスタンスの識別子。この変数のパスレポートを有効にします。
   * **fieldName**：アダプティブフォームフィールドの識別子。この変数のパスレポートを有効にします。
   * **panelName**：アダプティブフォームパネルの識別子。この変数のパスレポートを有効にします。
   * **formTitle**：フォームのタイトル。
   * **fieldTitle**：フォームフィールドのタイトル。
   * **panelTitle**：フォームパネルのタイトル。
   * **analyticsVersion**：フォーム分析のバージョン。

1. 「**設定の編集**／**コンバージョン**／**成功イベント**」の順に移動します。次の成功イベントを定義し、有効化します。

   | 成功イベント | タイプ |
   |---|---|
   | abandon | カウンター |
   | render | カウンター |
   | panelVisit | カウンター |
   | fieldVisit | カウンター |
   | 保存 | カウンター |
   | エラー | カウンター |
   | help | カウンター |
   | 送信 | カウンター |
   | timeSpent | 数値 |

   >[!NOTE]
   >
   >AEM Forms 分析の設定に使用されるイベント番号と prop 番号は、[AEM Analytics](/help/sites-administering/adobeanalytics.md) 設定で使用されるイベント番号と prop 番号とは異なる番号にする必要があります。

1. Adobe Marketing Cloud アカウントからログアウトします。

## クラウドサービス設定の作成 {#creating-cloud-service-configuration}

クラウドサービス設定は、Adobe Analytics アカウントに関する情報です。この設定で Adobe Experience Manager（AEM）を有効化し、Adobe Analytics に接続します。使用する各 Analytics アカウントに対してそれぞれ個別の設定を作成します。

1.  管理者として、AEM のオーサーインスタンスにログインします。
1. 左上隅で、 **Adobe Experience Manager**／**ツール** ![ハンマーアイコン](/help/forms/using/assets/tools.png)／**クラウドサービス**／**従来のクラウドサービス**&#x200B;をクリックします。
1. 「**Adobe Analytics**」アイコンを見つけます。「**設定を表示**」をクリックし、**[+]** をクリックして次に進み、新しい設定を追加します。

   初めて利用する場合は、「**今すぐ設定**」をクリックします。

1. 新しい設定にタイトルを追加します（名前フィールドへの記入はオプションです）。例えば、My analytics configuration などとします。「**作成**」をクリックします。

1. 設定ページで編集パネルが開いたら、次のフィールドに記入します。

   * **会社**：Adobe Analytics で使用されている会社名
   * **ユーザー名**：Adobe Analytics へのログインに使用する名前
   * **パスワード**：前述したアカウントの Adobe Analytics のパスワード。
   * **データセンター**：Adobe Analytics アカウントのデータセンター。

1. 「**Analytics に接続**」をクリックします。正常に接続されたことを通知するメッセージと共にダイアログが表示されます。「**OK**」をクリックします。

## クラウドサービスのフレームワークの作成 {#creating-cloud-service-framework}

Adobe Analytics フレームワークは、Adobe Analytics 変数と AEM 変数の間の一連のマッピングです。フレームワークを使用して、フォームから Adobe Analytics レポートにデータを入力する方法を設定します。フレームワークは Adobe Analytics 設定と関連付けられています。設定ごとに複数のフレームワークを作成できます。

1. AEM クラウドサービスコンソールで、Adobe Analytics の下にある「**設定を表示**」をクリックします。
1. Analytics 設定の横にある **[+]** リンクをクリックします。

   ![Adobe Analytics 設定](assets/adobe-analytics-cloud-services.png)

   Adobe Analytics 設定

1. フレームワークの&#x200B;**タイトル**&#x200B;と&#x200B;**名前**&#x200B;を入力し、**Adobe Analytics** フレームワークを選択して「**作成**」をクリックします。フレームワークが編集用に開きます。
1. 横にあるポッドの「レポートスイート」セクションで、「**項目を追加**」をクリックし、ドロップダウンリストを使用してフレームワークとやり取りを行うレポートスイート ID（例えば、JJEsquire）を選択します。
1. レポートスイート ID の横で、レポートスイートに情報を送信するサーバーインスタンスを選択します。

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. サイドキックにある&#x200B;**もう一方の**&#x200B;カテゴリからフレームワーク上に **Form Analytics コンポーネント**&#x200B;をドラッグします。
1. コンポーネントで定義された変数を使用して Analytics 変数をマッピングするには、AEM Content Finder からトラッキングコンポーネントのフィールド上に変数をドラッグします。

   ![Adobe Analytics の変数を使用して AEM の変数をマップする](assets/analytics_new.png)

1. サイドキックの&#x200B;**ページタブ**&#x200B;で「**フレームワークをアクティベート**」をクリックし、フレームワークをアクティベートします。

## AEM Forms Analytics Configuration サービスの設定 {#configuring-aem-forms-analytics-configuration-service}

1. オーサーインスタンスで、`https://<server>:<port>;/system/console/configMgr` でAEM Web Console Configuration Manager を開きます。
1. AEM Forms Analytics Configuration を検索し、開きます。

   ![AEM Forms Analytics Configuration サービス](assets/analytics_configuration.png)

   AEM Forms Analytics Configuration サービス

1. 次のフィールドに適切な値を指定し、「**保存**」をクリックします。

   * **SiteCatalyst フレームワーク**：「追跡用にフレームワークを設定」セクションで定義したフレームワークまたは設定を選択します。
   * **フィールド時間追跡ベースライン**：フィールド訪問を追跡する必要のある時間を秒単位で指定します。デフォルト値は 0 です。0（ゼロ）よりも大きな値を指定すると、2 つの独立した追跡イベントが Adobe Analytics サーバーに送信されます。最初のイベントは、完了フィールドの追跡を停止するように Analytics サーバーに指示を出します。指定された時間が経過すると、2 番目のイベントが送信されます。2 つ目のイベントは、訪問されたフィールドのトラッキングを開始するように Analytics サーバーに指示します。2 つの異なるイベントを使用すると、フィールドでの滞在時間を正確に測定できます。値として 0（ゼロ）を指定すると、1 つの追跡イベントが Adobe Analytics サーバーに送信されます。

   * **分析レポート同期 cron 形式**：Adobe Analytics からレポートを取得するための cron 式を指定します。デフォルト値は 0 0 2 ? &#42; &#42; です。

   * **レポート取得タイムアウト：** Analytics レポートの応答でサーバーを待機する時間を秒単位で指定します。デフォルト値は 120 秒です。

   >[!NOTE]
   >
   >レポート取得操作がタイムアウトになるまでの時間は、最大で、指定されている秒数に 10 秒を加算した時間になります。

1. パブリッシュインスタンスで手順 1 から 3 を繰り返し、Analytics を設定します。

これで、フォームの分析を有効にして、分析レポートを生成できます。

## フォームまたはドキュメント用に Analytics を有効化する {#enabling-analytics-for-a-form-or-document}

1. `https://[hostname]:'port'` で AEM ポータルにログインします。
1. **フォーム／フォームとドキュメント**&#x200B;をクリックして、フォームまたはドキュメントを選択し、「**Analytics を有効にする**」をクリックします。分析が有効になります。

   ![フォームまたはドキュメント用に Analytics を有効化する](assets/enable-analytics-1.png)

   フォーム用に Analytics を有効化する

   **A.** 「Analytics を有効にする」ボタン **B.** 選択したフォーム

   フォーム分析レポートの表示について詳しくは、[AEM Forms 分析レポートの表示と理解](../../forms/using/view-understand-aem-forms-analytics-reports.md)を参照してください。
