---
title: セカンダリノード認証の設定（Elytron ベース）
description: JBoss EAP 8 では、Elytron を使用して、セカンダリノードの安全な通信とプライマリドメインコントローラーへの登録が可能になります。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: 259cb81eb9652405dc7270535cbf9deb996ad2ac
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 5%

---


# セカンダリノード認証の設定（Elytron ベース）

## Elytron を使用したセカンダリノード認証の設定

JBoss EAP 8 では、**Elytron** を使用して、クラスター化されたデプロイメントで **プライマリノードとセカンダリノード** 間の通信が認証されます。 この構成により、セカンダリ・ノードの安全な登録とプライマリ・ドメイン・コントローラとの通信が確保されます。

環境とセキュリティの要件に応じて、2 つの設定オプションを使用できます。

## 前提条件

* **という名前の`secondary`** 管理ユーザーを **プライマリノード** で作成する必要があります。
* この設定を実行します **セカンダリノードのみ**。
* クラスター内の **各セカンダリノード** に対して設定を繰り返します。
* **JBoss は、プライマリノードとセカンダリノードの両方で完全に停止する必要があります**。
* 資格情報ストアの操作はすべて **オフラインモード** で実行する必要があります。

JBoss が実行中の場合に停止するには：

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux/UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

## 設定オプションを選択

* **オプション 1：デフォルトの資格情報ストアを使用したクイックセットアップ**
下位環境やテストでの使用に推奨します。

* **オプション 2：カスタム資格情報ストアの設定**
実稼動環境およびセキュリティ保護された環境で推奨されます。

## オプション 1：デフォルトの資格情報ストアを使用したクイックセットアップ

**次に最適：** 開発、テスト、クイックセットアップシナリオ。

### 概要

* デフォルトの秘密鍵証明書ストアファイル（`cs_secondary_hc.p12`）が事前設定されています。
* 既定の資格情報ストアのパスワードは既に `domain.conf` に設定されています。
* 認証パスワードエイリアスのみを追加する必要があります。

### 設定手順

#### 手順 1：デフォルトの資格情報ストアの確認

デフォルトの資格情報格納ファイルが存在することを確認します。

* **Windows**

  ```
  <JBOSS_HOME>\domain\configuration\cs_secondary_hc.p12
  ```

* **Linux**

  ```
  <JBOSS_HOME>/domain/configuration/cs_secondary_hc.p12
  ```

ファイルが存在しない場合は、**オプション 2** を使用します。

#### 手順 2：認証パスワードエイリアスの追加

`<JBOSS_HOME>/bin` から次のコマンドを実行します。

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

> シークレットの値は、プライマリノードで `secondary` ユーザーを作成する際に使用されるパスワードと一致させる必要があります。

#### 手順 3:domain.conf 設定の確認

次のエントリが既に存在することを確認します（変更は不要）。

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=password"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=password"
  ```

#### 手順 4：ノードを開始

1. **プライマリノード** を起動し、完全に初期化されるまで待ちます。
2. **セカンダリノード** を起動します。

### 検証

ログを確認します。

* **プライマリノード**

  ```
  <JBOSS_HOME>/domain/log/host-controller.log
  ```

  ```
  Registered remote secondary host "secondary"
  ```

* **セカンダリノード**

  ```
  Connected to primary host controller
  ```

## オプション 2：カスタム資格情報ストアの設定（実稼動）

**最適：** 高いセキュリティを必要とする実稼動環境。

### 設定手順

#### 手順 1：デフォルトの資格情報ストアを削除（存在する場合）

デフォルトの資格情報ストアが存在する場合は、名前を次のように変更します。

* **Windows**

  ```
  rename cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

* **Linux**

  ```
  mv cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

#### 手順 2：カスタム資格情報ストアの作成

`<JBOSS_HOME>/bin` から：

* **Windows**

  ```
  elytron-tool.bat credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

#### 手順 3：認証パスワードエイリアスの追加

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

#### 手順 4:domain.conf の更新

秘密鍵証明書ストアのパスワード参照を更新します。

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=YourCustomPassword"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=YourCustomPassword"
  ```

#### 手順 5:XML 設定の検証

設定済 `host-secondary.xml` の資格情報ストアおよび認証クライアントエントリが含まれていることを確認します。
デフォルト設定が存在する場合は、変更は必要ありません。


#### 手順 6：ノードを開始

1. **プライマリノード** を起動し、完全に起動するまで待ちます。
2. **セカンダリノード** を起動します。

### 検証

両方のノードのホスト コントローラ ログを使用して、登録が成功したことを確認します。

## 概要

* **オプション 1** は、事前設定済みの資格情報ストアを使用したクイックセットアップを提供します。
* **オプション 2** は、カスタムの資格情報ストアパスワードを使用して、より強力なセキュリティを有効にします。
* 設定を完了する必要があります **セカンダリノードのみ**。
* プライマリノードの設定は、ドメイン全体で自動的に再利用されます。

