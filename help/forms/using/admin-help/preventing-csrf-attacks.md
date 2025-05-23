---
title: CSRF 攻撃の防止
description: クロスサイトリクエストフォージェリー（CSRF）攻撃を防止し、ユーザーデータを侵害から保護する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 00f52303-66c3-4865-a74b-eda0e6949193
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 100%

---

# CSRF 攻撃の防止 {#preventing-csrf-attacks}

## CSRF 攻撃の仕組み {#how-csrf-attacks-work}

クロスサイトリクエストフォージェリー（CSRF）とは、有効なユーザーのブラウザーが悪質なリクエストの送信（iFrame 経由で）に利用される、web サイトの脆弱性のことです。ブラウザーは Cookie をドメインベースで送信するので、ユーザーがアプリケーションにログインしている場合、ユーザーのデータが侵害される可能性があります。

例えば、ブラウザーで管理コンソールにログインしている場合を想定します。リンクを含むメールメッセージを受信したとします。リンクをクリックすると、ブラウザーで新しいタブが開きます。開いたページには、認証済みの AEM Forms セッションの Cookie を使用して Forms サーバーに悪質なリクエストを行う非表示の iFrame が含まれています。User Management は有効な Cookie を受け取るので、そのリクエストを渡してしまいます。

## CSRF に関する用語 {#csrf-related-terms}

**リファラー：**&#x200B;リクエストの発信元のソースページのアドレス。例えば、site1.com 上の web ページに site2.com へのリンクが含まれています。このリンクをクリックすると、リクエストが site2.com にポストされます。このリクエストは site1.com のページを発信元としているので、このリクエストのリファラーは site1.com です。

**許可リスト登録済み URI：** URI はリクエスト対象の Forms サーバー上のリソースを識別します（例えば /adminui、/contentspace など）。一部のリソースでは、外部のサイトからリクエストがアプリケーションにアクセスすることができます。こうしたリソースは、許可リスト登録済み URI と見なされます。Forms サーバーはリファラーに対する許可リスト登録済み URI のチェックは行いません。

**Null リファラー**：ブラウザーの新しいウィンドウまたはタブを開き、アドレスを入力して Enter キーを押した場合、リファラーは null です。リクエストはまったく新規で、親 web ページから生成されたものではないので、このリクエストのリファラーはありません。Forms サーバーは、以下の場合に null リファラーを受け取ることができます。

* SOAP または REST エンドポイントで Acrobat からリクエストが送信された場合
* AEM Forms の SOAP または REST エンドポイントで HTTP リクエストを行うデスクトップクライアント
* ブラウザーの新しいウィンドウが開き、任意の AEM Forms web アプリケーションログインページの URL が入力された場合

SOAP および REST エンドポイントで null リファラーを許可してください。すべての URI ログインページ（/adminui、/contentspace、それらに対応するマッピングされたリソースなど）でも、null リファラーを許可してください。例えば、/contentspace に対してマッピングされたサーブレット /contentspace/faces/jsp/login.jsp は、null リファラーの例外とすることが必要です。この例外は、web アプリケーションで GET フィルタリングを有効にしている場合にのみ必要です。null リファラーを許可するかどうかはアプリケーションで指定できます。[AEM Forms の堅牢化とセキュリティ](https://help.adobe.com/ja_JP/livecycle/11.0/HardeningSecurity/index.html)の「クロスサイトリクエストフォージェリー攻撃からの保護」を参照してください。

**許可されているリファラーの例外：**&#x200B;許可されているリファラーの例外は、許可されているリファラーリストのサブリストです。このリファラーの例外からのリクエストはブロックされます。許可されているリファラーの例外は、web アプリケーションに固有のものです。許可されているリファラーの例外のサブセットを、特定の web アプリケーションの呼び出しに対して許可しない場合は、許可されているリファラーの例外を使用してリファラーをブロックリストに登録できます。許可されているリファラーの例外は、アプリケーションの web.xml ファイル内で指定します（ヘルプとチュートリアルページの AEM Forms の堅牢化とセキュリティの「クロスサイトリクエストフォージェリー攻撃からの保護」を参照してください）。

## 許可されているリファラーの機能の仕組み {#how-allowed-referers-work}

AEM Forms にはリファラーのフィルタリング機能が用意されており、CSRF 攻撃の防止に役立ちます。以下にリファラーのフィルタリングが機能する仕組みを示します。

1. Forms サーバーが、呼び出しに使用される HTTP メソッドを確認します。

   * POST の場合、Forms サーバーはリファラーのヘッダーのチェックを実行します。
   * GET の場合、Forms サーバーはリファラーをチェックしません。ただし、CSRF_CHECK_GETS が true に設定されている場合は除きます。この場合、Forms サーバーはリファラーのヘッダーを確認します。CSRF_CHECK_GETS は、アプリケーションの web.xml ファイル内で指定されます（[堅牢化とセキュリティガイド](https://help.adobe.com/ja_JP/livecycle/11.0/HardeningSecurity/index.html)の「クロスサイトリクエストフォージェリー攻撃からの保護」を参照してください）。

1. Forms サーバーが、リクエストされた URI が許可リスト登録済みかどうかを確認します。

   * URI が許可リスト登録済みの場合、サーバーはリクエストを渡します。
   * リクエストされた URI が許可リストに登録されていなかった場合、サーバーはリクエストのリファラーを取得します。

1. リクエスト内にリファラーがある場合、サーバーはそれが許可されているリファラーかどうかを確認します。許可されている場合は、リファラーの例外を確認します。

   * 例外の場合、リクエストはブロックされます。
   * 例外でない場合、リクエストは渡されます。

1. リクエスト内にリファラーが指定されていない場合、サーバーは null リファラーが許可されているかどうかを確認します。

   * null リファラーが許可されている場合は、リクエストが渡されます。
   * null リファラーが許可されていない場合、サーバーはリクエストされた URI が null リファラーの例外であるかどうかを確認し、その結果に基づいてリクエストを処理します。

## 許可されているリファラーの設定 {#configure-allowed-referers}

Configuration Manager を実行すると、許可されているリファラーリストに、デフォルトのホストおよび IP アドレス、または Forms サーバーが追加されます。このリストは、管理コンソールで編集できます。

1. 管理コンソールで、設定／User Management／設定／許可されているリファラー URL を設定をクリックします。許可されているリファラーリストがページ下部に表示されます。
1. 許可されているリファラーを追加するには、次の手順を実行します。

   * 許可されているリファラーボックスにホスト名または IP アドレスを入力します。一度に複数の許可されているリファラーを追加するには、各ホスト名または IP アドレスを 1 行ごとに入力します。
   * HTTP ポートボックスと HTTPS ポートボックスで、HTTP または HTTPS のいずれか、または両方を許可するポートを指定します。これらのボックスを空のままにした場合、デフォルトのポート（HTTP ではポート 80、HTTPS ではポート 443）が使用されます。ボックスに `0`（ゼロ）を入力した場合、そのサーバー上のすべてのポートが有効になります。特定のポート番号を入力して、そのポートのみを有効にすることもできます。
   * 「追加」をクリックします。

1. 許可されているリファラーリストからエントリを削除するには、リストから項目を選択して、「削除」をクリックします。

   許可されているリファラーリストが空の場合、CSRF 機能は動作を停止し、システムのセキュリティが低下します。

1. 許可されているリファラーリストを変更したら、AEM Forms サーバーを再起動してください。
