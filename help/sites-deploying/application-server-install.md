---
title: アプリケーションサーバーのインストール
description: Adobe Experience Manager をアプリケーションサーバーと共にインストールする方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 09d54b52-485a-453c-a2d0-535adead9e6c
source-git-commit: 5f968f5dc0696a683cc063d330c8edfba05f11ab
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 42%

---

# アプリケーションサーバーのインストール{#application-server-install}

>[!NOTE]
>
>Adobe Experience Manager（AEM）がリリースされているファイル形式は `JAR` と `WAR` です。これらの形式に対しては、アドビが提供するサポートレベルを維持できるよう、品質保証プロセスが実施されています。
>

この節では、アプリケーションサーバーを使用してAdobe Experience Manager（AEM）をインストールする方法について説明します。個々のアプリケーションサーバーに提供されている特定のサポートのレベルについては、「[サポートされているプラットフォーム](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers)」セクションを参照してください。

以下のアプリケーションサーバーのインストール手順について説明します。

* [WebSphere](#websphere)
* [Tomcat 11.0.x](#tomcat)

Web アプリケーションのインストール、サーバーの設定、サーバーの起動および停止方法について詳しくは、該当するアプリケーションサーバーのドキュメントを参照してください。

<!-- >[!NOTE]
>
>If you are using Dynamic Media in a WAR deployment, see [Dynamic Media documentation](/help/assets/config-dynamic.md#enabling-dynamic-media). -->

## 概要 {#general-description}

### アプリケーションサーバーに AEM をインストールするときのデフォルトの動作 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM は、単一の war ファイルとしてデプロイされます。

デプロイすると、デフォルトで次のようになります。

* 実行モードは `author`
* インスタンス（リポジトリ、Felix OSGI 環境、バンドルなど）は `${user.dir}/crx-quickstart` にインストールされます。`${user.dir}` は現在の作業ディレクトリです。 crx-quickstart へのこのパスは `sling.home` です。

* コンテキストルートは war ファイル名です。 例えば、`aem-65-lts` のように指定します。

#### 設定 {#configuration}

デフォルトの動作は次のように変更できます。

* 実行モード：デプロイメント前に、AEM war ファイルの `sling.run.modes` ファイルで `WEB-INF/web.xml` パラメーターを設定

* sling.home：デプロイメント前に、AEM war ファイルの `WEB-INF/web.xml` ファイルで `sling.home` パラメーターを設定

* コンテキストルート：AEM war ファイル名を変更

#### パブリッシュインストール {#publish-installation}

パブリッシュインスタンスをデプロイするには、実行モードを publish に設定する必要があります。

* AEM war ファイルから `WEB-INF/web.xml` を解凍します
* パラメーター `sling.run.modes` 公開に変更
* `web.xml` ファイルをAEM war ファイルに再圧縮します。
* AEM war ファイルをデプロイします。

#### インストールの確認 {#installation-check}

すべてがインストールされているかどうかを確認するには、次の操作を行います。

* `error.log` ファイルに対して「テール」を実行して、すべてのコンテンツがインストールされていることを確認
* `/system/console` を調べて、すべてのバンドルがインストールされていることを確認

#### 同じアプリケーションサーバーに 2 つのインスタンス {#two-instances-on-the-same-application-server}

デモ目的で、オーサーインスタンスとパブリッシュインスタンスの両方を 1 つのアプリケーションサーバーにインストールするのが適切な場合があります。 これを実現するには、次の手順を実行する必要があります。

1. パブリッシュインスタンス `sling.home` 変数と `sling.run.modes` 変数の変更
1. AEM war ファイルから `WEB-INF/web.xml` ファイルを解凍します
1. `sling.home` パラメーターを別のパスに変更する（絶対パスと相対パスが指定可能）
1. パブリッシュインスタンスの `sling.run.modes` を `publish` に変更します
1. `web.xml` ファイルを再圧縮
1. war ファイルの名前を、別々の名前になるように変更します。例えば、一方の名前を `aemauthor.war` に、もう一方の名前を `aempublish.war` に変更します
1. 高めのメモリ設定を使用します。例えば、デフォルトの AEM インスタンスの場合は、`-Xmx3072m` などを使用します。
1. 2 つの web アプリケーションをデプロイします
1. デプロイメント後、2 つの Web アプリケーションを停止します
1. オーサーインスタンスとパブリッシュインスタンスの両方で、`sling.properties` ファイルでプロパティ `felix.service.urlhandlers` が `false` に設定されていることを確認します。 （デフォルトでは `true` に設定されています）。
1. 2 つの web アプリケーションを再起動します。

## アプリケーションサーバーのインストール手順 {#application-servers-installation-procedures}

### WebSphere® 24.0.0.7 {#websphere}

デプロイメントの前に、上記の [ 概要 ](#general-description) をお読みください。

**サーバーの準備**

* Basic 認証ヘッダーを無効にします。

   * AEMによるユーザー認証を可能にする 1 つの方法は、WebSphere® サーバーのグローバル管理セキュリティを無効にすることです。 これをおこなうには、**セキュリティ/Global Security** に移動し、**Enable administrative security （管理セキュリティを有効にする）チェックボックス** のチェックを外して、サーバーを保存して再起動します。

* `"JAVA_OPTS= -Xmx2048m"` の設定
* コンテキストルート = / を使用して AEM をインストールする場合は、既存のデフォルト web アプリケーションのコンテキストルートを変更します。

**AEM Web アプリケーションのデプロイ**

* AEM war ファイルをダウンロードします
* 必要に応じて、`web.xml` ファイルで設定を行います。 詳しくは、上記の [ 概要 ](#general-description) を参照してください。

   * `WEB-INF/web.xml` ファイルを解凍します
   * `sling.run.modes` パラメーターを `publish` に変更します
   * 最初の `sling.home` パラメーターのコメントを解除し、必要に応じてこのパスを設定します
   * `web.xml` ファイルを再圧縮します。

* AEM war ファイルのデプロイ

   * コンテキストルートを選択してください Sling 実行モードを設定する場合は、デプロイウィザードの詳細手順を選択してから、ウィザードの手順 6 で指定する必要があります。

* AEM Web アプリケーションの起動

#### Tomcat 11.0.x {#tomcat}

デプロイ前に、上記の[概要](#general-description)をお読みください。

* **Tomcat サーバーの準備**

   * VM メモリ設定の値を増やします。

      * `bin/catalina.bat`（UNIX® の場合は `catalina.sh`）に、次の設定を追加します。

        ```
        set "JAVA_OPTS= -Xmx2048m`
        ```

   * Tomcat では、インストール時に管理者またはマネージャーによるアクセスは有効になりません。 そのため、次のアカウントへのアクセスを許可するには `tomcat-users.xml` を手動で編集する必要があります。

      * `tomcat-users.xml` を編集して、管理者およびマネージャーのアクセスを含めます。設定は次の例のようになります。

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
        role rolename="manager"/>
        role rolename="tomcat"/>
        <role rolename="admin"/>
        <role rolename="role1"/>
        <role rolename="manager-gui"/>
        <user username="both" password="tomcat" roles="tomcat,role1"/>
        <user username="tomcat" password="tomcat" roles="tomcat"/>
        <user username="admin" password="admin" roles="admin,manager-gui"/>
        <user username="role1" password="tomcat" roles="role1"/>
        </tomcat-users>
        ```

   * コンテキストルート「/」を使用して AEM をデプロイする場合は、既存の ROOT web アプリケーションのコンテキストルートを変更する必要があります。

      * ルート Web アプリケーションを停止してデプロイ解除します
      * Tomcat の webapps フォルダーにある `ROOT.war` フォルダーの名前を変更します。
      * Web アプリを再起動します。

   * manager-gui を使用してAEM web アプリケーションをインストールする場合は、アップロードするファイルの最大サイズを増やす必要があります。デフォルトでは、アップロードできるサイズは 50 MB までです。 これを実現するには、マネージャー web アプリケーションの `web.xml` を開きます。

     `webapps/manager/WEB-INF/web.xml`

     `max-file-size` と `max-request-size` を 500 MB 以上に増やします。 以下の `web.xml` ファイルの例で、次の `multipart-config` を参照してください。

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **AEM Web アプリケーションのデプロイ**

   * AEM war ファイルをダウンロードします。
   * 必要に応じて、`web.xml` ファイルで設定を行います。

      * `WEB-INF/web.xml` ファイルを解凍します
      * `sling.run.modes` パラメーターを `publish` に変更します
      * 最初の `sling.home` パラメーターのコメントを解除し、必要に応じてこのパスを設定します
      * `web.xml` ファイルを再圧縮します。

   * ルート Web アプリケーションとしてデプロイする場合は、AEM war ファイルの名前を `ROOT.war` に変更します。 `aemauthor` をコンテキストルートにする場合は、名前を `aemauthor.war` に変更します。
   * Tomcat の webapps フォルダーにコピーします。
   * AEM がインストールされるまで待ちます。
