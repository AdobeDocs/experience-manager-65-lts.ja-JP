---
title: プロキシサーバーツールを使用する方法
description: プロキシサーバーは、クライアントとサーバー間でリクエストをリレーする中間サーバーとして機能します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
exl-id: e33640ba-6039-4057-8942-b4faa9b2e250
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 100%

---

# プロキシサーバーツールを使用する方法{#how-to-use-the-proxy-server-tool}

プロキシサーバーは、クライアントとサーバー間のリクエストをリレーする中間サーバーとして機能します。プロキシサーバーは、クライアントとサーバーのインタラクションをすべて追跡し、TCP 通信全体のログを出力します。これにより、メインのサーバーにアクセスすることなく、現状を正確に監視できます。

プロキシサーバーは AEM インストール環境の次の場所にあります。

`crx-quickstart/opt/helpers/proxy-2.1.jar`

基盤となる通信プロトコルに関係なく、プロキシサーバーを使用して、クライアントとサーバーのインタラクションをすべて監視できます。例えば、以下のプロトコルを監視できます。

* HTTP（Web ページ用）
* HTTPS（セキュリティで保護された web ページ用）
* SMTP（メールメッセージ用）
* LDAP（ユーザー管理用）

例えば、TCP/IP ネットワーク経由で通信する任意の 2 つのアプリケーション（Web ブラウザーと AEM など）の間にプロキシサーバーを配置できます。これにより、CQ ページのリクエスト時の状況を正確に監視できます。

## プロキシサーバーツールの起動 {#starting-the-proxy-server-tool}

コマンドラインでサーバーを起動します。

`java -jar proxy-2.1.jar <host> <remoteport> <localport> [options]`

**パラメーター**

`<host>`

接続先の CRX インスタンスのホストアドレスです。インスタンスがローカルコンピューター上にある場合、これは `localhost` です。

`<remoteport>`

ターゲット CRX インスタンスのホストポートです。例えば、新しくインストールする AEM インストールのデフォルト値は **`4502`** です。また、新しくインストールする AEM オーサーインスタンスのデフォルト値は `4502` です。

`<localport>`

プロキシ経由で CRX インスタンスにアクセスするために接続するローカルマシン上のポートです。

**オプション**

`-q`（クワイエットモード）

コンソールウィンドウに出力を書き込みません。接続速度を低下させたくない場合や出力をファイルに記録する場合は、このオプションを使用します（-logfile オプションを参照）。

`-b`（バイナリモード）

トラフィック内で特定のバイトの組み合わせを検索する場合は、バイナリモードを有効にします。出力には 16 進および文字の出力が含まれます。

`-t`（タイムスタンプのログエントリ）

各ログ出力にタイムスタンプを追加します。タイムスタンプは秒単位なので、単一のリクエストの確認には適していない場合があります。長時間プロキシサーバーを使用する場合は、特定の時刻に発生したイベントを特定するためにこのオプションを使用します。

`-logfile <filename>`（ログファイルへの書き込み）

クライアントとサーバーのやり取りをログファイルに書き込みます。このパラメーターは静止モードでも使用できます。

**`-i <numIndentions>`**（インデントの追加）

アクティブな接続にはそれぞれ、読みやすさを考慮してインデントが指定されます。デフォルト値は 16 レベルです。この機能は `proxy.jar version 1.16` で導入されました。

### ログ形式 {#log-format}

proxy-2.1.jar が生成するログエントリはすべて次の形式になります。

`[timestamp (optional)] [Client|Server]-[ConnectionNumber]-[BytePosition] ->[Character Stream]`

例えば、web ページのリクエストは次のようになります。

`C-0-#000000 -> [GET /author/prox.html?CFC_cK=1102938422341 HTTP/1.1 ]`

* C は、このエントリがクライアントからのリクエスト（Web ページのリクエスト）であることを示します。
* 0 は接続数です（接続カウンターは 0 から開始します）。
* #00000 はバイトストリームのオフセットです。これは最初のエントリなので、オフセットは 0 です。
* `[GET <?>]` は、サンプルの HTTP ヘッダー（url）におけるリクエストのコンテンツです。

接続を閉じると、次の情報がログに記録されます。

```
C-6-Finished: 758 bytes (1.0 kb/s)
S-6-Finished: 665 bytes (1.0 kb/s)
```

これは、6 番目の接続において平均速度でクライアント（`C`）とサーバー（`S`）の間でやり取りされたバイト数を示します。

**ログ出力の例**

例として、要求時に次のコードを生成するページについて検討してみましょう。

### 例 {#example}

例として、次のリポジトリ内の単純な HTML ドキュメントについて検討してみましょう。

`/content/test.html`

さらに、次の画像ファイルがあります。

`/content/test.jpg`

`test.html` のコンテンツは次のとおりです。

```xml
<html>
<head>
    <title>Test</title>
</head>
<body>
    Test<br>
    <img src="test.jpg">
</body>
</html>
```

AEM インスタンスが `localhost:4502` で実行されている場合は、プロキシは次のように開始されます。

`java -jar proxy.jar localhost 4502 4444 -logfile test.log`

これで、`localhost:4444` のプロキシ経由で CQ／CRX インスタンスにアクセスできます。このポート経由のすべての通信は `test.log` に記録されます。

プロキシの出力を確認すると、ブラウザーと AEM インスタンスの間のインタラクションが表示されます。

起動時に、プロキシは次の情報を出力します。

```xml
starting proxy for localhost:4502 on port 4444
using logfile: <some-dir>/crx-quickstart/opt/helpers/test.log
```

ブラウザーを開いてテストページにアクセスします。

`http://localhost:4444/content/test.html`

ブラウザーがそのページの `GET` リクエストを行ったことを確認します。

```shell
C-0-#000000 -> [GET /content/test.html HTTP/1.1 ]
C-0-#000033 -> [Host: localhost:4444 ]
C-0-#000055 -> [Connection: keep-alive ]
C-0-#000079 -> [User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.11 (KHTML, like Gecko) Chrome/20.0.1132.57 Safari/536.11 ]
C-0-#000212 -> [Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8 ]
C-0-#000285 -> [Accept-Encoding: gzip,deflate,sdch ]
C-0-#000321 -> [Accept-Language: en-US,en;q=0.8 ]
C-0-#000354 -> [Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.3 ]
C-0-#000402 -> [Cookie: login-token=179ba6bd-e0a7-4909-a965-e11c7f2bc2fc%3a618bd8a8-fbaf-43c5-827d-c84c62248c5e_22ee860cc9036fee%3acrx.default%3b21148fb0-eb6c]
C-0-#000543 -> [-43c9-a2b9-c8d40618d8ae%3ad87a3d1a-5e9a-4d5a-bab1-0ee60ad6d8df_d0e4ddce0fcd84b6%3acrx.default%3b5cb95227-ea51-47bf-850b-68ad1dfd7297%3af3bbb6]
C-0-#000684 -> [59-7913-4285-8857-832c087bafd5_c484727d3b3665ad%3acrx.default; ys-cq-siteadmin-tree=o%3Awidth%3Dn%253A240%5EselectedPath%3Ds%253A/content ]
C-0-#000824 -> [ ]
```

AEM インスタンスが `test.html` ファイルのコンテンツを使用して応答します。

```shell
S-0-#000000 -> [HTTP/1.1 200 OK ]
S-0-#000017 -> [Connection: Keep-Alive ]
S-0-#000041 -> [Server: Day-Servlet-Engine/4.1.24  ]
S-0-#000077 -> [Content-Type: text/html;charset=utf-8 ]
S-0-#000116 -> [Content-Length: 104 ]
S-0-#000137 -> [Date: Mon, 16 Jul 2012 11:23:38 GMT ]
S-0-#000174 -> [Last-Modified: Mon, 16 Jul 2012 11:19:27 GMT ]
S-0-#000220 -> [ ]
S-0-#000222 -> [<html>]
S-0-#000229 -> [<head>]
S-0-#000236 -> [    <title>Test</title>]
S-0-#000260 -> [</head> ]
S-0-#000269 -> [<body>]
S-0-#000276 -> [ Test<br>]
S-0-#000286 -> [    <img src="test.jpg">]
S-0-#000311 -> [</body>]
S-0-#000319 -> [</html>]
```

### プロキシサーバーの使用例 {#uses-of-the-proxy-server}

次のシナリオは、プロキシサーバーツールの使用例を示しています。

**Cookie とその値の確認**

次のログエントリの例は、プロキシの起動後に開かれた 6 番目の接続でクライアントが送信したすべての Cookie とその値を示しています。

`C-6-#000635 -> [Cookie: cq3session=7e39bc51-ac72-3f48-88a9-ed80dbac0693; Show=ShowMode; JSESSIONID=68d78874-cabf-9444-84a4-538d43f5064d ]`

**ヘッダーとその値の確認**

次のログエントリの例は、サーバーによるキープアライブ接続の確立が可能であり、Content-Length ヘッダーが適切に設定されていることを示しています。

```
S-7-#000017 -> [Connection: Keep-Alive ]
 ...
 S-7-#000107 -> [Content-Length: 124 ]
```

**キープアライブが機能するかどうかの確認**

キープアライブは HTTP の機能の 1 つです。この機能により、クライアントはサーバーへの TCP 接続を再利用して、複数のリクエスト（ページコード、写真、スタイルシートなどのリクエスト）を行うことができます。キープアライブを使用しない場合、クライアントはリクエストごとに新しい接続を確立する必要があります。

キープアライブが機能するかどうかを確認するには：

* プロキシサーバーを起動します。
* ページのリクエストを行います。
* キープアライブが機能している場合は、接続カウンターで接続数が 5～10 を超えることはありません。
* キープアライブが機能していない場合は、接続カウンターが急激に増加します。

**失われたリクエストの検索**

複雑なサーバー設定でリクエストが失われた場合（例えば、ファイアウォールとディスパッチャーを使用する場合）は、プロキシサーバーを使用して、リクエストがどこで失われたかを特定できます。ファイアウォールがある場合は、次の手順を実行します。

* ファイアウォールの前にプロキシを起動します。
* ファイアウォールの後にもう 1 つのプロキシを起動します。
* この 2 つのプロキシを使用して、リクエストがどこまで届いているかを確認します。

**リクエストのハング**

リクエストがハングすることがある場合は、次の手順を実行します。

* プロキシを起動します。
* 待機するか、タイムスタンプを持つ各エントリと共にアクセスログをファイルに書き込みます。
* リクエストがハングし始めたら、開いた接続の数および問題の原因となったリクエストを確認できます。
