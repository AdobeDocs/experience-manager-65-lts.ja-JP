---
title: HTML5 フォームの最適化
description: HTML5 フォームの出力サイズを最適化できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdb9edc2-6a37-4d3f-97d5-0fc5664316be
feature: HTML5 Forms,Mobile Forms
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
exl-id: 1ab2fe5d-5fac-4a11-8d27-7c7607f98653
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 100%

---

# HTML5 フォームの最適化 {#optimizing-html-forms}

HTML5 フォームは、フォームを HTML5 形式でレンダリングします。フォームサイズやフォーム内の画像などの要因によって、結果の出力が大きくなる場合があります。データ転送を最適化するために、推奨されるアプローチは要求を対処する Web サーバーを使用して HTML 応答を圧縮することです。このアプローチでは、応答サイズ、ネットワークトラフィック、およびサーバーとクライアントマシンの間でのデータのストリーミングに要する時間を削減できます。

この記事は JBoss で、Apache Web Server 2.0 32 ビットの圧縮を有効にするために必要な手順を説明します。

>[!NOTE]
>
>次の手順は Apache Web Server 2.0 32 ビット以外のサーバーには適用されません。

お使いのオペレーティングシステムに適した Apache Web Server ソフトウェアを入手します。

* Windows の場合、Apache web サーバーを Apache HTTP Server Project サイトからダウンロードします。
* Solaris 64 ビットの場合、Apache web サーバーを Sunfreeware for Solaris web サイトからダウンロードします。
* Linux の場合、Apache web サーバーは、Linux システムにプレインストールされています。

Apache は HTTP または AJP プロトコルを使用して JBoss と通信できます。

1. *APACHE_HOME/conf/httpd.conf* ファイル内で次のモジュール設定に対してコメント解除します。

   ```java
   LoadModule proxy_balancer_module modules/mod_proxy.so
   LoadModule proxy_balancer_module modules/mod_proxy_http.so
   LoadModule deflate_module modules/mod_deflate.so
   ```

   >[!NOTE]
   >
   >Linux では、デフォルトの APACHE_HOME ディレクトリは /etc/httpd/ です。

1. JBoss のポート 8080 のプロキシを設定します。

   次の設定を *APACHE_HOME/conf/httpd.conf* 設定ファイルに追加します。

   ```java
   ProxyPass / https://<server_Name>:8080/
   ProxyPassReverse / https://<server_Name>:8080/
   ```

   >[!NOTE]
   >
   >プロキシを使用する場合、次の設定変更が必要です。
   >
   >* アクセス：*https://&lt;server>:&lt;port>/system/console/configMgr*
   * Apache Sling Referrer Filter 設定の編集
   * 「Allow Hosts」フィールドで、プロキシサーバーのエントリを追加します。

1. 圧縮を有効化します。

   次の設定を *APACHE_HOME/conf/httpd.conf* 設定ファイルに追加します。

   ```xml
   <Location /content/xfaforms>
     <IfModule mod_deflate.c>
        SetOutputFilter DEFLATE
        # Don’t compress
        SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
        SetEnvIfNoCase Request_URI \.(?:exe|t?gz|zip|bz2|sit|rar)$ no-gzip dont-vary
       #Dealing with proxy servers
   
        <IfModule mod_headers.c>
           Header append Vary User-Agent
        </IfModule>
     </IfModule>
   </Location>
   ```

1. AEM サーバーにアクセスするには、https://[Apache_server]:80 を使用します。
