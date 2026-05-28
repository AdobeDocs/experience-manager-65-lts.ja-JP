---
title: OSGiでのAEM 6.5 Forms LTSへのアップグレード
description: AEM 6.5.22.0 FormsからAEM 6.5 Forms LTSに直接アップグレードできます。
content-type: reference
role: Admin, User
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, AEM Forms on OSGi, AEM Forms Upgrade
exl-id: 9233d4b7-441c-4cbd-86f8-2c52b99c3330
source-git-commit: b5db6129e83dd7a54516707bbdb8864dc709d54b
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 44%

---

# OSGiでのAEM 6.5 Forms LTSへのアップグレード {#upgrade-to-aem-forms-osgi}

AEM 6.5からAEM 6.5 LTS[&#128279;](/help/sites-deploying/upgrade.md)に アップグレードするには、AEM 6.5.22.0 Forms以降にアップグレードしてください。 AEM 6.5.22.0からAEM 6.5 Forms LTSへの直接アップグレードがサポートされています。

AEM 6.0 Forms、AEM 6.1 Forms、AEM 6.2 Forms、AEM 6.3 Forms、AEM 6.4 FormsまたはAEM 6.5 Formsを使用している場合、AEM 6.5 Forms LTSへの直接アップグレードは利用できません。 アップグレードパスについて詳しくは、[&#x200B; アップグレードパス &#x200B;](/help/forms/using/upgrade.md)のドキュメントを参照してください。

サービスパック AEM Forms 6.5.22.0にアップグレードした後、次の手順に従ってAEM 6.5 LTS Formsにアップグレードします。

1. AEM Forms アドオンパッケージのインストール. 手順は次のとおりです。

   1. [ソフトウェア配布](https://experience.adobe.com/jp/downloads)を開きます。 ソフトウェア配布にログインするには、Adobe ID が必要です。
   1. ヘッダーメニューで「**[!UICONTROL Adobe Experience Manager]**」を選択します。
   1. 「**[!UICONTROL フィルター]**」セクションで、
      1. 「**[!UICONTROL ソリューション]**」ドロップダウンリストから「**[!UICONTROL Forms]**」を選択します。
      1. パッケージのバージョンとタイプを選択します。 また、「**[!UICONTROL ダウンロードを検索]**」オプションを使用して結果をフィルターすることもできます。
   1. お使いのオペレーティングシステムに適した Forms アドオンパッケージの名前を選択し、「**[!UICONTROL EULA 利用条件に同意する]**」を選択して、「**[!UICONTROL ダウンロード]**」を選択します。
   1. [パッケージマネージャー](/help/sites-administering/package-manager.md)を開き「**[!UICONTROL パッケージをアップロード]**」をクリックしてパッケージをアップロードします。
   1. パッケージを選択して、「**[!UICONTROL インストール]**」をクリックします。

      「[AEM Forms リリース](https://experienceleague.adobe.com/ja/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases)」記事に記載されている直接リンクからパッケージをダウンロードすることもできます。

      パッケージのインストールが完了したら、AEM インスタンスを再起動します。 **サーバーを直ちに停止しないでください。** AEM Forms サーバーを停止する前に、&lt;crx-repository>/error.log ファイルにServiceEvent REGISTERED メッセージとServiceEvent UNREGISTERED メッセージが表示されなくなり、ログが安定するまで待ちます。 また、いくつかのパッケージについては、インストールされたままの状態になる場合があります。 これらのパッケージの状態は無視しても問題ありません。


      **次のJVM コマンドラインパラメーターを使用して、AEM インスタンスを再起動します**。
      `--add-opens java.base/java.util=ALL-UNNAMED --add-exports=java.xml/com.sun.org.apache.xml.internal.serialize=ALL-UNNAMED`

      サーバーがスクリプトまたはサービスを介して起動されている場合は、それに応じて更新して上記を含め、後で再起動した後も効果的になるようにします。

      >[!NOTE]
      >
      > 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。 Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

1. インストール後のアクティビティを実行します。

   * **移行ユーティリティを実行**

     移行ユーティリティにより、以前のバージョンのアダプティブフォームや対応する管理アセットが AEM 6.5 Forms で使用できるようになります。 このユーティリティは、AEM ソフトウェア配布からダウンロードできます。 移行ユーティリティの詳しい設定方法と使用方法については、[移行ユーティリティ](../../forms/using/migration-utility.md)に関する説明を参照してください。

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

     Adobe Sign を以前のバージョンの AEM Forms で設定してある場合は、AEM Cloud サービスから Adobe Sign を再設定します。 詳しくは、[Adobe Sign と AEM Forms の統合](../../forms/using/adobe-sign-integration-adaptive-forms.md)を参照してください。

   * **jQuery のサポート**

     AEM 6.5 Formsでは、jQueryのバージョンが3.2.1に更新され、jQuery UIのバージョンが1.12.1に更新されます。 AEM フォームは、**noConflict** モードでJQueryを使用します。 そのため、他の jQuery バージョンを使用している場合、アップグレードの実行中に問題は表示されません。 ただし、AEM 6.5 Forms にアップグレードする場合は、次の手順を実行します。

      * カスタムコンポーネントが（存在する場合）、サポートされる jQuery バージョンと互換性があることを確認します。
      * サポートされていない API をカスタムコンポーネントから削除します。 削除された API のリストについては、[アップグレードガイド](https://jquery.com/upgrade-guide/3.0/)を参照してください。 例えば、load()、.unload()、.error() の各 API のサポートは削除されています。 前述の API の代わりに.on() メソッドを使用します。 例えば、$(&quot;img&quot;).load(fn) を $(&quot;img&quot;).on(&quot;load&quot;, fn) に変更します。

   * **分析機能とレポートの再設定（バージョン 6.2 以前の AEM Forms をアップグレードする場合のみ）**

     AEM 6.4 Forms では、ソースのトラフィック変数とインプレッションの成功イベントは使用できません。 そのため、バージョン 6.2 以前の AEM Forms をアップグレードすると、AEM Forms から Adobe Analytics サーバーにデータが送信されなくなり、アダプティブフォームの分析レポートが使用できなくなります。 さらに、AEM 6.4 Forms では、フォーム分析のバージョンのトラフィック変数と、フィールドでの滞在時間の成功イベントが導入されています。 そのため、AEM Forms 環境で分析とレポートを再設定します。 詳しい手順については、[分析とレポートの設定](../../forms/using/configure-analytics-forms-documents.md)を参照してください。

1. サーバーのアップグレードが成功し、すべてのデータが正常に移行され、問題なく動作することを確認してください。

   * **バンドルのステータスを確認：**&#x200B;すべてのバンドルがアクティブ状態になっていることを確認します。
   * **レプリケーションとリバースレプリケーションの検証：**&#x200B;移行されたフォームをいくつか公開、入力および送信します。 送信されたデータも検証します。
   * **管理者および開発者のユーザーインターフェイスへのアクセスを確認：**&#x200B;管理者アカウントで AEM インスタンスにログインし、次の URL にアクセスできることを確認します。

      * `https://'[server]:[port]'/crx/packmgr`
      * `https://'[server]:[port]'/crx/de`
      * `https://'[server]:[port]'/aem/forms.html/content/dam/formsanddocuments`

   >[!NOTE]
   >
   >AEM 6.4 Forms では crx-repository の構造が変更されています。 6.3 Forms から AEM 6.5 Forms にアップグレードした場合、新規作成するカスタマイズについては、変更後のパスを使用してください。 変更後のパスの一覧については、「[AEM Forms におけるリポジトリの再構築](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/implementing/deploying/restructuring/forms-repository-restructuring-in-aem-6-5)」を参照してください。


## JBoss EAP 8へのAEMのデプロイ（Windows）

### 概要

このガイドでは、JDK 21を使用してWindows環境でJBoss Enterprise Application Platform （EAP） 8にAdobe Experience Manager （AEM）をスタンドアロン OSGi WAR ファイルとしてデプロイする手順を説明します。

### システム要件

デプロイメントプロセスを開始する前に、環境が次の要件を満たしていることを確認してください。

| Component | 要件 |
|-----------|-------------|
| オペレーティングシステム | Windows Server 2016以降（64 ビット） |
| Java開発キット | JDK 21 （OracleまたはOpenJDK） |
| アプリケーションサーバー | JBoss EAP 8.x |
| AEM配布 | AEM WAR ファイル（Adobeから取得） |

>[!NOTE]
>
> `JAVA_HOME`環境変数がJDK 21 インストールディレクトリを指していることを確認します。

### 手順1:JBoss EAP 8のインストール

#### JBoss EAPのダウンロード

1. Red Hat Developer ポータルに移動します。\
   [https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. Windows用JBoss EAP 8 ZIP ディストリビューションをダウンロードします。

#### JBoss EAPの抽出

1. ダウンロードしたZIP ファイルを任意のインストールディレクトリに展開します。

2. このガイド全体で使用するディレクトリパスは`<JBOSS_HOME>`として注意してください。

   **例：**\
   `C:\jboss-eap-8.0`

### 手順2:AEM WAR ファイルの準備

#### AEM戦争を入手

Adobe Software DistributionまたはAdobe担当者からAEM WAR ファイルを取得します。

#### WAR ファイルの名前を変更

目的のURL コンテキストパスを反映するように、WAR ファイルの名前を変更します。

```
cq-quickstart.war
```

>[!IMPORTANT]
>
> WAR ファイル名によって、アプリケーションのURL コンテキストが決まります。 例えば、`cq-quickstart.war`は`/cq-quickstart`にアクセスできます。


### 手順3:AEM WARの設定

JBossにデプロイする&#x200B;**前にすべての設定変更を完了する必要があります。**

#### 作業ディレクトリの作成

1. 一時的な作業ディレクトリを作成します。

   ```
   C:\aem\war-config
   ```

2. `cq-quickstart.war` を、このディレクトリにコピーします。

#### 戦争コンテンツの抽出

1. **コマンドプロンプト**&#x200B;を開き、作業ディレクトリに移動します。

   ```cmd
   cd C:\aem\war-config
   ```

2. WAR ファイルを抽出します。

   ```cmd
   jar -xvf cq-quickstart.war
   ```

   これにより、`WEB-INF`およびその他のアプリケーションファイルを含むディレクトリ構造が作成されます。

### 手順4:JBoss デプロイメント記述子の設定

#### デプロイメント構造ファイルの作成

1. 抽出したWAR内の`WEB-INF` ディレクトリに移動します。

   ```cmd
   cd WEB-INF
   ```

2. `jboss-deployment-structure.xml`という名前の新しいファイルを作成します。

3. 次のXML コンテンツを追加します。

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

**目的：**&#x200B;この設定は、AEMで必要なJDK内部モジュールへのアクセスを提供します。

### 手順5：マルチパートアップロード設定の設定

>[!NOTE]
>
> 手順5は、**AEM Forms**&#x200B;にのみ適用されます。 **AEMのみ**&#x200B;を設定する場合は、この手順をスキップできます。


#### Web.xmlの変更

1. `WEB-INF\web.xml`をテキストエディターで開きます。

2. 実行モード設定を含む`<servlet>` セクションを見つけます。

   ```xml
   <!-- Set the runmode per default to author -->
   <init-param>
       <param-name>sling.run.modes</param-name>
       <param-value>author</param-value>
   </init-param>
   <load-on-startup>100</load-on-startup>
   </servlet>
   ```

3. 閉じる`</servlet>` タグと前の行を次の場所に置き換えます。

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

4. `web.xml`を保存して閉じます。

**目的：**&#x200B;これらの設定により、AEM FormsおよびDigital Asset Managementで大きなファイルのアップロード（最大1 GB）が可能になります。

### 手順6:WAR ファイルの再パッケージ

すべての設定変更を完了したら、WAR ファイルを再パッケージします。

1. 抽出したコンテンツを含む作業ディレクトリに戻ります。

   ```cmd
   cd C:\aem\war-config
   ```

2. 新しいWAR ファイルを作成します。

   ```cmd
   jar -cvf cq-quickstart.war *
   ```

>[!IMPORTANT]
>
> この手順は、すべての設定が完了した後に1回だけ実行します。

### 手順7:AEMのデプロイと起動

#### JBossへのWARのデプロイ

1. 再パッケージ化された`cq-quickstart.war`をJBoss デプロイメントディレクトリにコピーします。

   ```
   <JBOSS_HOME>\standalone\deployments
   ```

   **例：**
   `C:\jboss-eap-8.0\standalone\deployments`

#### JVM設定の設定（オプションですが推奨）

JBossを開始する前に、JVM メモリ設定を行います。

1. `<JBOSS_HOME>\bin\standalone.conf.bat`をテキストエディターで開きます。

1. 次の行を変更または追加して、ヒープメモリを設定します。

   ```batch
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=512m"
   ```

>[!NOTE]
>
> サーバーのキャパシティとAEMの要件に基づいて、メモリ値を調整します。

1. ファイルを保存して閉じます。

#### JBoss EAPの開始

1. **コマンドプロンプト**&#x200B;を&#x200B;**管理者**&#x200B;として開きます。

1. JBoss bin ディレクトリに移動します。

   ```cmd
   cd <JBOSS_HOME>\bin
   ```

   **例：**
   `cmd cd C:\jboss-eap-8.0\bin`

1. JBoss サーバーを起動します。

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

   **パラメーター：**
   * `-b 0.0.0.0` — サーバーをすべてのネットワークインターフェイスにバインドします
   * `-bmanagement 0.0.0.0` – 管理インターフェイスをすべてのネットワークインターフェイスにバインドします

#### 展開の監視

デプロイメントメッセージのコンソール出力を確認します。 デプロイメントが成功した場合は、次のように表示されます。

```
Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
```

### 手順8:AEMへのアクセス

デプロイメントが完了し、AEMが完全に開始されたら、次の手順を実行します。

**AEM オーサーURL:**
`http://<server-ip>:8080/cq-quickstart`

**既定の資格情報：**

* ユーザー名：`admin`
* パスワード：`admin`

**重要：**&#x200B;最初のログイン直後にデフォルトのパスワードを変更します。

### トラブルシューティング

#### よくある問題

| 問題 | 解決策 |
|-------|----------|
| ClassNotFoundExceptionでデプロイメントが失敗する | `jboss-deployment-structure.xml`が正しく設定されていることを確認します |
| 起動時のOutOfMemoryError | `standalone.conf.bat`のヒープメモリを増やす |
| デプロイメント後にAEMが起動しない | `<JBOSS_HOME>\standalone\log\server.log`のJBoss ログを確認する |
| ブラウザーでAEMにアクセスできない | ファイアウォール設定でポート 8080が許可されていることを確認する |

#### ログファイル

* **JBoss サーバーログ：** `<JBOSS_HOME>\standalone\log\server.log`
* **AEM エラーログ：**&#x200B;起動後にAEM Web コンソールで利用できます\
  `http://<server-ip>:8080/cq-quickstart/system/console`

### その他の設定

#### 実行モードの設定

AEM実行モード（オーサー/パブリッシュ）を変更するには、WARを再パッケージ化する前に、`WEB-INF\web.xml`の`sling.run.modes` パラメーターを変更します。

```xml
<init-param>
    <param-name>sling.run.modes</param-name>
    <param-value>publish</param-value>
</init-param>
```

#### 本番に関する推奨事項

実稼動環境用：

* JBossでのSSL/TLS証明書の設定
* AEM レプリケーションエージェントの設定
* 負荷分散のDispatcherの設定
* 自動バックアップを有効にする
* 監視とアラートの実装

### 関連ドキュメント

* [JBoss EAP 8 ドキュメント](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0)
* [Adobe Experience Manager Documentation](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ja)
* [AEM インストールおよびデプロイメントガイド](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=ja)

### ドキュメント情報

| フィールド | 値 |
|-------|-------|
| 最終更新日 | 2026年2月 |
| AEM のバージョン | 6.5以上（LTS） |
| JBoss バージョン | EAP 8.x |
| JDK バージョン | 21 |
| プラットフォーム | Windows |


