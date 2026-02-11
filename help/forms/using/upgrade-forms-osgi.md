---
title: OSGi でのAEM 6.5 Forms LTS へのアップグレード
description: AEM 6.5.22.0 FormsからAEM 6.5 Forms LTS に直接アップグレードすることができます。
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: b7aa877f9e782b0568adc7baa440dc630c690454
workflow-type: tm+mt
source-wordcount: '1527'
ht-degree: 47%

---

# OSGi でのAEM 6.5 Forms LTS へのアップグレード {#upgrade-to-aem-forms-osgi}

[AEM 6.5 からAEM 6.5 LTS へのアップグレード &#x200B;](/help/sites-deploying/upgrade.md) を行うには、AEM 6.5.22.0 Forms以降にアップグレードします。 AEM 6.5.22.0 からAEM 6.5 Forms LTS への直接アップグレードがサポートされています。

AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms、AEM 6.3 Forms、AEM 6.4 FormsまたはAEM 6.5 Formsを使用している場合、AEM 6.5 Forms LTS に直接アップグレードすることはできません。 アップグレードパスについて詳しくは、「[&#x200B; アップグレードパス &#x200B;](/help/forms/using/upgrade.md) ドキュメントを参照してください。

サービスパック AEM Forms 6.5.22.0 にアップグレードした後、次の手順に従ってAEM 6.5 LTS Formsにアップグレードします。

1. AEM Forms アドオンパッケージのインストール. 手順は次のとおりです。

   1. [ソフトウェア配布](https://experience.adobe.com/jp/downloads)を開きます。ソフトウェア配布にログインするには、Adobe ID が必要です。
   1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」を選択します。
   1. 「**[!UICONTROL フィルター]**」セクションで、
      1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
      1. パッケージのバージョンとタイプを選択します。また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
   1. お使いのオペレーティングシステムに適した Forms アドオンパッケージの名前を選択し、「**[!UICONTROL EULA 利用条件に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」を選択します。
   1. [パッケージマネージャー](/help/sites-administering/package-manager.md)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
   1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

      「[AEM Forms リリース](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)」記事に記載されている直接リンクからパッケージをダウンロードすることもできます。

      パッケージのインストールが完了したら、AEM インスタンスを再起動します。**その際、すぐにサーバーを停止しないでください。** AEM Forms サーバーを停止する前に、ServiceEvent REGISTERED メッセージと ServiceEvent UNREGISTERED メッセージが &lt;crx-repository>/error.log ファイルに表示されなくなり、このログファイルが安定した状態になるまで待ちます。また、いくつかのパッケージについては、インストールされたままの状態になる場合があります。これらのパッケージの状態は無視しても問題ありません。


      **次の追加の JVM コマンドラインパラメーターを使用してAEM インスタンスを再起動します**。
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      サーバーがスクリプトまたはサービスを使用して起動された場合は、上記の内容を含めるようにサーバーを適切に更新し、その後の再起動後も有効になるようにします。

      >[!NOTE]
      >
      > 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

1. インストール後のアクティビティを実行します。

   * **移行ユーティリティを実行**

     移行ユーティリティにより、以前のバージョンのアダプティブフォームや対応する管理アセットが AEM 6.5 Forms で使用できるようになります。このユーティリティは、AEM ソフトウェア配布からダウンロードできます。 移行ユーティリティの詳しい設定方法と使用方法については、[移行ユーティリティ](../../forms/using/migration-utility.md)に関する説明を参照してください。

     [ドラフト統合とコンポーネント送信のサンプル](https://helpx.adobe.com/jp/experience-manager/6-3/forms/using/integrate-draft-submission-database.html)をデータベースで使用して旧バージョンのアップグレードを行う場合は、アップグレードの実行後に、以下の SQL クエリを実行してください。

     ```sql
     UPDATE metadata m, additionalmetadatatable am
     SET m.dataType = am.value
     WHERE m.id = am.id
     AND am.key = 'dataType'
     ```

     ```sql
     DELETE from additionalmetadatatable
     WHERE `key` = 'dataType'
     ```

   * **Adobe Sign の再設定（AEM 6.2 Forms 以前のバージョンをアップグレードする場合のみ）**

     Adobe Sign を以前のバージョンの AEM Forms で設定してある場合は、AEM Cloud サービスから Adobe Sign を再設定します。詳しくは、[Adobe Sign と AEM Forms の統合](../../forms/using/adobe-sign-integration-adaptive-forms.md)を参照してください。

   * **jQuery のサポート**

     AEM 6.5 Forms では、jQuery のバージョンが 3.2.1 に、jQuery UI のバージョンが1.12.1に更新されます。AEM Form は、**noConflict** モードの JQuery を使用します。そのため、他の jQuery バージョンを使用している場合、アップグレードの実行中に問題は表示されません。 ただし、AEM 6.5 Forms にアップグレードする場合は、次の手順を実行します。

      * カスタムコンポーネントが（存在する場合）、サポートされる jQuery バージョンと互換性があることを確認します。
      * サポートされていない API をカスタムコンポーネントから削除します。 削除された API のリストについては、[アップグレードガイド](https://jquery.com/upgrade-guide/3.0/)を参照してください。 例えば、load()、.unload()、.error() の各 API のサポートは削除されています。 前述の API の代わりに.on() メソッドを使用します。 例えば、$(&quot;img&quot;).load(fn) を $(&quot;img&quot;).on(&quot;load&quot;, fn) に変更します。

   * **分析機能とレポートの再設定（バージョン 6.2 以前の AEM Forms をアップグレードする場合のみ）** 

     AEM 6.4 Forms では、ソースのトラフィック変数とインプレッションの成功イベントは使用できません。そのため、バージョン 6.2 以前の AEM Forms をアップグレードすると、AEM Forms から Adobe Analytics サーバーにデータが送信されなくなり、アダプティブフォームの分析レポートが使用できなくなります。さらに、AEM 6.4 Forms では、フォーム分析のバージョンのトラフィック変数と、フィールドでの滞在時間の成功イベントが導入されています。そのため、AEM Forms 環境で分析とレポートを再設定します。詳しい手順については、[分析とレポートの設定](../../forms/using/configure-analytics-forms-documents.md)を参照してください。

1. サーバーのアップグレードが成功し、すべてのデータが正常に移行され、問題なく動作することを確認してください。

   * **バンドルのステータスを確認：**&#x200B;すべてのバンドルがアクティブ状態になっていることを確認します。
   * **レプリケーションとリバースレプリケーションの検証：**&#x200B;移行されたフォームをいくつか公開、入力および送信します。送信されたデータも検証します。
   * **管理者および開発者のユーザーインターフェイスへのアクセスを確認：**&#x200B;管理者アカウントで AEM インスタンスにログインし、次の URL にアクセスできることを確認します。

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >AEM 6.4 Forms では crx-repository の構造が変更されています。6.3 Forms から AEM 6.5 Forms にアップグレードした場合、新規作成するカスタマイズについては、変更後のパスを使用してください。変更後のパスの一覧については、「[AEM Forms におけるリポジトリの再構築](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5)」を参照してください。


## JBoss EAP 8 へのAEMのデプロイ（Windows）

### 概要

このガイドでは、JDK 21 を使用して、Windows 環境の JBoss Enterprise Application Platform （EAP） 8 にAdobe Experience Manager（AEM）をスタンドアロンの OSGi WAR ファイルとしてデプロイする手順を説明します。

### システム要件

デプロイメントプロセスを開始する前に、お使いの環境が次の要件を満たしていることを確認します。

| コンポーネント | 要件 |
|-----------|-------------|
| オペレーティングシステム | Windows Server 2016 以降（64 ビット） |
| Java 開発キット | JDK 21 （Oracleまたは OpenJDK） |
| アプリケーションサーバー | JBoss EAP 8.x |
| AEM配布 | AEM WAR ファイル（Adobeから取得） |

>[!NOTE]
>
> `JAVA_HOME` 環境変数が JDK 21 インストールディレクトリを指していることを確認します。

### 手順 1:JBoss EAP 8 のインストール

#### JBoss EAP のダウンロード

1. Red Hat 開発者ポータルに移動します。\
   [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. Windows 用 JBoss EAP 8 ZIP 配布をダウンロードします。

#### JBoss EAP の抽出

1. ダウンロードした ZIP ファイルを目的のインストールディレクトリに抽出します。

2. このガイド全体で使用する `<JBOSS_HOME>` は、このディレクトリパスに注意してください。

   **例：**\
   ```C:\jboss-eap-8.0```

### 手順 2:AEM WAR ファイルを準備

#### AEM戦争を得る

Adobe ソフトウェア配布またはAdobeの担当者からAEM WAR ファイルを入手します。

#### WAR ファイル名を変更

WAR ファイルの名前を、目的の URL コンテキストパスに合わせて変更します。

```
cq-quickstart.war
```

>[!IMPORTANT]
>
> WAR ファイル名によって、アプリケーションの URL コンテキストが決まります。 例えば、`cq-quickstart.war` は `/cq-quickstart` でアクセス可能になります。


### 手順 3:AEM WAR の設定

設定の変更はすべて、JBoss へのデプロイ **前** に完了する必要があります。

#### 作業ディレクトリの作成

1. 一時的な作業ディレクトリを作成します。

   ```
   C:\aem\war-config
   ```

2. `cq-quickstart.war` を、このディレクトリにコピーします。

#### WAR コンテンツの抽出

1. **コマンドプロンプト** を開き、作業ディレクトリに移動します。

   ```cmd
   cd C:\aem\war-config
   ```

2. WAR ファイルを解凍します。

   ```cmd
   jar -xvf cq-quickstart.war
   ```

   これにより、`WEB-INF` およびその他のアプリケーションファイルを含んだディレクトリ構造が作成されます。

### 手順 4:JBoss デプロイメント記述子の設定

#### 配置構造ファイルを作成

1. 抽出した WAR 内の `WEB-INF` ディレクトリに移動します。

   ```cmd
   cd WEB-INF
   ```

2. `jboss-deployment-structure.xml` という名前の新規ファイルを作成します。

3. 次の XML コンテンツを追加します。

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jboss-deployment-structure xmlns="urn:jboss:deployment-structure:1.2">
       <deployment>
           <dependencies>
               <module name="jdk.unsupported" />
           </dependencies>
       </deployment>
   </jboss-deployment-structure>
   ```

4. ファイルを保存して閉じます。

**目的：** この設定を使用すると、AEMで必要な JDK 内部モジュールにアクセスできます。

### 手順 5：マルチパートアップロード設定の指定

>[!NOTE]
>
> 手順 5 は、**AEM Forms** にのみ適用されます。 **AEMのみ** を設定している場合は、この手順をスキップできます。


#### web.xml の変更

1. `WEB-INF\web.xml` をテキストエディターで開きます。

2. 実行モード設定を含む `<servlet>` セクションを見つけます。

   ```xml
   <!-- Set the runmode per default to author -->
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

3. 終了 `</servlet>` タグと前の行を次のように置き換えます。

   ```xml
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <multipart-config>
       <max-file-size>1048576000</max-file-size>
       <max-request-size>1048576000</max-request-size>
       <file-size-threshold>0</file-size-threshold>
   </multipart-config>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

4. 保存して閉じ `web.xml` す。

**目的：** この設定を使用すると、AEM Formsおよびデジタルアセット管理で、大きなファイルのアップロード（最大 1 GB）が可能になります。

### 手順 6:WAR ファイルの再パッケージ化

すべての設定変更が完了したら、WAR ファイルを再パッケージ化します。

1. 抽出したコンテンツを含む作業ディレクトリに戻ります。

   ```cmd
   cd C:\aem\war-config
   ```

2. 新規 WAR ファイルを作成します。

   ```cmd
   jar -cvf cq-quickstart.war *
   ```

>[!IMPORTANT]
>
> この手順は、すべての設定が完了した後、1 回だけ実行します。

### 手順 7:AEMのデプロイと開始

#### JBoss への WAR のデプロイ

1. 再パッケージ化された `cq-quickstart.war` を JBoss デプロイメントディレクトリにコピーします。

   ```
   <JBOSS_HOME>\standalone\deployments
   ```

   **例：**
   ```C:\jboss-eap-8.0\standalone\deployments```

#### JVM 設定の指定（オプションですが推奨）

JBoss を起動する前に、JVM メモリ設定を指定します。

1. `<JBOSS_HOME>\bin\standalone.conf.bat` をテキストエディターで開きます。

1. ヒープメモリを設定するには、次の行を変更または追加します。

   ```batch
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=512m"
   ```

>[!NOTE]
>
> サーバーの処理能力とAEMの要件に応じて、メモリ値を調整します。

1. ファイルを保存して閉じます。

#### JBoss EAP の起動

1. **コマンドプロンプト** を **管理者** として開きます。

1. JBoss bin ディレクトリに移動します。

   ```cmd
   cd <JBOSS_HOME>\bin
   ```

   **例：**
   ```cmd cd C:\jboss-eap-8.0\bin```

1. JBoss サーバーを起動します。

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

   **パラメーター：**
   * `-b 0.0.0.0` — サーバをすべてのネットワーク インターフェイスにバインドします。
   * `-bmanagement 0.0.0.0` – 管理インターフェイスをすべてのネットワーク インターフェイスにバインドします

#### デプロイメントの監視

コンソール出力でデプロイメントメッセージを確認します。 デプロイメントの成功は、次のように示されます。

```
Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
```

### 手順 8:AEMへのアクセス

デプロイメントが完了し、AEMが完全に開始したら、以下を行います。

**AEM オーサー URL:**
```http://<server-ip>:8080/cq-quickstart```

**デフォルトの資格情報：**

* ユーザー名：`admin`
* パスワード：`admin`

**重要：** 最初のログイン直後にデフォルトのパスワードを変更します。

### トラブルシューティング

#### よくある問題

| 問題 | 解決策 |
|-------|----------|
| ClassNotFoundException でデプロイが失敗する | `jboss-deployment-structure.xml` が正しく設定されていることを確認します。 |
| 起動時の OutOfMemoryError | `standalone.conf.bat` のヒープメモリを増やす |
| デプロイ後にAEMが開始しない | `<JBOSS_HOME>\standalone\log\server.log` で JBoss ログを確認する |
| ブラウザーでAEMにアクセスできない | ファイアウォール設定でポート 8080 が許可されていることを確認します。 |

#### ログファイル

* **JBoss サーバーログ：** `<JBOSS_HOME>\standalone\log\server.log`
* **AEM エラーログ：** で起動後、AEM Web コンソールから使用可能\
  `http://<server-ip>:8080/cq-quickstart/system/console`

### その他の設定

#### 実行モードの設定

AEMの実行モード（オーサー/パブリッシュ）を変更するには、WAR を再パッケージ化する前に、`sling.run.modes` で `WEB-INF\web.xml` パラメーターを変更します。

```xml
<init-param>
    <param-name>sling.run.modes</param-name>
    <param-value>publish</param-value>
</init-param>
```

#### 実稼動の推奨事項

実稼動環境の場合：

* JBoss での SSL/TLS 証明書の設定
* AEM レプリケーションエージェントの設定
* ロードバランシング用の Dispatcher の設定
* 自動バックアップを有効にする
* 監視とアラートの実装

### 関連ドキュメント

* [JBoss EAP 8 ドキュメント &#x200B;](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0)
* [Adobe Experience Manager ドキュメント &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
* [AEM インストールおよびデプロイメントガイド &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=ja)

### ドキュメント情報

| フィールド | 値 |
|-------|-------|
| 最終更新日 | 2026年2月 |
| AEM のバージョン | 6.5 以上（LTS） |
| JBoss バージョン | EAP 8.x |
| JDK バージョン | 21 |
| プラットフォーム | Windows |


