---
title: AEM Forms Workspace の概要
description: LiveCycle AEM Forms Workspace を使用して、ビジネス自動化プロセスを管理する方法の概要です。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
exl-id: b38cd444-80f2-4747-9a99-68f69bd87e34
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 100%

---

# AEM Forms Workspace の概要 {#getting-started-with-aem-forms-workspace}

AEM Forms Workspace では、以下のタスクを実行できます。

* ビジネスプロセスを開始する
* 個人の TODO リストまたはアクセス可能な他の TODO リストに割り当てられているタスクの表示と操作
* 開始または参加したプロセスに含まれるタスクを追跡する

## AEM Forms Workspace 内の移動 {#navigating-html-workspace}

表示される AEM Forms Workspace ユーザーインターフェイスの項目は、作業中のプロセスおよびタスクに応じて異なります。「要約」、「フォーム」、「詳細」、「履歴」、「添付ファイル」または「メモ」の各タブ、およびこのヘルプで説明するボタンはすべて、表示される場合とされない場合があります。

AEM Forms Workspace の主要なユーザーインターフェイスは、以下のいずれかの方法を使用して操作できます。

* 「開始プロセス」「TODO リスト」「環境設定」「追跡」「ヘルプ」およびログアウトオプションにアクセスするには、上部ナビゲーションバーのアイテムをクリックします。
* 「開始プロセス」「TODO」または「追跡」タブをクリックして、3 つの主要な作業領域にアクセスします。
* 「開始プロセス」「TODO」および「追跡」タブで、左側パネルのリスト内にある項目をクリックすると、お気に入り、プロセスカテゴリ、検索テンプレート、ドラフト、割り当てられているタスクにアクセスできます。リストにある追加のアイテムを表示するには、スクロールバーを使用します。
* すべてのアクションボタン（「承認」「拒否」「転送」「問い合わせ」「ロック」「共有」）は、ドキュメントと所有者の両方に表示されます。
* ページ下部のナビゲーションバーにある「すべてのオプション」アイコンをクリックすると、タスクを別のユーザーに転送したり、タスクを別のユーザーと共有することができます。また、タスクについて別のユーザーに問い合わせたり、タスクをロックしたりすることができます。
* 「履歴」タブでは、タスクを選択すると、そのタスクの「添付ファイル」タブと「割り当て」タブが表示されます。
* マウスを使用せずに AEM Forms Workspace 内を移動するには、Tab キー、矢印キーおよびスペースバーを使用します。

## AEM Forms Workspace をスクリーンリーダーで使用する {#using-html-workspace-with-screen-readers}

AEM Forms Workspace は web ベースの HTML アプリケーションであり、スクリーンリーダーと互換性があります。AEM Forms Workspace のインターフェイス内で移動するには、キーボードを使用できます。

AEM Forms Workspace をスクリーンリーダーで使用する場合は、以下の点に注意してください。

* AEM Forms Workspace は、標準的なスクリーンリーダーツールに適合する標準的な HTML アプリケーションです。スクリーンリーダーツールを実行するのに特別なスクリプトは必要ありません。
* AEM Forms Workspace 内のすべての移動は「アンカー」タグを経由しますが、タブから容易にアクセスすることができます。
* フォームの読み込みには数秒かかる場合があります。スクリーンリーダーでは、フォームが読み込み中であること、および待機の必要があることは音声で通知されません。

## キーボードを使用した AEM Forms Workspace 内の移動 {#navigating-html-workspace-using-a-keyboard}

キーボードを使用して AEM Forms Workspace 内を移動する場合、移動はアクセシビリティ規則に準拠して行われます。特定の状況下では、タブ移動の順序は通常の順序とは異なります。インターフェイス内での移動時には、以下のヒントを参考にしてください。

* ブラウザーの上部にあるツールバーの範囲外にタブ移動できない場合は、Ctrl + Tab キーを押して、ブラウザーウィンドウのコンテンツにタブ移動します。
* AEM Forms Workspace のヘルプが別のブラウザーウィンドウで開きます。ヘルプを表示すると、フォーカスは AEM Forms Workspace が含まれているブラウザーウィンドウに戻ります。フォーカスが戻っても、ヘルプメニューはフォーカスされたままになります。
* プロセスを開始したり、タスクを完了するためにフォームを開く場合、フォーカスは既存の要素に残り、フォームには移動しません。タブを使用してフォーカスをフォームに移動し、フォーム内をブラウズします。フォーム内のタブ移動の順序は、フォームの種類やデザインによって異なります。

  PDF フォームでは、フォームの一番下までタブ移動したり、フォームを送信したりすると、カーソルのフォーカスはブラウザーのアドレスバーにジャンプします。「ドラフトとして保存」や「完了」などのフォームのアクションボタンに移動するには、再度（フォーム全体ではなく）メニュー内をタブ移動します。フォームがまだ開いている場合は、ボタンをタブでスキップして、フォームに戻ることもできます。

## 環境設定の管理 {#managing-preferences}

以下のカテゴリに、様々な AEM Forms Workspace 環境設定を指定することができます。

**不在設定を管理：**&#x200B;環境設定を指定し、不在時に他のユーザーにタスクを割り当てる方法を管理します。[不在時の環境設定の指定](todo-lists.md#setting-out-of-office-preferences)を参照してください。

**キューを管理：**&#x200B;他のユーザーと TODO リストを共有する場合や、別のユーザーのリストへのアクセス権限を要求する場合の環境設定を指定します。[グループキューと共有キューのタスクの操作](todo-lists.md#working-with-tasks-from-group-and-shared-queues)を参照してください。

**UI 設定：** AEM Forms Workspace とのやり取りの方法について環境設定を指定します。[ユーザーインターフェイスの環境設定の指定](#set-user-interface-preferences)を参照してください。

### ユーザーインターフェイスの環境設定の指定 {#set-user-interface-preferences}

環境設定／UI 設定タブでユーザーインターフェイスの環境設定を指定します。次の環境設定を使用できます。

* **開始場所：** AEM Forms Workspace にログインしたときに表示されるページを指定します。利用可能なオプションは、「開始プロセス」、「TODO」、「トラッキング」、および「お気に入り」の 4 つです。
* **ログアウトプロンプト：**「ログアウト」をクリックした後に、ログアウトすることを確認するプロンプトを表示するかどうかを指定します。
* **日付の形式：** AEM Forms Workspace 全体で使用する日付の表示形式を指定します。
* **時刻の形式：** AEM Forms Workspace 全体で使用する時間の表示形式を指定します。
* **メールでタスクイベントを通知：**&#x200B;個人の TODO リストまたは所属するグループの TODO リスト内のタスクの割り当てやリマインダー、デッドラインなど、タスクイベントのメール通知を受信するかどうかを指定します。
* **メールの添付形式：**&#x200B;フォームのコピーをメールの通知メッセージに添付するかどうかを指定します。添付ファイルは、PDF 形式および XDP 形式のフォームについてのみサポートされています。
* **ドラフトを定期的に保存：**&#x200B;フォームのドラフトを定期的に自動保存するかどうかを指定します。ドラフトを定期的に保存するには、このオプションを有効にし、自動保存期間を 1 分から 30 分の範囲で設定します。自動保存が有効のときに、ユーザーがドラフトで作業をしていると、指定期間（分）が経過するごとにドラフトは定期的に保存されます。ドラフトが自動保存されるのは、ドラフトが最後に保存または自動保存されてから変更が行われた場合のみです。ドラフトを保存すると、アラートメッセージが画面に表示されます。
