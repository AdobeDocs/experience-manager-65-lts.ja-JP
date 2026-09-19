---
title: セカンダリノード認証の設定（Elytron ベース）
description: JBoss EAP 8は、Elytronを使用して、プライマリドメインコントローラーとのセカンダリノードの安全な通信と登録を可能にします。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: 212aa75c-7f2a-4140-8051-77643065e429
source-git-commit: c89b742e24734fc67883b9dec966f59a01062a2a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 5%
---
# セカンダリノード認証の設定（Elytron ベース）

## Elytronを使用したセカンダリノード認証の設定

JBoss EAP 8では、**Elytron**&#x200B;を使用して、クラスター化されたデプロイメントの&#x200B;**プライマリノードとセカンダリノード**&#x200B;間の通信を認証します。 この設定により、プライマリドメインコントローラーとのセカンダリノードの安全な登録と通信が保証されます。

環境とセキュリティ要件に応じて、2つの設定オプションを使用できます。


## 前提条件

* `secondary`**という名前の**&#x200B;管理ユーザーを&#x200B;**プライマリノード**&#x200B;に作成する必要があります。
* この設定は、セカンダリノード **でのみ実行します**。
* クラスター内の各セカンダリノード **について、**&#x200B;設定を繰り返します。
* プライマリノードとセカンダリノードの両方で&#x200B;**JBossを完全に停止する必要があります**。
* すべての資格情報ストア操作は、**オフラインモード**&#x200B;で実行する必要があります。

実行中のJBossを停止するには：

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux / UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

## 設定オプションの選択

* **オプション 1：既定の資格情報ストアを使用したクイック セットアップ**
より低い環境とテスト向け。

* **オプション 2：資格情報ストアのカスタム設定**
本番環境と安全な環境に適しています。

## オプション 1：デフォルトの資格情報ストアを使用したクイックセットアップ

**開発、テスト、クイック セットアップのシナリオ：**&#x200B;に最適です。

### 概要

* 既定の資格情報ストア ファイル （`cs_secondary_hc.p12`）が事前設定されています。
* 既定の資格情報ストア パスワードは既に`domain.conf`に設定されています。
* 認証パスワードエイリアスのみを追加する必要があります。

### 設定手順

#### 手順1：デフォルトの資格情報ストアの確認

デフォルトの資格情報ストアファイルが存在することを確認します。

* **Windows**

  ```
  <JBOSS_HOME>\domain\configuration\cs_secondary_hc.p12
  ```

* **Linux**

  ```
  <JBOSS_HOME>/domain/configuration/cs_secondary_hc.p12
  ```

ファイルが存在しない場合は、**オプション 2**&#x200B;を使用します。

#### 手順2：認証パスワードエイリアスの追加

`<JBOSS_HOME>/bin`から次のコマンドを実行します。

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "password" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

> 秘密鍵の値は、プライマリノードで`secondary` ユーザーを作成する際に使用されるパスワードと一致する必要があります。

#### 手順3:domain.conf設定の確認

次のエントリが既に存在することを確認します（変更は必要ありません）。

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=password"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=password"
  ```

#### 手順4：ノードの開始

1. **プライマリノード**&#x200B;を開始し、完全に初期化されるのを待ちます。
2. **セカンダリノード**&#x200B;を開始します。

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

## オプション 2：カスタム資格情報ストア設定（実稼動環境）

**強化されたセキュリティを必要とする**&#x200B;実稼動環境に最適です。

### 設定手順

#### 手順1：デフォルトの資格情報ストアの削除（存在する場合）

デフォルトの資格情報ストアが存在する場合は、名前を変更します。

* **Windows**

  ```
  rename cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

* **Linux**

  ```
  mv cs_secondary_hc.p12 cs_secondary_hc.p12.bak
  ```

#### 手順2：カスタム資格情報ストアの作成

`<JBOSS_HOME>/bin`から：

* **Windows**

  ```
  elytron-tool.bat credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --create --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12"
  ```

#### 手順3：認証パスワードエイリアスの追加

* **Windows**

  ```
  elytron-tool.bat credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

* **Linux**

  ```
  ./elytron-tool.sh credential-store --location "../domain/configuration/cs_secondary_hc.p12" --password "YourCustomPassword" --type KeyStoreCredentialStore --properties "keyStoreType=PKCS12" --add "secondary_hc_auth" --secret "ActualSecondaryUserPassword"
  ```

#### 手順4:domain.confの更新

資格情報ストアのパスワード参照を更新します。

* **Windows**

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DSec_Auth_PASS=YourCustomPassword"
  ```

* **Linux**

  ```
  JAVA_OPTS="$JAVA_OPTS -DSec_Auth_PASS=YourCustomPassword"
  ```

#### 手順5:XML設定の検証

`host-secondary.xml`に、設定済みの資格情報ストアと認証クライアントのエントリが含まれていることを確認します。
デフォルト設定が存在する場合、変更は必要ありません。


#### 手順6: ノードの開始

1. **プライマリノード**&#x200B;を開始し、完全に開始されるまで待ちます。
2. **セカンダリノード**&#x200B;を開始します。

### 検証

両方のノードのホストコントローラのログを使用して、登録が成功したことを確認します。

## 概要

* **オプション 1**&#x200B;では、事前設定済みの資格情報ストアを使用して迅速に設定できます。
* **オプション 2**&#x200B;は、カスタム資格情報ストア パスワードを使用して、より強力なセキュリティを有効にします。
* セカンダリノードでのみ&#x200B;**設定を完了する必要があります**。
* プライマリノードの設定は、ドメイン全体で自動的に再利用されます。
