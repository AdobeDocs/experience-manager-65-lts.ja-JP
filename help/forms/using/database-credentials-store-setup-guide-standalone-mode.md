---
title: データベース資格情報ストア設定ガイド （スタンドアロンモード）
description: スタンドアロンモードの JBoss/Red Hat EAP でのAEM Forms JEE 用のデータベース資格情報ストアの設定を確認します。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 2%

---


# データベース資格情報ストア設定ガイド （スタンドアロンモード）

## 概要

このガイドでは、JBoss/Red Hat EAP 上のAEM Forms JEE の **データベース資格情報ストアの設定** スタンドアロンモード **について説明** ます。 これは、手動インストールを実行する場合に必要です。

**このガイドの内容は次のとおりです。**

- データベース資格情報ストア （`cred-store.p12`）を作成しています
- データベース・パスワードの別名の安全な追加
- 資格情報ストアを使用するための JBoss の設定

**重要：** これらのスクリプトは **オフラインモードのみ** で動作します。 これらのスクリプトを実行するには、JBoss を停止する必要があります。 スクリプトでは、サーバー `embed-server` 停止する必要があるモードを使用します。

**注意：** これは完全なスタンドアロン インストール ガイド **ありません**。 このドキュメントでは、次のことを前提としています。

- JBoss はすでにインストールされています
- スタンドアロン構成ファイル （`lc_oracle.xml`、`lc_mysql.xml`、または `lc_mssql.xml`）は既に構成されています
- データベースが設定され、アクセス可能です

完全なスタンドアロン インストール手順が必要な場合は、メインのインストール ガイドを参照してください。

## 前提条件

これらのスクリプトを実行する前に、以下を確認します。

1. **JBoss を停止する必要があります**
   - これらのスクリプトは **オフラインモードのみ** で動作します
   - スクリプトでは、サーバーの停止を必要とする `embed-server` を使用します
   - JBoss が実行中の場合、スクリプトは失敗します
   - JBoss が実行中かどうかを確認します。
      - Windows:`java.exe` プロセスのタスクマネージャーを確認する
      - Linux:`ps aux | grep jboss` または `ps aux | grep java`
   - 以下を実行している場合は JBoss を停止します。
      - JBoss が実行されているターミナルで `Ctrl+C` を押します
      - または、プロセスを手動で強制終了します

2. **データベースのパスワードの準備が完了しました**

3. **資格情報ストアのセキュリティで保護されたパスワードを決定しました**

4. **使用しているデータベース構成ファイルがわかります。**
   - `lc_oracle.xml` （Oracle データベースの場合）
   - `lc_mysql.xml` （MySQL データベースの場合）
   - `lc_mssql.xml` （Microsoft SQL Server データベースの場合）

## 設定手順

### 手順 1：データベース資格情報ストアの作成

提供されたスクリプトを使用して、データベース資格情報ストアを作成し、必要なすべてのパスワードエイリアスを追加します。

#### Windows:

**スクリプトの場所：** `create-elytron-cred-standalone.bat`

`batch cd path\to\script\location create-elytron-cred-standalone.bat`

**スクリプトにより、次のプロンプトが表示されます。**
1. **JBOSS_HOME パス** （例：`C:\Adobe\Adobe_Experience_Manager_Forms\jboss`）
2. **設定ファイル名** （例：`lc_oracle.xml`、`lc_mysql.xml`、`lc_mssql.xml`）
3. **資格情報ストアのパスワード** （キーストアファイルを保護します – このパスワードを保存します）
4. **データベースパスワード** （実際のデータベースパスワード）

**スクリプトの機能：**

- `JBOSS_HOME\standalone\configuration\cred-store.p12` に資格情報ストアを作成します
- 構成ファイルを一時的に変更して、資格情報ストアの作成を有効にします
- データベース・パスワードとともに次の別名を追加します：
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- 構成ファイルを元の状態に復元します
- すべてのエイリアスが正常に追加されたことを確認します

#### Linux:

**スクリプトの場所：** `create-elytron-cred-standalone.sh`

`bash cd /path/to/script/location chmod +x create-elytron-cred-standalone.sh./create-elytron-cred-standalone.sh`

**スクリプトにより、次のプロンプトが表示されます。**

1. **JBOSS_HOME パス** （例：`/opt/Adobe/Adobe_Experience_Manager_Forms/jboss`）
2. **設定ファイル名** （例：`lc_oracle.xml`、`lc_mysql.xml`、`lc_mssql.xml`）
3. **資格情報ストアのパスワード** （キーストアファイルを保護します – このパスワードを保存します）
4. **データベースパスワード** （実際のデータベースパスワード）

**スクリプトの機能：**

- `JBOSS_HOME/standalone/configuration/cred-store.p12` に資格情報ストアを作成します
- 構成ファイルを一時的に変更して、資格情報ストアの作成を有効にします
- データベース・パスワードとともに次の別名を追加します：
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- 構成ファイルを元の状態に復元します
- すべてのエイリアスが正常に追加されたことを確認します

**期待される出力：**

```
=== JBoss Elytron Credential Store Setup ===
Enter JBOSS_HOME path (e.g. /opt/jboss): /opt/Adobe/Adobe_Experience_Manager_Forms/jboss
Enter configuration file name (e.g. lc_oracle.xml): lc_oracle.xml
Enter credential store password: ********
Confirm credential store password: ********
Enter database password: ********
Creating credential store using JBoss CLI...
Adding aliases to credential store...
Verifying credential store aliases...

All 4 aliases verified successfully!
- EncryptDBPassword
- EncryptDBPassword_IDP_DS
- EncryptDBPassword_EDC_DS
- EncryptDBPassword_AEM_DS

Credential store setup completed successfully!
```

### 手順 2：スタンドアロン設定ファイルの更新

スクリプトの実行後、起動時に資格情報ストアパスワードを読み取るように JBoss を設定する必要があります。

#### Windows:

**ファイルの場所：** `<JBOSS_HOME>\bin\standalone.conf.bat`

例：`C:\Adobe\Adobe_Experience_Manager_Forms\jboss\bin\standalone.conf.bat`

次の行を追加または更新します。

```batch
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourActualPassword123"
```

`YourActualPassword123` を、手順 1 で使用した **資格情報ストアのパスワード** に置き換えます。

#### Linux:

**ファイルの場所：** `<JBOSS_HOME>/bin/standalone.conf`

例：`/opt/Adobe/Adobe_Experience_Manager_Forms/jboss/bin/standalone.conf`

次の行を追加または更新します。

```bash
JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourActualPassword123"
```

`YourActualPassword123` を、手順 1 で使用した **資格情報ストアのパスワード** に置き換えます。

### 手順 3:JBoss の開始

資格情報ストアのセットアップが完了したら、適切な設定ファイルを使用して JBoss を起動します。

**注意：** スタンドアロンモードで JBoss を起動するための正確な起動コマンドと手順については、**メインインストールガイド** を参照してください。 起動コマンドは、使用する設定やデータベースの種類（`lc_oracle.xml`、`lc_mysql.xml`、`lc_mssql.xml`）によって異なる場合があります。

## 検証

### サーバーログの確認

**ログの場所：**

- Windows：`<JBOSS_HOME>\standalone\log\server.log`
- Linux: `<JBOSS_HOME>/standalone/log/server.log`

**成功した起動メッセージを探します：**

```
INFO  [org.jboss.as.server] WFLYSRV0025: JBoss EAP started
INFO  [org.jboss.as.connector.deployers.jdbc] Bound data source [java:/AdobeDataSource]
```

**関連するエラーはありません：**

- 資格情報ストアの読み込み
- データベース接続
- エイリアスの欠落

## トラブルシューティング

### 問題 1：資格情報ストアが見つからない

**エラーメッセージ：**

```
ERROR Unable to load credential store
```

**解決策：**

1. 秘密鍵証明書ストアファイルが存在することを確認します。
   - Windows：`dir <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux: `ls -l <JBOSS_HOME>/standalone/configuration/cred-store.p12`
2. 見つからない場合は、資格情報ストア作成スクリプトを再実行します（手順 1）

### 問題 2：資格情報ストアのパスワードが間違っている

**エラーメッセージ：**

```
ERROR Unable to load credential store - Invalid password
```

**解決策：**
`standalone.conf.bat` / `standalone.conf` （手順 2）のパスワードが、資格情報ストアの作成（手順 1）時に使用したパスワードと一致することを確認します。

**修正方法：**
`standalone.conf.bat` / `standalone.conf` を編集し、パスワードを更新します。

```
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=CorrectPassword"
```

### 問題 3：データベース接続に失敗する

**エラーメッセージ：**

```
ERROR Failed to obtain connection
```

**解決策：**

1. 資格情報ストアで使用されているデータベース パスワードが正しいことを確認します
2. データソース設定で正しいエイリアスが参照されていることを確認します
3. データベースサーバーへのネットワーク接続の確認

**資格情報ストアを再作成するには：**

1. JBoss を停止
2. 既存の資格情報ストアの削除：
   - Windows：`del <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux: `rm <JBOSS_HOME>/standalone/configuration/cred-store.p12`
3. 資格情報ストア作成スクリプトを、正しいデータベースパスワードで再実行します。

### 問題 4：実行中にスクリプトが失敗する

**エラーメッセージ：**

```
ERROR: jboss-cli.bat is not found
```

**解決策：**
JBOSS_HOME のパスが正しく、JBoss のインストールディレクトリを指していることを確認します。

**エラーメッセージ：**

```
ERROR: Configuration file not found
```

**解決策：**

1. 設定ファイル名が正しいことを確認します
2. ファイルがディレクトリに存在すること `JBOSS_HOME\standalone\configuration\` 確認します
3. 正しいデータベース固有の設定ファイルを使用していることを確認します

## クイックリファレンス

### データベース資格情報ストア （スタンドアロン モード）

**目的：** データベースパスワードを安全に保存する

**スクリプト：**

- Windows：`create-elytron-cred-standalone.bat`
- Linux: `create-elytron-cred-standalone.sh`

**作成：**

- ファイル：`standalone/configuration/cred-store.p12`
- エイリアス：`EncryptDBPassword`、`EncryptDBPassword_IDP_DS`、`EncryptDBPassword_EDC_DS`、`EncryptDBPassword_AEM_DS`

**設定：**

- 変数：`-DCS_PASS=password`
- ファイル：`standalone.conf.bat` （Windows）または `standalone.conf` （Linux）

