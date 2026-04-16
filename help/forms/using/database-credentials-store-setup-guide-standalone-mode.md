---
title: データベース資格情報ストア設定ガイド （スタンドアロンモード）
description: JBoss/Red Hat EAP上のAEM Forms JEEのデータベース資格情報ストア設定をスタンドアロンモードで検索します。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: f6e29287-a558-43ad-8465-ebf167c79c63
source-git-commit: b4abf61e0d30396e78ecebf228114ad2bde30633
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 2%

---

# データベース資格情報ストア設定ガイド （スタンドアロンモード）

## 概要

このガイドでは、**スタンドアロンモード**&#x200B;でのJBoss/Red Hat EAP上のAEM Forms JEEの&#x200B;**データベース資格情報ストア設定**&#x200B;について説明します。 これは、手動インストールを実行する場合に必要です。


**このガイドの内容：**

- データベース資格情報ストアを作成しています（`cred-store.p12`）
- データベースのパスワードエイリアスを安全に追加する
- 資格情報ストアを使用するためのJBossの設定

**重要：**&#x200B;これらのスクリプトは&#x200B;**オフラインモードでのみ動作します**。 これらのスクリプトを実行する前に、JBossを停止する必要があります。 スクリプトは`embed-server` モードを使用しています。このモードでは、サーバーを停止する必要があります。

**注：**&#x200B;これは&#x200B;**not**&#x200B;完全なスタンドアロン インストール ガイドです。 このドキュメントでは、次の条件を満たしていることを前提としています。

- JBossはすでにインストールされています
- スタンドアロン設定ファイル （`lc_oracle.xml`、`lc_mysql.xml`または`lc_mssql.xml`）は既に設定されています
- データベースが設定され、アクセス可能である

完全なスタンドアロンインストール手順が必要な場合は、メインインストールガイドを参照してください。

## 前提条件

これらのスクリプトを実行する前に、次のことを確認してください。

1. **JBossを停止する必要があります**
   - これらのスクリプトは&#x200B;**オフラインモードでのみ機能します**
   - スクリプトは`embed-server`を使用しています。サーバーを停止する必要があります
   - JBossが実行されている場合、スクリプトは失敗します
   - JBossが実行されているかどうかを確認します。
      - Windows: `java.exe` プロセスのタスク マネージャーを確認してください
      - Linux: `ps aux | grep jboss`または`ps aux | grep java`
   - 実行中の場合はJBossを停止します。
      - JBossが実行されているターミナルで`Ctrl+C`を押します
      - あるいは手作業でプロセスを終了させたり

2. **データベースのパスワードを準備しました**

3. **資格情報ストアの安全なパスワードが決定されました**

4. **使用しているデータベース設定ファイル：**
   - `lc_oracle.xml` （Oracle データベースの場合）
   - `lc_mysql.xml` （MySQL データベースの場合）
   - `lc_mssql.xml` （Microsoft SQL Server データベースの場合）

## 手順の設定

### 手順1：データベース資格情報ストアの作成

提供されたスクリプトを使用して、データベース資格情報ストアを作成し、必要なすべてのパスワードエイリアスを追加します。

#### Windowsの場合

**スクリプト：** `create-elytron-cred-standalone.bat`

`create-elytron-cred-standalone.bat` ソフトウェア配布ポータル [から](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/full-installer/6-6-0-20251218-2-12345/6.5.1.LTS_Scripts.zip) スクリプトをダウンロードします。

**次のプロンプトが表示されます：**
1. **JBOSS_HOME パス** （例：`C:\Adobe\Adobe_Experience_Manager_Forms\jboss`）
2. **設定ファイル名** （例：`lc_oracle.xml`、`lc_mysql.xml`、または`lc_mssql.xml`）
3. **資格情報ストアのパスワード** （これにより、キーストアファイルが保護されます。このパスワードを記憶してください）
4. **データベース パスワード** （実際のデータベース パスワード）

**スクリプトの機能：**

- 次の場所に資格情報ストアを作成します：`JBOSS_HOME\standalone\configuration\cred-store.p12`
- 設定ファイルを一時的に変更して、資格情報ストアの作成を有効にします
- データベースのパスワードに次のエイリアスを追加します。
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- 設定ファイルを元の状態に戻します
- すべてのエイリアスが正常に追加されたことを確認します

#### Linuxでは：

**スクリプト** `create-elytron-cred-standalone.sh`

`create-elytron-cred-standalone.sh` ソフトウェア配布ポータル [から](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/fd/full-installer/6-6-0-20251218-2-12345/6.5.1.LTS_Scripts.zip) スクリプトをダウンロードします。

**次のプロンプトが表示されます：**

1. **JBOSS_HOME パス** （例：`/opt/Adobe/Adobe_Experience_Manager_Forms/jboss`）
2. **設定ファイル名** （例：`lc_oracle.xml`、`lc_mysql.xml`、または`lc_mssql.xml`）
3. **資格情報ストアのパスワード** （これにより、キーストアファイルが保護されます。このパスワードを記憶してください）
4. **データベース パスワード** （実際のデータベース パスワード）

**スクリプトの機能：**

- 次の場所に資格情報ストアを作成します：`JBOSS_HOME/standalone/configuration/cred-store.p12`
- 設定ファイルを一時的に変更して、資格情報ストアの作成を有効にします
- データベースのパスワードに次のエイリアスを追加します。
   - `EncryptDBPassword`
   - `EncryptDBPassword_IDP_DS`
   - `EncryptDBPassword_EDC_DS`
   - `EncryptDBPassword_AEM_DS`
- 設定ファイルを元の状態に戻します
- すべてのエイリアスが正常に追加されたことを確認します

**予想される出力：**

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

### 手順2：スタンドアロン設定ファイルの更新

スクリプトを実行した後、起動時に資格情報ストアのパスワードを読み取るようにJBossを設定する必要があります。

#### Windowsの場合

**ファイルの場所：** `<JBOSS_HOME>\bin\standalone.conf.bat`

例：`C:\Adobe\Adobe_Experience_Manager_Forms\jboss\bin\standalone.conf.bat`

次の行を追加または更新します。

```batch
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourActualPassword123"
```

`YourActualPassword123`を、手順1で使用した&#x200B;**資格情報ストアのパスワード**&#x200B;に置き換えます。

#### Linuxでは：

**ファイルの場所：** `<JBOSS_HOME>/bin/standalone.conf`

例：`/opt/Adobe/Adobe_Experience_Manager_Forms/jboss/bin/standalone.conf`

次の行を追加または更新します。

```bash
JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourActualPassword123"
```

`YourActualPassword123`を、手順1で使用した&#x200B;**資格情報ストアのパスワード**&#x200B;に置き換えます。

### 手順3:JBossの開始

資格情報ストアの設定が完了したら、適切な設定ファイルを使用してJBossを起動します。

**メモ：** JBossをスタンドアロン モードで起動するための正確な起動コマンドと手順については、**メインインストールガイド**&#x200B;を参照してください。 起動コマンドは、特定の設定とデータベースの種類（`lc_oracle.xml`、`lc_mysql.xml`または`lc_mssql.xml`）によって異なる場合があります。

## 検証

### サーバーログの確認

**ログの場所：**

- Windows：`<JBOSS_HOME>\standalone\log\server.log`
- Linux: `<JBOSS_HOME>/standalone/log/server.log`

**成功したスタートアップ メッセージを探します：**

```
INFO  [org.jboss.as.server] WFLYSRV0025: JBoss EAP started
INFO  [org.jboss.as.connector.deployers.jdbc] Bound data source [java:/AdobeDataSource]
```

**次に関連するエラーはありません：**

- 資格情報ストアの読み込み
- データベース接続
- エイリアスがありません

## トラブルシューティング

### 問題1：資格情報ストアが見つかりません

**エラーメッセージ：**

```
ERROR Unable to load credential store
```

**解決策：**

1. 資格情報ストアファイルが存在することを確認します。
   - Windows：`dir <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux: `ls -l <JBOSS_HOME>/standalone/configuration/cred-store.p12`
2. 見つからない場合は、資格情報ストア作成スクリプトを再実行します（手順1）

### 問題2：資格情報ストアのパスワードが間違っている

**エラーメッセージ：**

```
ERROR Unable to load credential store - Invalid password
```

**解決策：**
`standalone.conf.bat` / `standalone.conf`のパスワード（手順2）が、資格情報ストアの作成時に使用されたパスワード（手順1）と一致することを確認します。

**修正：**
`standalone.conf.bat` / `standalone.conf`を編集し、パスワードを更新します。

```
set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=CorrectPassword"
```

### 問題3: データベース接続に失敗しました

**エラーメッセージ：**

```
ERROR Failed to obtain connection
```

**解決策：**

1. 資格情報ストアで使用されるデータベースのパスワードが正しいことを確認します
2. データソース設定が正しいエイリアスを参照していることを確認します
3. データベース・サーバへのネットワーク接続の確認

**資格情報ストアを再作成するには：**

1. JBossを停止
2. 既存の資格情報ストアを削除します。
   - Windows：`del <JBOSS_HOME>\standalone\configuration\cred-store.p12`
   - Linux: `rm <JBOSS_HOME>/standalone/configuration/cred-store.p12`
3. 正しいデータベースパスワードで資格情報ストア作成スクリプトを再実行します

### 問題4：実行中にスクリプトが失敗する

**エラーメッセージ：**

```
ERROR: jboss-cli.bat is not found
```

**解決策：**
JBOSS_HOME パスが正しく、JBoss インストールディレクトリを指していることを確認します。

**エラーメッセージ：**

```
ERROR: Configuration file not found
```

**解決策：**

1. 設定ファイル名が正しいことを確認します
2. ファイルが`JBOSS_HOME\standalone\configuration\` ディレクトリにあることを確認してください
3. 適切なデータベース固有の設定ファイルを使用していることを確認してください

## クイックリファレンス

### データベース資格情報ストア （スタンドアロンモード）

**目的：** データベース パスワードを安全に保存する

**スクリプト：**

- Windows：`create-elytron-cred-standalone.bat`
- Linux: `create-elytron-cred-standalone.sh`

**作成回数：**

- ファイル：`standalone/configuration/cred-store.p12`
- エイリアス：`EncryptDBPassword`、`EncryptDBPassword_IDP_DS`、`EncryptDBPassword_EDC_DS`、`EncryptDBPassword_AEM_DS`

**設定：**

- 変数：`-DCS_PASS=password`
- ファイル：`standalone.conf.bat` （Windows）または`standalone.conf` （Linux）
