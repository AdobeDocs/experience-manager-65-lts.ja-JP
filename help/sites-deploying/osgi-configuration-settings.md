---
title: OSGi 設定
description: この記事では、プロジェクトの実装に関連する OSGi 設定（バンドルに従ってリストされます）について説明します。このリストはガイドラインの役目を果たすものであり、すべてを網羅しているわけではありません。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: d3356f5f-f80f-4ce0-b4e2-3ee927208ab1
source-git-commit: 408f6aaedd2cc0315f6e66b83f045ca2716db61d
workflow-type: tm+mt
source-wordcount: '3247'
ht-degree: 98%

---

# OSGi 設定{#osgi-configuration-settings}

[OSGi](https://www.osgi.org/) は、AEM の技術スタックにおける基本要素です。AEM の複合バンドルおよびそれらの設定を制御するために使用します。

OSGi は「*標準化されたプリミティブを提供し、小さく再利用が可能で連携機能に優れたコンポーネントを組み合わせてアプリケーションを構築することを可能にします。これらのコンポーネントからアプリケーションを作成し、デプロイすることができます*」。

この機能により、バンドルの管理が容易になり、バンドルを個別に停止、インストールおよび起動できます。相互依存関係は自動的に処理されます。各 OSGi コンポーネント（[OSGi の仕様](https://docs.osgi.org/specification/)を参照）は、各種バンドルの 1 つに含まれています。AEM で作業する場合、このようなバンドルの設定を管理する方法はいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

次の OSGi 設定（バンドルに従ったリスト）は、プロジェクトの実装に関連しています。すべての設定に調整が必要なわけではなく、一部の設定は AEM の動作を説明する目的で言及されています。

>[!CAUTION]
>
>このリストはガイドラインの役目を果たすことを目的としたものであり、すべてを網羅しているわけではありません。すべてのバンドルがリストされているわけではなく、リストされているバンドルに関しても、すべてのパラメーターがリストされているわけではありません。
>
>必要な設定は、プロジェクトによって異なります。
>
>使用する値およびパラメーターについて詳しくは、web コンソールを確認してください。

>[!NOTE]
>
>AEM 内の機能の特定の領域では、さらに多くのバンドルが必要な場合があります。この場合、設定の詳細は、該当する機能の関連ページで確認できます。

**AEM レプリケーションイベントリスナー**&#x200B;設定：

* **実行モード**：レプリケーションイベントがリスナーに配信されます。例えば、オーサーとして定義されている場合、これはレプリケーションを「開始」するシステムです。

* プロジェクトコードがパブリッシュ環境でレプリケーションイベント（リバースレプリケーション）を処理する場合は、実行モード&#x200B;**公開**&#x200B;を追加する必要があります。例えば、Dispatcher を使用してパブリッシュ環境からフラッシュする場合や、他のパブリッシュインスタンスへの標準レプリケーションが発生する場合などです。

**AEM リポジトリ変更リスナー**&#x200B;設定：

* **パス**：配布準備が整ったリポジトリイベントをリッスンする場所

**CRX Sling クライアントリポジトリ**：基になるコンテンツリポジトリへのアクセスを設定します。

* **管理者パスワード**&#x200B;をインストール後に変更して、インスタンスの [セキュリティ](/help/sites-administering/security-checklist.md) を確保してください。
* その他の変更は必要ありません。また、リポジトリへのアクセスに影響を与える可能性があるので、注意が必要です。

**Apache Felix OSGi 管理コンソール**&#x200B;設定：

* **Plugins**：**Apache Felix Web Management Console** でトップレベルのメニュー項目として使用できるメインのナビゲーション項目（コンソールプラグイン）です。それぞれ容量とリソースが必要なので、不要なものは無効にしてください。

>[!CAUTION]
>
>必ず以下を設定してください。
>
>**ユーザー名**&#x200B;と&#x200B;**パスワード**：Apache Felix web 管理コンソールにアクセスするための資格情報です。
>インスタンスの[セキュリティ](/help/sites-administering/security-checklist.md)を確保するには、最初のインストールの後にパスワードを変更する必要があります。

>[!NOTE]
>
>この設定は起動時に必要なので、リポジトリが使用可能になる前に、Felix コンソールを使用して設定する必要があります。

**Apache Sling Customizable Request Data Logger** 設定：

* **ロガー名**&#x200B;と&#x200B;**ログ形式**：リクエストおよびアクセスのログの場所と形式を設定します（デフォルト：`request.log`）。このログファイルは、パフォーマンスを分析する際や、web チェーンに関連する機能をデバッグする際には必須です。これは [Apache Sling Request Logger](#apacheslingrequestlogger) とペアで使用されます。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)および [Sling のログ](https://sling.apache.org/documentation/development/logging.html)を参照してください。

**Apache Sling Thread Pool** 設定：

* **Min Pool Size** および **Max Pool Size**：イベントスレッドを保持するために使用するプールのサイズ。

* **Queue Size**：プールを使い果たした場合のスレッドキューの最大サイズ。キューを無制限に設定するため、推奨値は `-1` です。制限を設定すると、その制限を超えた場合に損失が発生する可能性があります。

* これらの設定を変更すると、イベント数が非常に多いシナリオ（AEM DAM またはワークフローの使用量が多い場合など）でパフォーマンスが向上する可能性があります。
* テストを実施して、状況に応じた値を確立する必要があります。
* これらの設定はインスタンスのパフォーマンスに影響を及ぼす可能性があるので、変更の際は十分な理由と検討が必要です。

**Apache Sling GET Servlet**：レンダリングの一部の要素を設定します。

* **Auto Index**：閲覧のためのディレクトリのレンダリングを有効または無効にします。
* デフォルトのレンディション（**HTML**、**プレーンテキスト**、**JSON**、**XML** など）を&#x200B;**有効**（または無効）にします。
JSON を無効にしないでください。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Apache Sling Java Script Handler**：.java ファイルのコンパイルを、スクリプト（サーブレット）として設定します。

特定の設定がパフォーマンスに影響を与える場合があります。特に実稼動インスタンスの場合は、可能な限りこれらの設定を無効にします。

* **Source VM** と **Target VM** で、ランタイム JVM として使用する JDK バージョンを定義します。

* 実稼動インスタンスの場合：

   * 「**デバッグ情報の生成**」を無効化

**Apache Sling JCR Installer**：多くの場合、これらのパラメーターの設定は必要ありませんが、設定を理解しておくと開発時やデバッグ時に役立ちます。例えば、インストールフォルダーは、チェックインやチェックアウト、パッケージの作成に役立つ場合があります。

* **Installation folders name regexp** および **Max hierarchy depth of install folders**：インストールするリソースを検索するリポジトリフォルダーとその階層の深さを指定します。ワイルドカード（例：.&#42;/install）を使用すると、該当する一致項目（`/libs/sling/install` や `/libs/cq/core/install` など）をすべて検索できます。

* **Search Path**：インストールするリソースを jcrinstall が検索するパスのリストです。そのパスの重み付け係数を示す数値も表示されます。

**Apache Sling Queue Configuration** ジョブのスケジュール設定を管理するパラメーターを設定します。

* **再試行間隔**、**再試行の最大回数**、**並列ジョブの最大数** など。

* これらの設定を変更すると、多数のジョブが存在するシナリオのパフォーマンスが向上します。例えば、AEM DAM とワークフローの使用頻度が高い場合などです。
* テストを実施して、状況に応じた値を確立する必要があります。
* これらの設定は理由なく変更しないでください。十分に検討してから変更してください。

**Apache Sling JSP Script Handler**：JSP スクリプトハンドラーのパフォーマンス関連の設定を行います。パフォーマンスを向上させるには、可能な限り無効にする必要があります。

特に、実稼動インスタンスの場合は、次の設定を無効にします。

* 「**デバッグ情報の生成**」を無効化
* 「**生成された Java™ の保持**」を無効化
* 「**マッピングされたコンテンツ**」を無効化
* 「**ソースフラグメントの表示**」を無効化

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Apache Sling Logging Configuration** 設定：

* **Log Level** および **Log File**：主要なログ設定（error.log）の場所とログレベルを定義します。`DEBUG`、`INFO`、`WARN`、`ERROR`、`FATAL` のいずれかのレベルに設定できます。

* **ログファイルの数**&#x200B;と&#x200B;**ログファイルのしきい値**&#x200B;を使用して、ログファイルのサイズとバージョンの回転を定義します。

* ログメッセージの形式は、**メッセージパターン**&#x200B;を使用して定義します。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md#global-logging)と [Sling のログ](https://sling.apache.org/documentation/development/logging.html)を参照してください。

**Apache Sling Logging Logger Configuration（ファクトリ設定）** 設定：

* **Log Level**、**Log File** および **Message Format**：ログファイルとメッセージの詳細を定義します。

* **Logger**：カテゴリを定義します（例：com.day.cq のログのみ）。

* **ファクトリ設定**&#x200B;を使用すると、必要とする様々なログレベルやカテゴリに合わせて、任意の数の追加設定を適用できます。
* このような設定は開発時に役立ちます。例えば、特定のサービスの TRACE メッセージを特定のログファイルに記録する場合などに使用できます。
* このような設定は実稼動環境で役立ちます。例えば、特定のサービスに関するメッセージを個別のログファイルに記録すると、監視を容易化することができます。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)と [Sling のログ](https://sling.apache.org/documentation/development/logging.html)を参照してください。

**Apache Sling Logging Writer Configuration（ファクトリ設定）** 設定：

* **Log File**：ログファイルの有無を定義します。
* **Number of Log Files**：バージョンのローテーションを定義します。

* このライターは、**Apache Sling Logging Logger Configuration** 設定で使用できます。

* このような設定は開発時に役立ちます。例えば、特定のサービスの TRACE メッセージを特定のログファイルに記録する場合などに使用できます。
* このような設定は実稼動環境で役立ちます。例えば、特定のサービスに関するメッセージを個別のログファイルに記録すると、監視を容易化することができます。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)と [Sling のログ](https://sling.apache.org/documentation/development/logging.html)を参照してください。

**Apache Sling Main Servlet** 設定：

* **Number of Calls per Request** および **Recursion Depth**：無限再帰および過度のスクリプトの呼び出しからシステムを保護します。

**Apache Sling Commons MIME Type Service** 以下を設定します。

* **MIME タイプ**：プロジェクトに必要なタイプをシステムに追加します。これにより、ファイルに対する `GET` リクエストで適切な content-type ヘッダーを設定し、ファイルタイプとアプリケーションをリンクすることができます。

**Apache Sling リファラーフィルター**：CRX WebDAV と Apache Sling のクロスサイトリクエストフォージェリー（CSRF）に関する既知のセキュリティ問題に対処するには、リファラーフィルターを設定する必要があります。

リファラーフィルターサービスは OSGi のサービスの 1 つであり、次の設定が可能です。

* どの http メソッドをフィルターするか
* 空のリファラーヘッダーを使用できるかどうか
* サーバーホスト以外に許可されるサーバーのリスト

詳しくは、[「セキュリティチェックリスト」のクロスサイトのリクエスト偽造に関する問題](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery)を参照してください。

>[!NOTE]
>
>Apache Sling Referrer Filter はクイックフィックスパッケージのインストールに依存します。

**Apache Sling Request Logger** 設定：

* 要求をログに記録する方法を定義するための様々なパラメーター。
* **Enable Request Log**：有効または無効にします。

* **Enable Access Log**：有効または無効にします。

[Apache Sling Customizable Request Data Logger](#apacheslingcustomizablerequestdatalogger) とペアで使用されます。

詳しくは、[AEM のログ](/help/sites-deploying/configure-logging.md)および [Sling のログ](https://sling.apache.org/documentation/development/logging.html)を参照してください。

**Apache Sling Resource Resolver Factory**：Sling リソースの解決の主要な要素を設定します。

* **Resource Search Path**：プロジェクト固有のパスを追加します（ただし、`/libs` または `/apps` は削除しないでください）。

* **Virtual URLs**：バニティ URL のマッピングを定義します。

* **URL Mappings**：エイリアスを定義します。（例：`/content` から `/` へのマッピング）。

* **Mapping Location**：`/etc/map` で外面化されるマッパー設定です。

* ローカルインストール（例えば、`https://localhost:4502/system/console/jcrresolver`）を使用して、どのリソースリゾルバーがアクティブかを判断します。

[https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution](https://cwiki.apache.org/confluence/display/SLING/Flexible+Resource+Resolution) を参照してください。

>[!CAUTION]
>
>これらのオプションをリポジトリで設定します。
>
>そうしないと、Felix コンソールで行った「**URL Mappings**」に対する変更が、次回の起動時に AEM によって上書きされる可能性があります。

**Apache Sling Servlet／Script Resolver and Error Handler** Sling サーブレットとスクリプトリゾルバーには、次の複数のタスクがあります。

1. `ServletResolver` として使用され、要求を処理するために呼び出す Servlet または Script を選択します。

1. `SlingScriptResolver` として機能します。

1. エラー処理を管理します。そのためには、要求処理のサーブレット／スクリプトの解決に使用するのと同じアルゴリズムを使用してエラー処理のサーブレット／スクリプトを選択する `ErrorHandler` インターフェイスを実装します。

次のような様々なパラメーターを設定できます。

* **Execution Paths**：実行可能なスクリプトを検索するパスを表示します。特定のパスを設定することで、実行可能なスクリプトを制限できます。パスを設定しない場合は、デフォルト値（`/` = ルート）を使用し、すべてのスクリプトの実行が許可されます。
設定したパス値がスラッシュで終わる場合は、サブツリー全体が検索対象となります。末尾にスラッシュを指定しないと、完全一致の場合にのみスクリプトが実行されます。

* **Default Extensions**：デフォルトの動作が使用される拡張子のリストです。リソースタイプの最後のパスセグメントをスクリプト名として使用できます。

**Apache HTTP Components Proxy Configuration** - Apache HTTP クライアントを使用するすべてのコード用のプロキシ設定です。HTTP の作成時に使用されます（レプリケーション時など）。

設定を作成する際には、工場出荷時の設定に変更を加えないでください。代わりに、設定マネージャー（**https://localhost:4502/system/console/configMgr/**）を使用して、このコンポーネントの工場出荷時の設定を作成してください。このプロキシ設定は、**org.apache.http.proxyconfigurator** で利用できます。

**Adobe Granite HTML Library Manager**：クライアントライブラリ（css または js）の処理（例えば、基盤となる構造の表示形式）を制御するために設定します。

* 実稼動インスタンスの場合：

   * 「**縮小**」を有効にして CRLF 文字と空白文字を削除する
   * 「**Gzip**」を有効にして、1 回のリクエストでファイルを gzip で圧縮してアクセスできるようにする。
   * 「**デバッグ**」を無効にする
   * 「**タイミング**」を無効にする

* JS 開発の場合（特に、Firebug を使用するか、デバッグを行う場合）：

   * 「**デバッグ**」を無効にします。
   * 「**デバッグ**」を有効にして、デバッグ用のファイルを分離し、Firebug で使用します。
   * 「**タイミング**」を有効にします（タイミングに関する設定を行う場合）。
   * **デバッグ**&#x200B;コンソールを有効にして、JS コンソールのログメッセージを確認します。

>[!CAUTION]
>
>**縮小**&#x200B;または **Gzip** の設定を変更する場合は、clientlibs キャッシュの内容を削除します。詳しくは、[ナレッジベースの記事](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-16543.html?lang=ja)を参照してください。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Adobe Granite HTTP Header Authentication Handler** HTTP リクエストの基本的な認証方法に関するシステム全体の設定です。

[閉じられたユーザーグループ](/help/sites-administering/cug.md)を使用すると、（特に）以下を設定できます。

* **HTTP レルム**
* **デフォルトのログインページ**

**Day CQ Link Checker Service**：必要に応じて、次の項目を設定します。

* **Scheduler Period**：外部リンクを自動的にチェックする間隔を定義します。

* **Bad Link Tolerance Interval**：失敗した外部リンクが無効と見なされるまでの期間を指定します。
* **Link Check Override Patterns**：リンクチェックから除外するパスを定義します。

**Day CQ Link Checker Task**：単一のリンクチェッカータスク（外部リンクを確認するタスク）の設定を指定します。

* **Good Link Test Interval** および **Bad Link Test Interval で定義されている間隔をチェックします。** 

* リンクをチェックする際に外部アクセスのために必要な、インターネットアクセスおよび NTLM 用のプロキシに関連する様々なパラメーターを設定します。

**Day CQ Mail Service**：メールサーバーのホスト名とアクセスの詳細を設定します。「メールサービスの設定」の節を参照してください。

**Day CQ MCM Newsletter**：ニュースレターで使用する様々な設定を指定します。

**Day CQ Root Mapping**：以下の項目を設定します。

* **ターゲットパス**：「`/`」に対するリクエストのリダイレクト先を定義します。

AEM では次の 2 つの UI を使用できます。

* タッチ操作対応 UI が標準の UI です。
* 非推奨のクラシック UI も引き続き問題なく機能します

AEM ルートマッピングを使用すると、希望する UI を、インスタンスのデフォルトとして設定できます。

* タッチ操作対応 UI をデフォルトの UI にするには、**ターゲットパス**&#x200B;を次のように指定します。

  ```shell
     /projects.html
  ```

* クラシック UI をデフォルトの UI とするには、**ターゲットパス**&#x200B;を次のように指定します。

  ```shell
     /welcome.html
  ```

>[!NOTE]
>
>標準インストールでは、タッチ操作向け UI がデフォルトの UI です。

**Adobe Granite SSO Authentication Handler**：シングルサインオン（SSO）の詳細を設定します。この詳細情報は、企業の作成者の設定や、LDAP との連動で必要となることが多くあります。

様々な設定プロパティがあります。

* **パス**
この認証ハンドラーをアクティブにする対象のパス。このパラメーターを空のままにすると、認証ハンドラーは無効になります。例えば、/ というパスを指定すると、認証ハンドラーはリポジトリ全体に対して使用されます。

* **Service Ranking**
OSGi フレームワークサービスランキングの値は、このサービスの呼び出しに使用する順序を示すために使用されます。これは `int` 値で、値が大きいほど優先度が高くなります。
デフォルト値は `0` です。

* **Header Names**
ユーザー ID を含んでいる可能性のあるヘッダーの名前です。

* **Cookie Names**
ユーザー ID を含んでいる可能性のある Cookie の名前です。

* **Parameter Names**
ユーザー ID を指定する可能性のあるリクエストパラメーターの名前です。

* **User Map**
選択したユーザーについて、HTTP リクエストから抽出されたユーザー名を、認証情報オブジェクト内の別のユーザー名に置き換えることができます。マッピングはここで定義します。ユーザー名 `admin` がマップの両側に表示される場合、マッピングは無視されます。「=」文字を使用する場合は、先頭に「\」を付けてエスケープする必要があります。

* **Format**：ユーザー ID を指定する際の形式を示します。次のいずれかを使用します。

   * `Basic`：ユーザー ID が HTTP Basic 認証形式でエンコードされている場合
   * `AsIs`：ユーザー ID がプレーンテキストで指定されている場合や、正規表現が適用されている値をそのまま、または正規表現として使用する必要がある場合

**Day CQ WCM Debug Filter**：ページへのアクセス時に ?debug=layout などのサフィックスを使用できるので、開発時に便利です。例えば、https://localhost:4502/cf#/content/geometrixx/en/support.html?debug=layout は開発者が関心を持つ可能性のあるレイアウト情報を提供します。

* パフォーマンスとセキュリティを確保するために、実稼動インスタンスでは無効にします。

**Day CQ WCM Filter**：以下の項目を設定します。

* **WCM Mode**：デフォルトモードを定義します。
* オーサーインスタンスでは、このモードを `edit`、`disable,preview` または `analytics` に設定できます。
その他のモードは、サイドキックからアクセスできます。またはサフィックス `?wcmmode=disabled` を使用して実稼動環境をエミュレートできます。

* パブリッシュインスタンスでは、`disabled` に設定して、その他のモードにアクセスできないようにする必要があります。

>[!NOTE]
>
>AEM を[実稼動準備完了モード](/help/sites-administering/production-ready.md)で実行している場合は、この設定は自動的に実稼動インスタンス用に設定されます。

**Day CQ WCM Link Checker** 以下の項目を設定します。

* **書き換え設定のリスト**：コンテンツベースのリンクチェックツール設定の場所のリストを指定します。設定は実行モードに基づくことができます。これはオーサー環境とパブリッシュ環境を区別するために重要です。それぞれの環境でリンクチェッカーの設定が異なる場合があるからです。

**Day CQ WCM Page Manager Factory**：以下の項目を設定します。

* **ページサブツリーのアクティベーションチェック**：（レプリケーション権限を持たない）ユーザーが（ページがアクティベートされていない場合でも）ページを削除または移動できるかをチェックします。

**Day CQ WCM Page Processor**：以下の項目を設定します。

* **パス**：システムが `jcr:Event` をトリガーする前にページの変更をリッスンする場所のリストです。

**Adobe Page Impressions Tracker**：オーサーインスタンスの場合は、次のように設定します。

* **sling.auth.requirements**：このプロパティの値を `-/libs/wcm/stats/tracker` に設定します

>[!CAUTION]
>
>この設定では、トラッキングサービスへの匿名リクエストが許可されます。

>[!NOTE]
>
>詳しくは、[ページインプレッション](/help/sites-deploying/configuring.md#enabling-page-impressions)を参照してください。

**Day CQ WCM Page Statistics**：パブリッシュインスタンスの場合は、次のように設定します。

* **URL to send data**：ページ統計の追跡に使用する URL を設定します（トラッカーリクエストが Dispatcher を経由する場合は必須）。例えば、デフォルトは `https://localhost:4502/libs/wcm/stats/tracker` です。

* **Tracking script enabled**：ページ上の追跡スクリプトのインクルードを有効化（`true`）または無効化（`false`）します。デフォルト値は `false` です。

>[!NOTE]
>
>詳しくは、[ページインプレッション](/help/sites-deploying/configuring.md#enabling-page-impressions)を参照してください。

**Day CQ WCM Version Manager**：システム内でバージョンを管理するかどうか、および管理方法を制御します。

* **Create Version on Activation**：標準インストールで有効になります。
* **Enable Purging**

* **Purge Paths**：検索アクションで検索するパス。
* **Implicit Versioning Paths**：暗黙のバージョン管理がアクティブなパス。

* **Max Version Age**：バージョンの最長有効期間（日数）。

* **Max Number Versions**：保存するバージョンの最大数。

詳しくは、[バージョンのパージ](/help/sites-deploying/version-purging.md)を参照してください。

**Day CQ Workflow Email Notification Service**：ワークフローから送信されるメール通知を設定します。

**Adobe AEM Rewriter HTML パーサーファクトリ**

CQ リライターの HTML パーサーを制御します。

* **追加のタグをプロセス** - パーサーで処理する HTML タグを追加または削除できます。デフォルトで処理されるタグは、A、IMG、AREA、FORM、BASE、LINK、SCRIPT、BODY、HEAD です。
* **キャメルケースを保持** - デフォルトでは、HTML パーサーによってキャメルケース（例：`eBay`）の属性が小文字（例：`ebay`）に変換されます。キャメルケースの属性を保持するには、これをオフにします。この設定は、Angular 2 などのフロントエンドフレームワークを使用する際に役立ちます。

**Day Commons JDBC Connections Pool**：コンテンツのソースとして使用される外部データベースへのアクセスを設定します。

ファクトリ設定なので、複数のインスタンスを設定できます。

**CDN Rewriter**：AEM と CDN の間の通信では、アセットやバイナリが安全な方法でエンドユーザーに配信されるようにする必要があります。このプロセスには、次の 2 つのタスクが含まれます。

* 最初（またはキャッシュ内のリソースが期限切れになった後）に、CDN を介して AEM からリソースにアクセスします。
* CDN にキャッシュされたリソースに安全にアクセスします。CDN にリソースがキャッシュされた後は、リクエストは AEM に送信されず、そのリソースにアクセスできるすべてのユーザーの処理は CDN で行われます。

AEM は、内部アセットの URL を外部の CDN URL に書き直すリライターを提供しています。これにより、JWS 署名および有効期限を含む、CDN に渡すリンクが書き直され、アセットに安全にアクセスできるようになります。この機能は、オーサーインスタンスで使用されます。

全体的なフローは次のとおりです。

1. ユーザーが AEM で認証を行い、アセットを含むページをリクエストします。
1. リクエストされたページには、`/content/dam/geometrixx-media/articles/paladin_trailer.jpg/jcr:content/renditions/cq5dam.thumbnail.319.319.png` に類似したアセットが含まれます
1. リライターは、リンクを、JWS 署名を含む CDN URL に変換します。
   `CDN_domain/content/dam/geometrixx-media/articles/paladin_trailer.jpg/_jcr_content/renditions/cq5dam.thumbnail.319.319.png?cdn_sign=JWS_SIGNATURE`

1. ユーザーのブラウザーによって、CDN サーバーにアセット要求が転送されます。
1. 要求が `cdn_sign` パラメーターと共に AEM に転送されるように、CDN を設定する必要があります。
1. 認証ハンドラーによって `cdn_sign` パラメーターが検証され、CDN にアセットが返された後、アセットがユーザーに配信されます。

次の図に、ユーザーのブラウザー、CDN および AEM の間のフローを示します。

![chlimage_1-8](assets/chlimage_1-8.png)

>[!NOTE]
>
>この機能は、AEM オーサーインスタンスでのみ使用できます。

**CDNConfigServiceImpl**：CDN 設定を指定します。

CDN の書き直し機能を使用できるようにするには、com.adobe.cq.cdn.rewriter.impl.CDNConfigServiceImpl の設定に **CDN 配布ドメイン名**&#x200B;を入力します。

また、このサービスには、CDN 書き直しの有効化／無効化、CDN 書き直しが実行されるパスのプレフィックス、TTL 値、プロトコル（HTTP または HTTPS）など、その他の設定オプションも含まれます。

**CDNRewriter**：内部画像の URL を CDN URL に書き直すリライターです。

com.adobe.cq.cdn.rewriter.impl.CDNRewriter の&#x200B;**タグ属性**&#x200B;値は、選択した画像のリンクのみが書き直されるように定義できます。
