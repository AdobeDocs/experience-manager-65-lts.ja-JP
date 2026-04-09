---
title: JBoss EAP 8でのAEM 6.5 LTSのアップグレード（Windows）
description: このガイドでは、JDK 21を使用して、既存のAdobe Experience Manager（AEM） 6.5 LTS インストールをJBoss EAP 7.4からWindows上のJBoss EAP 8にアップグレードする手順を説明します。
source-git-commit: 835530039678bc16a6de87b8d580be91a2026f94
workflow-type: tm+mt
source-wordcount: '1374'
ht-degree: 4%

---

# JBoss EAP 8でのAEM 6.5 LTSのアップグレード（Windows）

## 概要

このガイドでは、JDK 21を使用して、既存のAdobe Experience Manager（AEM） 6.5 LTS インストールをJBoss EAP 7.4からWindows上のJBoss EAP 8にアップグレードする手順を説明します。

**アップグレードパス：** JBoss EAP 7.4 （JDK 11）→ JBoss EAP 8 （JDK 21）

## 重要な注意点

>[!NOTE]
>
>これは重要なアップグレード手順です。 このアップグレードは、必ず実稼動以外の環境で実行し、完全なバックアップを維持してください。
>
> **&#x200B; 前提条件：**&#x200B;続行する前に、完全なシステムバックアップと文書化されたロールバックプランが必須です。

## アップグレード前の要件

### システム要件

| コンポーネント | 要件 |
|-----------|-------------|
| オペレーティングシステム | Windows Server 2016以降（64 ビット） |
| Source環境 | JBoss EAP 7.4 （AEM 6.5 LTS搭載） |
| ターゲット環境 | JBoss EAP 8.x |
| Java開発キット | JDK 21 （OracleまたはOpenJDK） |
| AEM のバージョン | AEM 6.5 サービスパック（最新版をお勧めします） |
| ディスク容量 | アップグレードプロセス用の最小50 GBの空き容量 |

### 必要なダウンロード

アップグレードを開始する前に、次の情報を入手してください。

1. **JBoss EAP 8.0 ディストリビューション**\
   ダウンロード元：[https://developers.redhat.com/products/eap/download](https://developers.redhat.com/products/eap/download)

2. **JDK 21 インストーラー**\
   Windows （64 ビット版）用Oracle JDK 21またはOpenJDK 21をダウンロード

3. **AEM 6.5 LTS WAR ファイル**\
   Adobe Software Distributionから最新のAEM 6.5 Service Pack WARを入手する

## ステップ 1：完全なバックアップを作成する

>[!IMPORTANT]
>
> 続行する前に、包括的なバックアップを実行します。

### バックアップチェックリスト

- [ ]既存のJBoss EAP 7.4 インストールディレクトリの完全バックアップ
- [ ] フォルダーの`crx-repository` バックアップ
- [ ] フォルダーの`crx-quickstart` バックアップ
- [ すべてのカスタム設定の]書き出し
- [ ] データベースのバックアップ （外部データベースを使用している場合）
- [ ]現在のシステムの状態と設定を文書化します

### バックアップを作成

```cmd
# Example backup location
C:\AEM-Backups\Pre-Upgrade-<date>

# Copy entire JBoss 7.4 directory
xcopy "C:\jboss-eap-7.4" "C:\AEM-Backups\Pre-Upgrade-<date>\jboss-eap-7.4" /E /I /H
```

**推奨：** バックアップを別のドライブまたはネットワークの場所に保存します。

## 手順2:JBoss EAP 8のインストール

### JBoss EAP 8の抽出

1. JBoss EAP 8 ZIP ディストリビューションをターゲットインストールディレクトリに抽出します。

   ```
   C:\jboss-eap-8.0
   ```

2. このガイド全体で使用するディレクトリパスは`<JBOSS_HOME>`として注意してください。

### ディレクトリ構造のレプリケート

新しいJBoss EAP 8のインストールが、以前のJBoss EAP 7.4のセットアップと同じカスタムディレクトリ構造を持っていることを確認します。特に次の点が重要です。

- カスタムデプロイメントディレクトリ
- 外部設定フォルダー
- ログファイルの場所
- カスタムモジュールやライブラリ

## 手順3：リポジトリデータの移行

### CRX リポジトリをコピー

1. 既存のJBoss EAP 7.4 インストールに移動します。

   ```
   <OLD_JBOSS_HOME>\bin\crx-repository
   ```

2. `crx-repository` フォルダー全体を新しいJBoss EAP 8 インストールにコピーします。

   ```cmd
   xcopy "C:\jboss-eap-7.4\bin\crx-repository" "C:\jboss-eap-8.0\bin\crx-repository" /E /I /H
   ```

**重要：**&#x200B;このフォルダーにはコンテンツリポジトリが含まれており、完全に転送する必要があります。

### リポジトリコピーの検証

コピー後、リポジトリのサイズと構造がソースに一致することを確認します。

```cmd
dir "C:\jboss-eap-8.0\bin\crx-repository" /s
```

## 手順4:AEM インスタンスの停止

変更を加える前に、AEMが完全に停止されていることを確認します。

### Windows サービスで停止

1. **サービス**&#x200B;を開きます（実行：`services.msc`）
2. AEM/JBoss サービスを探す
3. 右クリックして、**停止**&#x200B;を選択します
4. サービスが完全に停止するのを待ちます

### コマンドラインで停止

AEMを手動で起動した場合：

1. JBoss コンソールウィンドウに移動
2. `Ctrl+C`を押す
3. 正常なシャットダウンが完了するのを待ちます

### シャットダウンを確認

Java プロセスが実行されていないことを確認します。

```cmd
tasklist | findstr java
```

## 手順5：従来のAEM ファイルのクリーンアップ

古いファイルを`crx-quickstart` ディレクトリから削除して、クリーンなアップグレードを確実に行います。

>[!CAUTION]
>
> 以下に示す特定のファイルとフォルダーのみを削除します。 他の設定ファイル、カスタムコード、リポジトリデータは削除しないでください。

### 5.1 Launchpad起動フォルダーの削除

**場所：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\startup
```

**アクション：**

```cmd
rd /s /q "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\startup"
```

**目的：**&#x200B;このフォルダーには、アップグレード時に再生成される古いOSGi バンドルが含まれています。

### 5.2 ベース JAR ファイルの削除

**場所：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar
```

**アクション：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\org.apache.sling.launchpad.base.jar"
```

**目的：**&#x200B;このJARは、新しいWAR ファイルのバージョンに置き換えられます。

### 5.3 Bootstrap コマンドファイルの削除

**場所：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt
```

**アクション：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\bundle0\BootstrapCommandFile_*.txt"
```

**目的：** Bootstrap コマンドが新しい環境に対して再生成されます。

### 5.4 sling.options ファイルの削除

**場所：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file
```

**アクション：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\felix\sling.options.file"
```

### 5.5 sling_bootstrap.txt ファイルの削除

**場所：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt
```

**アクション：**

```cmd
del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\launchpad\sling_bootstrap.txt"
```

### 5.6 sling.properties ファイルのバックアップと削除

このファイルには、後で結合する必要がある環境固有の設定が含まれています。

**場所：**

```
<JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
```

**アクション：**

1. **バックアップの作成：**

   ```cmd
   copy "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties" "C:\AEM-Backups\sling.properties.backup"
   ```

2. **オリジナルを削除：**

   ```cmd
   del "C:\jboss-eap-8.0\bin\crx-repository\crx-quickstart\conf\sling.properties"
   ```

**目的：**&#x200B;新しい`sling.properties`が生成されます。 アップグレード後にカスタム設定を復元するには、バックアップを確認します。

## 手順6:JDK 21のインストールと設定

### JDK 21のインストール

1. Windows用JDK 21 インストーラーの実行
2. 標準の場所（例：`C:\Program Files\Java\jdk-21`）にインストール
3. インストールウィザードを完了します

### 環境変数の設定

#### Java_HOMEを設定

1. **システムのプロパティ** → **詳細** → **環境変数**&#x200B;を開きます
2. **システム変数**&#x200B;で、**新規**&#x200B;をクリックします
3. 次のように設定します。
   - 変数名：`JAVA_HOME`
   - 変数値：`C:\Program Files\Java\jdk-21`
4. **OK**&#x200B;をクリック

#### パス変数を更新

1. **システム変数**&#x200B;で、`Path`を選択し、**編集**&#x200B;をクリックします
2. 新しいエントリを追加：

   ```
   %JAVA_HOME%\bin
   ```

3. このエントリをリストの先頭に移動して、JDK 21が優先されるようにします
4. すべてのダイアログで「**OK**」をクリックします

### Java インストールの確認

1. **new** コマンドプロンプトを開きます（更新された環境変数を読み込むには）
2. Java バージョンの確認：

   ```cmd
   java -version
   ```

   予想される出力：

   ```
   java version "21.0.x"
   Java(TM) SE Runtime Environment (build 21.0.x+...)
   Java HotSpot(TM) 64-Bit Server VM (build 21.0.x+..., mixed mode, sharing)
   ```

3. Java_HOMEを確認します。

   ```cmd
   echo %JAVA_HOME%
   ```

## 手順7:JVM設定の設定

AEMをデプロイする前に、実稼動用に適切なJVM メモリ設定を行います。

### standalone.conf.batの編集

1. 次の URL に移動します。

   ```
   <JBOSS_HOME>\bin
   ```

2. `standalone.conf.bat`をテキストエディターで開く（管理者として）

3. `JAVA_OPTS`設定を見つけるか追加します。

   ```batch
   rem # AEM Production JVM Settings
   set "JAVA_OPTS=-Xms4096m -Xmx4096m -XX:MaxMetaspaceSize=768m"
   set "JAVA_OPTS=%JAVA_OPTS% -Djava.net.preferIPv4Stack=true"
   set "JAVA_OPTS=%JAVA_OPTS% -Dfile.encoding=UTF-8"
   set "JAVA_OPTS=%JAVA_OPTS% -server"
   ```

4. ファイルを保存して閉じる

**おすすめの設定：**

| パラメーター | 推奨値 | 説明 |
|-----------|-------------------|-------------|
| `-Xms` | 4096m - 8192m | 初期ヒープサイズ |
| `-Xmx` | 4096m - 8192m | 最大ヒープサイズ |
| `-XX:MaxMetaspaceSize` | 768m - 1024m | メタスペースの制限 |

**メモ：** サーバーの使用可能なメモリとワークロードの要件に基づいて値を調整します。

## ステップ 8:AEM 6.5 LTS WARをデプロイする

### WAR ファイルの準備

AEM WAR ファイルがデプロイメントガイドに従って適切に設定されていることを確認します。

- `jboss-deployment-structure.xml`さんがいます
- `web.xml`にはマルチパート設定が含まれています
- WARは、変更が加えられると再び使用されます

### JBossへのデプロイ

1. AEM 6.5 LTS WAR ファイルをデプロイメントディレクトリにコピーします。

   ```cmd
   copy "C:\AEM-Downloads\cq-quickstart-6.5.xx.war" "C:\jboss-eap-8.0\standalone\deployments\cq-quickstart.war"
   ```

**重要：** WAR ファイル名が目的のURL コンテキストパスと一致することを確認します。

## 手順9:AEMでJBoss EAP 8を開始する

### サーバーの起動

1. **コマンドプロンプト**&#x200B;を&#x200B;**管理者**&#x200B;として開く

2. JBoss bin ディレクトリに移動します。

   ```cmd
   cd C:\jboss-eap-8.0\bin
   ```

3. JBoss EAP 8を開始：

   ```cmd
   standalone.bat -b 0.0.0.0 -bmanagement 0.0.0.0
   ```

### 初期起動の監視

以下のコンソール出力を確認します。

1. **戦争展開：**

   ```
   Deployed "cq-quickstart.war" (runtime-name : "cq-quickstart.war")
   ```

2. **AEMの初期化メッセージ：**

   ```
   Apache Sling Application Launcher
   Sling Home: crx-repository/crx-quickstart
   ```

3. **リポジトリのアップグレード （該当する場合）:**

   ```
   Performing repository migration...
   ```

**予想される起動時間：** リポジトリのサイズとシステム リソースに応じて5 ～ 15分

## 手順10: アップグレードの成功を検証する

### AEMの起動を確認

最後の起動メッセージのJBoss コンソールを監視します。

```
**** AEM started successfully ****
```

### AEMのインターフェイスにアクセス

1. Web ブラウザーを開く
2. 次の URL に移動します。

   ```
   http://localhost:8080/cq-quickstart
   ```

3. 管理者の資格情報でログインします。
   - ユーザー名：`admin`
   - パスワード：`admin` （またはカスタムパスワード）

### システム情報の検証

1. **ツール** → **操作** → **Web コンソール**&#x200B;に移動します

   ```
   http://localhost:8080/cq-quickstart/system/console
   ```

2. **システム情報**&#x200B;をクリックします

3. 検証：

   - **JVM バージョン：**&#x200B;ではJava 21が表示されます
   - **JBoss バージョン：**&#x200B;ではEAP 8.xが表示されます
   - **AEM バージョン：**&#x200B;では6.5.xxが表示されます

### システムの正常性の確認

**ツール** → **操作** → **診断**&#x200B;に移動して、ヘルスチェックを実行します。

- バンドルステータス：すべてのバンドルは「アクティブ」である必要があります
- リソース解決：正常なステータスを表示する必要があります
- クエリのパフォーマンス：低下がないか確認してください

## アップグレード後のタスク

### カスタム設定の復元

1. バックアップされた`sling.properties` ファイルを確認します
2. カスタム実行モードまたは設定を新しいファイルに復元します。

   ```
   <JBOSS_HOME>\bin\crx-repository\crx-quickstart\conf\sling.properties
   ```

3. 設定が変更された場合は、AEMを再起動します

### レプリケーションエージェントの更新

1. 作成者&#x200B;**の** ツール **→** デプロイメント **→** レプリケーション **→** エージェントに移動します
2. すべてのレプリケーションエージェントのレビューとテスト
3. 古いサーバーパスへのハードコードされた参照を更新する

### クリティカル機能のテスト

- [ ] コンテンツのオーサリングと公開
- [ ] アセットのアップロードと処理
- [ ] ワークフロー実行
- [ ] ユーザー認証
- [ ]統合エンドポイント
- [ ] カスタムコンポーネントとテンプレート

### パフォーマンスの最適化

1. 一時的なキャッシュを確認してクリアする
2. 初回使用時のシステムパフォーマンスの監視
3. 実際の使用パターンに基づいて、必要に応じてJVM設定を調整します

## トラブルシューティング

### よくある問題

| 問題 | 考えられる原因 | 解決策 |
|-------|---------------|----------|
| AEMを開始できません | 正しくないJava バージョン | `JAVA_HOME` ポイントをJDK 21に確認 |
| リポジトリの破損エラー | 不完全なリポジトリコピー | バックアップからの復元とリポジトリの再コピー |
| OutOfMemoryError | ヒープメモリが不十分 | `-Xmx`の`standalone.conf.bat`を増やす |
| 「インストール済み」状態のバンドル | 依存関係がありません | Web コンソールでバンドルの依存関係を確認する |
| ポート 8080は既に使用されています | ポートを使用する別のサービス | 競合するサービスを停止するか、JBoss ポートを変更します |

### ログファイルの場所

- **JBoss サーバーログ：**\
  `<JBOSS_HOME>\standalone\log\server.log`

- **AEM エラーログ：**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\error.log`

- **AEM アクセス ログ：**\
  `<JBOSS_HOME>\bin\crx-repository\crx-quickstart\logs\access.log`

### ロールバック手順

アップグレードが失敗して解決できない場合：

1. JBoss EAP 8を停止
2. JBoss EAP 7.4の完全なバックアップを復元する
3. `crx-repository` フォルダーを復元
4. `JAVA_HOME` ポイントをJDK 11に確認します（ロールバックする場合）
5. 前の環境を開始

## ベストプラクティス

### 実稼動デプロイメントの前

- [ ]開発環境で完全なアップグレードプロセスをテストする
- [ 実稼動環境のようなデータを使用したステージング環境での] テスト
- [ ]すべてのカスタム設定と統合のドキュメント化
- [ ]詳細なロールバック計画の作成
- [ メンテナンスウィンドウ中に] スケジュールのアップグレード
- [ ]計画されたダウンタイムをすべての関係者に通知

### アップグレードが成功した後

- [ ] 48 ～ 72時間システムログを監視する
- [ ] パフォーマンスの問題を特定するために負荷テストを実行します
- [ ] システムドキュメントを更新
- [ ] JBoss EAP 8の違いに関するチームのトレーニング
- [ ]すべてのアップグレードドキュメントとバックアップをアーカイブ

## 関連ドキュメント

- [JBoss EAP 8移行ガイド &#x200B;](https://access.redhat.com/documentation/en-us/red_hat_jboss_enterprise_application_platform/8.0/html/migration_guide/)
- [Adobe Experience Manager 6.5 アップグレードガイド &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html?lang=ja)
- [AEM サービスパックのインストール &#x200B;](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/service-pack/sp-release-notes.html?lang=ja)

## ドキュメント情報

| フィールド | 値 |
|-------|-------|
| ドキュメントのバージョン | 1.0 |
| 最終更新日 | 2026年2月 |
| AEM のバージョン | 6.5 LTS |
| Source Platform | JBoss EAP 7.4 / JDK 11 |
| Target Platform | JBoss EAP 8.x / JDK 21 |
| オペレーティングシステム | Windows Server |

**法的通知：** Adobe、Adobe Experience Manager、およびAEMはAdobe Inc.の登録商標です。JBossおよびRed HatはRed Hat, Inc.の登録商標です。
