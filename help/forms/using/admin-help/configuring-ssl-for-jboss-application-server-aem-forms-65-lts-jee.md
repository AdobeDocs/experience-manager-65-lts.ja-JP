---
title: JBoss Application Server （AEM 6.5 LTS JEE）用のSSLの設定
description: JBoss Application Server での SSL の設定方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
exl-id: 8a2fbfdc-2b6a-4c9d-beab-1908a9261003
source-git-commit: 96fe29ceae4c38238ccc40d456f2ad8e276788c7
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# JBoss Application Server （AEM 6.5 LTS JEE）用のSSLの設定

## 概要

Java EEで動作するJBoss Application Server for Adobe Experience Manager（AEM） 6.5 LTSでSSLを設定するには、セキュアなHTTPS通信を有効にする必要があります。 SSLを有効にすると、クライアントとサーバー間でやり取りされるデータが暗号化されるため、本番環境のAEM Formsの導入では重要なセキュリティ要件となります。

このプロセスには、主にふたつの段階があります。

- **SSL資格情報を取得** – 自己署名証明書を生成するか、認証局（CA）から要求します。
- **JBossでSSLを有効にする** — JBoss CLI コマンドを使用してElytron サブシステムを使用します。

このガイドでは、次のプレースホルダー値を使用します。

- `[appserver root]` — AEM Formsを実行しているJBoss アプリケーションサーバーのホームディレクトリ。
- `[type]` – 実行されたインストールの種類によって異なるフォルダー名。
- `[JAVA_HOME]` — JDKがインストールされているディレクトリ。

## パート 1:SSL資格情報の作成（自己署名）

CAからの証明書がない場合は、Java `keytool` ユーティリティを使用して自己署名SSL資格情報を生成できます。 開発環境やテスト環境に適しています。

### ステップ 1 - キーストアを生成する

コマンドプロンプトで`[JAVA_HOME]/bin`に移動し、次のコマンドを実行して、値を環境に適した値に置き換えます。 ホスト名は、アプリケーションサーバーの完全修飾ドメイン名（FQDN）である必要があります。

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

プロンプトが表示されたら、`keystore_password`を入力します。 キーストアとキーのパスワードは同じである必要があります。

### 手順2 - キーストアを設定ディレクトリにコピーする

生成されたキーストアを、インストールタイプに適した設定フォルダーにコピーします。

```bash
# Windows Single Server
copy keystorename.keystore [appserver root]\standalone\configuration

# Windows Server Cluster
copy keystorename.keystore [appserver root]\domain\configuration

# Linux Single Server
cp keystorename.keystore [appserver root]/standalone/configuration

# Linux Server Cluster
cp keystorename.keystore [appserver root]/domain/configuration
```

### 手順3 – 証明書ファイルの書き出し

次のいずれかのコマンドを使用して、キーストアから証明書をエクスポートします。

```bash
# Single Server
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/standalone/configuration/keystorename.keystore

# Server Cluster
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/domain/configuration/keystorename.keystore
```

プロンプトが表示されたら、`keystore_password`を入力します。

### 手順4 – 証明書のコピーと検証

`AEMForms_cert.cer`を構成ディレクトリにコピーし、その内容を確認します：

```bash
# Copy (Linux Single Server example)
cp AEMForms_cert.cer [appserver root]/standalone/configuration

# Verify certificate contents (Single Server)
keytool -printcert -v -file [appserver root]/standalone/configuration/AEMForms_cert.cer

# Verify certificate contents (Server Cluster)
keytool -printcert -v -file [appserver root]/domain/configuration/AEMForms_cert.cer
```

### 手順5 – 証明書をJava トラストストアにインポートする

読み込む前に、`cacerts` ファイルが書き込み可能であることを確認してください。

```bash
# Windows: Right-click cacerts → Properties → deselect Read-only

# Linux:
chmod 777 [JAVA_HOME]/jre/lib/security/cacerts
```

次に、証明書を読み込みます。

```bash
keytool -import -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [JAVA_HOME]/jre/lib/security/cacerts
```

パスワードの入力を求められたら、「`changeit`」（デフォルトのJava トラストストストアパスワード）と入力します。このパスワードが変更されている場合は、管理者に確認してください。 **この証明書を信頼しますか？ [no]**、タイプ `yes`。 次の確認メッセージが表示されます。*「証明書がキーストアに追加されました。」*

>[!NOTE]
>
> WorkbenchからSSL経由でAEM Formsに接続する場合は、Workbench コンピューターに証明書もインストールする必要があります。

## パート 2:Elytron サブシステムを使用したJBossでのSSLの有効化

SSL資格情報を設定すると、JBoss CLI経由でElytron セキュリティサブシステムを使用してJBossでHTTPSを有効にできるようになりました。 続行する前に、キーストアファイルが適切な設定ディレクトリにあることを確認してください。

>[!NOTE]
>
> Windowsでは、各CLI コマンドは、改行のない1行として入力する必要があります。 `keystorename.keystore`を実際のファイル名に置き換え、`changeit`をキーストア/キーパスワードに置き換えます。

### ステップ 6a - Elytron キーストアを作成する

```bash
/subsystem=elytron/key-store=aemKeyStore:add(
  path="keystorename.keystore",
  relative-to=jboss.server.config.dir,
  type="JKS",
  credential-reference={clear-text="changeit"})
```

キーストアがその形式を使用している場合は、`JKS`を`PKCS12`に置き換えます。

### ステップ 6b - Elytron Key-Managerを作成する

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  credential-reference={clear-text="changeit"})
```

キーストアに複数の証明書エントリが含まれている場合は、エイリアスを明示的に指定します。

```bash
/subsystem=elytron/key-manager=aemKeyManager:add(
  key-store=aemKeyStore,
  alias="AEMForms Cert",
  credential-reference={clear-text="changeit"})
```

### 手順6c - サーバーSSL コンテキストの更新

```bash
/subsystem=elytron/server-ssl-context=applicationSSC:write-attribute(
  name=key-manager,
  value=aemKeyManager)
```

### ステップ 6d – 下のHTTPS リスナーを設定する

SSL コンテキストをUndertow （JBoss web サーバー）に接続して、HTTPS リスナーを有効にします。

```bash
/subsystem=undertow/server=default-server/https-listener=https:add(
  socket-binding=https,
  ssl-context=applicationSSC)
```

## パート 3：アプリケーションサーバーの再起動

Elytron設定が完了したら、JBossを再起動して変更を適用します。

### ターンキーインストール（Windows サービス）

- **Campaign コントロールパネル/管理ツール/サービス**&#x200B;を開きます。
- Adobe Experience Manager forms **の** JBossを選択します。
- **アクション/停止**&#x200B;を選択し、サービスが停止するのを待ちます。
- **アクション/開始**&#x200B;を選択します。

### 事前設定済みまたは手動のJBoss インストール

コマンドプロンプトから、`[appserver root]/bin`に移動します。

```bash
# Stop the server
Windows: shutdown.bat -S
Linux:   ./shutdown.sh -S

# Wait until JBoss fully shuts down, then start the server
Windows: run.bat -c <profile>
Linux:   ./run.sh -c <profile>
```

## パート 4：認証局から資格情報を要求する

実稼動環境では、信頼できる認証局（CA）によって発行された証明書を使用する必要があります。 このプロセスでは、キーペアを生成し、証明書署名要求（CSR）を作成してから、CA署名済み証明書を読み込みます。

### キーストアの生成とCSRの作成

`[JAVA_HOME]/bin`に移動して、キーストアを生成します。

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

次に、CAに送信するCSRを生成します。

```bash
keytool -certreq -alias "AEMForms Cert" \
  -keystore keystorename.keystore \
  -file AEMFormscertRequest.csr
```

`.csr` ファイルをCAに送信します。 署名済み証明書を再度受け取ったら、次の手順に従います。

### CA署名証明書の読み込み

最初にCA ルート証明書をインポートします。

```bash
keytool -import -trustcacerts -file rootcert.pem \
  -keystore keystorename.keystore -alias root
```

ルート証明書がまだブラウザーから信頼されていない場合は、そのルート証明書もブラウザーに読み込みます。 次に、CA署名証明書を読み込みます。

```bash
keytool -import -trustcacerts -file CACertificateName.crt \
  -keystore keystorename.keystore
```

>[!NOTE]
>
> 読み込まれたCA署名証明書は、キーストアに存在する既存の自己署名公開証明書を置き換えます。

CA証明書をインポートしたら、パート 2 （Elytron設定）の&#x200B;**手順6a ～ 6d**&#x200B;に進み、サーバーを再起動し（パート 3）、SSL アクセスを確認します。

## SSL アクセスの確認

サーバーを再起動した後、HTTPS経由でAEM Forms管理コンソールにアクセスして、SSLが正しく機能していることを確認します。 JBossのデフォルト SSL ポートは`8443`です。

```
https://[host name]:8443/adminui
```

管理コンソールがHTTPS経由で正常に読み込まれた場合、SSLは正しく設定されています。 以降のすべてのAEM FormsへのSSL接続にポート `8443`を使用します。
