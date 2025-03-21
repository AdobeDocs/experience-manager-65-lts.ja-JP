---
title: サーバー設定の指定
description: サーバー設定ページから、メール、タスク通知および管理者通知の設定にアクセスできます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: da8031f2-26ab-41e2-bf54-7032727ca192
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '2643'
ht-degree: 100%

---

# サーバー設定の指定 {#configuring-server-settings}

サーバー設定ページから、Forms Workflow の様々な設定にアクセスできます。

* **メールの設定**：メールの送信に加えて、それらのメールに使用されるメールサーバーを設定することができます（[メールの設定](configuring-server-settings.md#configuring-email-settings)を参照）。
* **タスク通知の設定**：エンドユーザーおよびグループに、タスクに関するメール通知で送信されるメッセージを有効化、無効化または変更することができます。（[ユーザーおよびグループへの通知の設定](configuring-server-settings.md#configuring-notifications-for-users-and-groups)を参照してください）。
* **管理者通知の設定**：管理タスクについてのメール通知で送信されるメッセージを有効化、無効化または変更することができます。（[管理者への通知の設定](configuring-server-settings.md#configuring-notifications-for-administrators)を参照）。

## メールの設定 {#configuring-email-settings}

Forms サーバーのメールアカウントを指定できます。このメールアカウントを通じて、AEM Forms ユーザーおよび管理者にメールメッセージの送信が行われます。これらのメールは、完了する必要があるタスクをユーザーに通知したり、タスクが期限切れになったことをユーザーに通知したり、発生したプロセスエラーを管理者に通知したりする際に使用されます。

AEM Forms とユーザーの間でメールメッセージを送信できるようにするには、メールの設定ページで送信メールの設定を行います。送信メールは、SMTP サーバーを使用する必要があります。

AEM Forms でユーザーからのメールメッセージを受信して処理するには、Complete Task サービスのメールエンドポイントを作成します（[Complete Task サービス用のメールエンドポイントの作成](/help/forms/using/admin-help/configuring-email-endpoints.md#create-an-email-endpoint-for-the-complete-task-service)を参照）。

設計および実装するプロセスでメールが不要な場合は、メールの設定ページのオプションを設定する必要はありません。

### 送信メールの設定 {#configure-outgoing-email-settings}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

1. 管理コンソールで、サービス／Forms Workflow／サーバー設定／メールの設定をクリックします。
1. 「送信メッセージを有効化」を選択します。
1. 「SMTP サーバー」ボックスに、メールサーバーの名前または IP アドレスを入力します。Forms Workflow からのすべてのメール通知メッセージが、このメールサーバーから送信されます。
1. 「ユーザー名」ボックスと「パスワード」ボックスに、SMTP サーバーが認証を要求する場合に使用するログイン名とパスワードを入力します。匿名ログインを許可する場合は、これらを空白のままにします。
1. 「メールアドレス」ボックスに、Forms Workflow が送信するメールの返信者アドレスとして使用するメールアドレスを入力します。

   >[!NOTE]
   >
   >Micfosoft Exchange Server を使用していて、メールアドレスが無効なアドレスの場合、Micfosoft Exchange Server はメールを配信リストに送信できません。この問題を解決するには、Microsoft Exchange Server 上の配信リスト毎に「**外部コミュニケーションを有効化**」オプションを選択します。

1. 「保存」をクリックします。

>[!NOTE]
>
>間違った情報を入力した場合は、「キャンセル」をクリックして、前に表示したページに戻ります。

### AEM Forms Workspace を使用するためのメールテンプレートの設定 {#configuring-email-templates-to-use-html-workspace}

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

デフォルトでは、AEM Forms によって送信されるメールは Flex Workspace（JEE 上の AEM Forms では廃止されています）へのリンクを含みます。AEM Forms によって送信されるメールが AEM Forms Workspace へのリンクを含むように設定できます。Flex Workspace（JEE 上の AEM forms では廃止されています）を上回る AEM Forms Workspace のメリットについて詳しくは、[こちら](/help/forms/using/features-html-workspace-available-flex.md)の記事を参照してください。

1. 管理コンソールで、ホーム／サービス／Forms Workflow／サーバー設定／タスク通知をクリックします。
1. タスクの割り当てテンプレートを開きます。
1. タスク通知のテンプレートを次のように設定します。`https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@`

   ```java
   https://@@notification-host@@:8080/lc/libs/ws/index.html?taskId=@@taskid@@
   ```

## ユーザーおよびグループへの通知の設定 {#configuring-notifications-for-users-and-groups}

タスク通知ページでは、Forms Workflow がユーザーとグループに送信するメール通知を生成する際に使用するテンプレートを設定できます。Forms Workflow 変数を使用して、通知をカスタマイズおよびフォーマットできます。

ユーザーとグループには、次の種類の通知を設定できます。

* リマインダー
* タスクの割り当て
* デッドライン

グループへのメール通知を生成するには、User Management でそのグループのメールアドレスを指定します。<!--Fix broken link See Setting up and organizing users -->Forms Workflow によってメール通知がグループに送信されると、そのグループ内の、メールアドレスが指定されている各メンバーがそのメール通知を受け取ります。メール通知を受信したグループのメンバーがタスクを要求する場合、そのメール通知に記載されている要求リンクをクリックして、Workspace のタスクの詳細ページを開く必要があります。メンバーは、このページから、作業項目を要求または要求して開くことができます。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

### ユーザーまたはグループへのリマインダーの設定 {#configure-reminders-for-users-or-groups}

タスク完了の期限が近づいてきたら、割り当てられているユーザーまたはグループにリマインダー通知を送信することができます。リマインダー通知の正確な送信時刻を決定するルールは、プロセス開発者が決定します。

1. 管理コンソールで、サービス／Forms Workflow／サーバー設定／タスク通知をクリックします。
1. 通知タイプで、「リマインダー」（ユーザーの場合）または「グループ - リマインダー」（グループの場合）をクリックします。
1. 「リマインダーを有効化」または「グループ - リマインダーを有効化」を選択します。
1. （ユーザー通知のみ）リマインダーのメールメッセージに、フォームとそのデータの添付ファイルを含めるには、「フォームデータを含める」を選択します。
1. 「件名」ボックスに、メールメッセージの件名行のテキストを入力します。このフィールドには、デフォルトのテキストが事前に入力されています。このフィールドのカスタマイズについて詳しくは、[通知内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)を参照してください。
1. 「通知テンプレート」ボックスに、メールメッセージの本文のテキストを入力します。このフィールドには、デフォルトのテキストが事前に入力されています。このフィールドのカスタマイズについて詳しくは、[通知内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)を参照してください。
1. メッセージの形式リストで、メールメッセージの送信形式（「HTML」または「テキスト」）を選択します。デフォルトの形式は HTML です。
1. メールのエンコーディングリストで、メールメッセージに使用するエンコーディング形式を選択します。デフォルトは UTF-8 です。日本以外のほとんどのユーザーはこれを使用します。日本のユーザーは、ISO2022-JP も選択できます。
1. 「保存」をクリックします。

### ユーザーまたはグループへのタスクの割り当て通知の設定 {#configure-task-assignment-notifications-for-users-or-groups}

ユーザーまたはグループにタスクが割り当てられたときに、それぞれにタスクの割り当て通知を送信することができます。

1. 管理コンソールで、サービス／Forms Workflow／サーバー設定／タスク通知をクリックします。
1. 通知タイプで、ユーザーにタスクの割り当て通知を送信する場合は「タスクの割り当て」、グループに送信する場合は「グループ - タスクの割り当て」をクリックします。
1. 「ユーザーのタスク割り当てを有効にする」または「グループのタスク割り当てを有効にする」を選択します。
1. （ユーザー通知のみ）タスクの割り当てのメールメッセージに、フォームとそのデータの添付ファイルを含めるには、「フォームデータを含める」を選択します。
1. 「件名」ボックスに、メールメッセージの件名行のテキストを入力します。このフィールドには、デフォルトのテキストが事前に入力されています。このフィールドのカスタマイズについて詳しくは、[通知内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)を参照してください。
1. 「通知テンプレート」ボックスに、メールメッセージの本文のテキストを入力します。このフィールドには、デフォルトのテキストが事前に入力されています。このフィールドのカスタマイズについて詳しくは、[通知内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)を参照してください。
1. メッセージの形式リストで、メールメッセージの送信形式（「HTML」または「テキスト」）を選択します。デフォルトの形式は HTML です。
1. メールのエンコーディングリストで、メールメッセージに使用するエンコーディング形式を選択します。デフォルトは UTF-8 です。日本以外のほとんどのユーザーはこれを使用します。日本のユーザーは、ISO2022-JP も選択できます。
1. 「保存」をクリックします。

### ユーザーまたはグループへのデッドライン通知の設定 {#configure-deadline-notifications-for-users-or-groups}

割り当てられたタスクの実行期限を過ぎた場合、ユーザーおよびグループにデッドライン通知を送信することができます。ユーザーは割り当てられたタスクを実行できないので、デッドライン通知は情報を提供するためのものに過ぎません。

1. 管理コンソールで、サービス／Forms Workflow／サーバー設定／タスク通知をクリックします。
1. 通知タイプで、「デッドライン」（ユーザーの場合）または「グループ - デッドライン」（グループの場合）をクリックします。
1. 「デッドラインを有効化」または「グループ - デッドラインを有効化」を選択します。
1. 「件名」ボックスに、メールメッセージの件名行のテキストを入力します。このフィールドには、デフォルトのテキストが事前に入力されています。このフィールドのカスタマイズについて詳しくは、[通知内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)を参照してください。
1. 「通知テンプレート」ボックスに、メールメッセージの本文のテキストを入力します。このフィールドには、デフォルトのテキストが事前に入力されています。このフィールドのカスタマイズについて詳しくは、[通知内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)を参照してください。
1. メッセージの形式リストで、メールメッセージの送信形式（「HTML」または「テキスト」）を選択します。デフォルトの形式は HTML です。
1. メールのエンコーディングリストで、メールメッセージに使用するエンコーディング形式を選択します。デフォルトは UTF-8 です。日本以外のほとんどのユーザーはこれを使用します。日本のユーザーは、ISO2022-JP も選択できます。
1. 「保存」をクリックします。

### すべてのメールの DO NOT DELETE タグを非表示 {#hide-the-do-not-delete-tag-for-all-emails}

人間中心のプロセスで送信されたすべてのメールで、DO NOT DELETE 追跡タグを非表示にするようメールを設定できます。

<!-- 
For details, see [How to hide the 'DO-NOT-DELETE' tag with CSS](https://blogs.adobe.com/LiveCycleHelp/2013/09/how-to-hide-the-do-not-delete-tag-with-css.html) 
-->

## 管理者への通知の設定 {#configuring-notifications-for-administrators}

Forms Workflow が、管理者に送信されるメール通知を生成する際に使用するテンプレートを設定できます。

管理者には、次の種類の通知を設定できます。

* 停止したブランチ
* 停止した操作

### 停止したブランチ通知の設定 {#configure-stalled-branch-notifications}

ブランチが停止した場合（意図的またはエラーが原因で停止した場合）、管理者または問題を調査できる別のユーザーにメール通知を送信することができます。

1. 管理コンソールで、サービス／Forms Workflow／サーバー設定／管理者通知をクリックします。
1. 通知タイプで、「停止したブランチ」をクリックします。
1. 「停止したブランチを有効化」を選択します。
1. 「メールアドレス」ボックスに、ブランチが停止したときに通知するユーザーのアドレスを入力します。アドレスは、user@domain.com の形式で入力します。また、各アドレスはコンマで区切ります。通常は、管理者のメールアドレスを入力します。
1. 「件名」ボックスに、メールメッセージの件名行のテキストを入力します。このフィールドには、デフォルトのテキストが事前に入力されています。このフィールドのカスタマイズについて詳しくは、[通知内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)を参照してください。
1. 「通知テンプレート」ボックスに、メールメッセージの本文のテキストを入力します。このフィールドには、デフォルトのテキストが事前に入力されています。このフィールドのカスタマイズについて詳しくは、[通知内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)を参照してください。
1. メッセージの形式リストで、メールメッセージの送信形式（「HTML」または「テキスト」）を選択します。デフォルトの形式は HTML です。
1. メールのエンコーディングリストで、メールメッセージに使用するエンコーディング形式を選択します。デフォルトは UTF-8 です。日本以外のほとんどのユーザーはこれを使用します。日本のユーザーは、ISO2022-JP も選択できます。
1. 「保存」をクリックします。

### 停止した操作通知の設定 {#configure-stalled-operation-notifications}

操作が停止した場合（意図的またはエラーが原因で停止した場合）、管理者または問題を調査できる別のユーザーにメール通知を送信することができます。

1. 管理コンソールで、サービス／Forms Workflow／サーバー設定／管理者通知をクリックします。
1. 通知タイプで、「停止した操作」をクリックします。
1. 「停止した操作を有効化」を選択します。
1. 「メールアドレス」ボックスに、操作が停止したときに通知するユーザーのアドレスを入力します。アドレスは、user@domain.com の形式で入力します。また、各アドレスはコンマで区切ります。通常は、管理者のメールアドレスを入力します。
1. 「件名」ボックスに、メールメッセージの件名行のテキストを入力します。このフィールドには、デフォルトのテキストが事前に入力されています。このフィールドのカスタマイズについて詳しくは、[通知内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)を参照してください。
1. 「通知テンプレート」ボックスに、メールメッセージの本文のテキストを入力します。このフィールドには、デフォルトのテキストが事前に入力されています。このフィールドのカスタマイズについて詳しくは、[通知内容のカスタマイズ](configuring-server-settings.md#customizing-the-content-of-notifications)を参照してください。
1. 「保存」をクリックします。

## 通知内容のカスタマイズ {#customizing-the-content-of-notifications}

タスク通知ページと管理者通知ページには、次に示すような、通知メッセージをカスタマイズするための様々な機能があります。

* リッチテキストエディター
* 変数選択
* URL 生成

### リッチテキストエディター {#rich-text-editor}

通知テンプレート領域はリッチテキストエディターなので、これを使用してメール通知メッセージの HTML を生成することができます。「通知テンプレート」ボックスの下に、フォントと段落の書式設定オプションがあります。フォントタイプ、サイズ、スタイル、カラーのほか、段落の配置と箇条書きについてのオプションがあります。

### URL 生成 {#url-generation}

タスク通知の場合のみ、Forms Workflow には事前定義された 2 つの URL 設定が表示されます。これらの設定を URL 生成リストから「通知テンプレート」ボックスにドラッグしてカスタマイズすることができます。

* OpenTask は、「リマインダー」と「タスクの割り当て」の通知タイプで使用できます。この URL は Workspace 内のタスクへのリンクで、ユーザーはメール通知からタスクに簡単にアクセスできます。OpenTask URL を「通知テンプレート」ボックスにドラッグすると、URL は次の形式で表示されます。

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

* ClaimTask は、「グループ - リマインダー」および「グループ - タスクの割り当て」の通知タイプで使用できます。この URL は Workspace のタスクの詳細ページへのリンクです。このページから、ユーザーは作業項目を要求または要求して開くことができます。ClaimTask URL を「通知テンプレート」ボックスにドラッグすると、URL は次の形式で表示されます。

  `https://@@notification-host@@:<PORT>/workpace/Main.html?taskId=@@taskid@@`

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

ソリューションをクラスター環境にデプロイする場合は、`@@notification-host@@` をクラスターアドレスに置き換えます。

`<`*PORT* `>` はアプリケーションサーバーの HTTP リスナーのポート番号です。サポートされるアプリケーションサーバーのデフォルトの HTTP リスナーポートは、以下のとおりです。

**JBoss：** 8080

**Oracle WebLogic Server：** 7001

**IBM WebSphere：** 9080

これらの URL を正しく機能させるには、`<`*PORT* `>` を環境に適したポート番号に置き換えます。

>[!NOTE]
>
>Forms 以外のカスタム web アプリケーションを使用して、タスクへのアクセスをユーザーに提供する場合は、そのカスタムアプリケーションに適した URL 形式を使用する必要があります。

### 変数選択 {#variable-picker}

変数選択リストには便利な変数があり、「件名」ボックスまたは「通知テンプレート」ボックスにドラッグ＆ドロップできます。「件名」ボックスまたは「通知テンプレート」ボックスに変数をドロップすると、実際の Forms ワークフローの変数名の両端に 2 つの @ 記号が付いたものに変わります（「`@@taskid@@`.@@」など）。

ユーザーまたはグループへのリマインダー、タスクの割り当て、およびデッドラインの場合、「件名」ボックスと「通知テンプレート」ボックスで以下の変数を使用できます。

**description** Workbench 内のプロセスのユーザー手順で定義された説明プロパティの内容。ユーザー手順は、開始ポイント、タスクの割り当て操作、または複数のタスクの割り当て操作です。

**instructions** Workbench 内のプロセスのユーザー手順で定義された、タスクの手順プロパティの内容。

**notification-host** AEM Forms アプリケーションサーバーのホスト名。

**process-name** プロセスの名前。

**operation-name** 手順の名前。

**taskid** 現在のタスクの一意の ID。

**actions** 受信者がクリックできる有効なルート（承認、却下など）の番号付きリストを作成します。

グループリマインダー、グループタスクの割り当て、グループのデッドラインの場合、次の変数も使用できます。

**group-name** 作業項目に割り当てられたグループの名前。

>[!NOTE]
>
>変数に値が設定されていない場合は、何も返されません。

停止したブランチの場合は、次の変数を「件名」ボックスおよび「通知テンプレート」ボックスで使用できます。

**branch-id** 分岐の識別子。

**process-id** プロセスインスタンスの識別子。

**notification-host** AEM Forms アプリケーションサーバーのホスト名。

停止した操作の場合は、次の変数を「件名」ボックスおよび「通知テンプレート」ボックスで使用できます。

**action-id** 操作の識別子。

**branch-id** 分岐の識別子。

**process-id** プロセスインスタンスの識別子。

**notification-host** AEM Forms アプリケーションサーバーのホスト名。

### 「件名」ボックスでの変数の使用 {#using-a-variable-in-the-subject-box}

タスクの割り当て通知の「件名」ボックスに、次のテキストを入力するとします。

`Please complete task @@taskid@@`

タスク 376 が割り当てられると、ユーザーは次の件名のメールを受け取ります。

`Please complete task 376`

### 「通知テンプレート」ボックスでの変数の使用 {#using-variables-in-the-notification-template-box}

停止したブランチの通知の「通知テンプレート」ボックスに、次のテキストを入力するとします。

`Branch @@branch-id@@ has stalled! You have received this notification from @@notification-host@@.`

ブランチ番号が 4868 で、サーバー名が `ServerXYZ` の場合、管理者は次の内容のメールを受け取ります。

`Branch 4868 has stalled! You have received this notification from ServerXYZ.`

## Business Activity Monitoring 接続の設定 {#configuring-business-activity-monitoring-connections}

オプションで提供されるモジュールである Business Activity Monitoring（BAM）では、操作と主要なパフォーマンスインジケーターのリアルタイムでの表示を可能にする、一連の操作ダッシュボードを使用できます。

BAM の設定ページでは、BAM を実行するサーバーへの接続を設定して、プロセス関連のイベントを追跡し、そのサーバーに送信できます。

1. 管理コンソールで、サービス／Forms Workflow／サーバー設定／BAM の設定をクリックします。
1. 「BAM ホスト」ボックスに、BAM を実行するサーバーの名前を入力します。デフォルトは localhost です。
1. 「BAM ポート」ボックスに、BAM を実行するサーバーに接続するときに使用するポートを入力します。デフォルトの BAM ポートは、JBoss で 8080、WebLogic で 7001、WebSphere で 9080 です。
1. 「サーバーホスト」ボックスに、ホスト Forms サーバーの名前または IP アドレスを入力します。デフォルト値は localhost です。
1. 「サーバーポート」ボックスに、Forms サーバーで使用されるポート番号を入力します。
1. 「ユーザー名」ボックスおよび「パスワード」ボックスに、BAM サーバーにアクセスするための適切なユーザー ID とパスワードを入力します。デフォルトのユーザー名は「CognosNowAdmin」、デフォルトのパスワードは「manager」です。
1. 「保存」をクリックします。
