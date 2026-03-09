---
title: JBoss Application Server の SSL の設定（AEM 6.5 LTS JEE）
description: JBoss Application Server での SSL の設定方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
exl-id: 8a2fbfdc-2b6a-4c9d-beab-1908a9261003
source-git-commit: e48d0604cc8fd1cf745aafa9c70aab17944f4882
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 1%

---

# JBoss Application Server の SSL の設定（AEM 6.5 LTS JEE）

## 概要

Java EE で動作するAdobe Experience Manager（AEM） 6.5 LTS 用の JBoss Application Server で SSL を設定するには、安全な HTTPS 通信を有効にする必要があります。 SSL を有効にすると、クライアントとサーバーの間で交換されるデータが暗号化されるので、AEM Formsの実稼動環境のセキュリティ要件が非常に重要になります。

このプロセスには、次の 2 つの主な段階があります。

- **SSL 秘密鍵証明書の取得**：自己署名証明書を生成するか、認証局（CA）に証明書を要求します。
- **JBoss での SSL の有効化** - JBoss CLI コマンドを使用して Elytron サブシステムを使用。

このガイド全体で、次のプレースホルダー値を使用します。

- `[appserver root]` - AEM Formsを実行する JBoss Application Server のホームディレクトリ。
- `[type]` – 実行されるインストールのタイプによって異なるフォルダ名。
- `[JAVA_HOME]` — JDK がインストールされているディレクトリ。

## パート 1:SSL 秘密鍵証明書の作成（自己署名）

CA からの証明書がない場合は、Java `keytool` ユーティリティを使用して自己署名 SSL 秘密鍵証明書を生成できます。 これは、開発環境やテスト環境に適しています。

### 手順 1 - キーストアを生成する

コマンドプロンプトで `[JAVA_HOME]/bin` に移動し、次のコマンドを実行して、値を環境に適した値に置き換えます。 ホスト名は、アプリケーションサーバーの完全修飾ドメイン名（FQDN）である必要があります。

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

プロンプトが表示されたら、`keystore_password` を入力します。 キーストアのパスワードとキーは同一である必要があります。

### 手順 2 - キーストアを設定ディレクトリにコピーします。

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

### 手順 3 – 証明書ファイルのエクスポート

次のいずれかのコマンドを使用して、キーストアから証明書を書き出します。

```bash
# Single Server
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/standalone/configuration/keystorename.keystore

# Server Cluster
keytool -export -alias "AEMForms Cert" -file AEMForms_cert.cer \
  -keystore [appserver root]/domain/configuration/keystorename.keystore
```

プロンプトが表示されたら、`keystore_password` を入力します。

### 手順 4 – 証明書をコピーして検証する

`AEMForms_cert.cer` を設定ディレクトリにコピーし、その内容を確認します。

```bash
# Copy (Linux Single Server example)
cp AEMForms_cert.cer [appserver root]/standalone/configuration

# Verify certificate contents (Single Server)
keytool -printcert -v -file [appserver root]/standalone/configuration/AEMForms_cert.cer

# Verify certificate contents (Server Cluster)
keytool -printcert -v -file [appserver root]/domain/configuration/AEMForms_cert.cer
```

### 手順 5 – 証明書を Java トラストストアにインポート

インポートする前に、`cacerts` ファイルが書き込み可能であることを確認してください。

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

パスワードの入力を求められたら、`changeit` （デフォルトの Java トラストストアパスワード。これが変更されているかどうかを管理者に確認してください）と入力します。 **この証明書を信頼しますか？ [ いいえ]**、「`yes`」と入力します。 「*証明書がキーストアに追加されました。」という確認メッセージが表示されます*

>[!NOTE]
>
> Workbench から SSL 経由でAEM Formsに接続する場合は、証明書を Workbench コンピューターにもインストールする必要があります。

## パート 2:Elytron サブシステムを使用した JBoss での SSL の有効化

SSL 資格情報を配置すると、JBoss CLI で Elytron セキュリティサブシステムを使用して、JBoss で HTTPS を有効にできるようになります。 続行する前に、キーストアファイルが適切な設定ディレクトリにあることを確認します。

>[!NOTE]
>
> Windows では、各 CLI コマンドを改行なしで 1 行で入力する必要があります。 `keystorename.keystore` は実際のファイル名に、`changeit` はキーストア/キーのパスワードに置き換えます。

### 手順 6a - Elytron キーストアの作成

```bash
/subsystem=elytron/key-store=aemKeyStore:add(
  path="keystorename.keystore",
  relative-to=jboss.server.config.dir,
  type="JKS",
  credential-reference={clear-text="changeit"})
```

キーストアで `JKS` の形式を使用している場合は、`PKCS12` を AEM に置き換えます。

### 手順 6b - Elytron Key-Manager の作成

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

### 手順 6c - サーバー SSL コンテキストの更新

```bash
/subsystem=elytron/server-ssl-context=applicationSSC:write-attribute(
  name=key-manager,
  value=aemKeyManager)
```

### 手順 6d - Undertow HTTPS リスナーの設定

SSL コンテキストを Undertow （JBoss web サーバー）にワイヤリングして、HTTPS リスナーを有効にします。

```bash
/subsystem=undertow/server=default-server/https-listener=https:add(
  socket-binding=https,
  ssl-context=applicationSSC)
```

## パート 3：アプリケーションサーバーの再起動

Elytron 設定が完了したら、JBoss を再起動して変更を適用します。

### 自動インストール（Windows サービス）

- **Campaign コントロールパネル/管理ツール/サービス** を開きます。
- **Adobe Experience Manager Forms の JBoss** を選択します。
- **アクション/停止** を選択し、サービスが停止するのを待ちます。
- **アクション/開始** を選択します。

### 事前設定済みの JBoss インストールまたは手動の JBoss インストール

コマンドプロンプトで、`[appserver root]/bin` に移動します。

```bash
# Stop the server
Windows: shutdown.bat -S
Linux:   ./shutdown.sh -S

# Wait until JBoss fully shuts down, then start the server
Windows: run.bat -c <profile>
Linux:   ./run.sh -c <profile>
```

## 第 4 部：認証局からの秘密鍵証明書の要求

実稼動環境の場合は、信頼できる認証局（CA）から発行された証明書を使用する必要があります。 このプロセスには、キーペアの生成、証明書署名リクエスト（CSR）の作成、CA 署名証明書の読み込みが含まれます。

### キーストアの生成と CSR の作成

`[JAVA_HOME]/bin` に移動し、キーストアを生成します。

```bash
keytool -genkey -dname "CN=Host Name, OU=Group Name, O=Company Name, L=City Name, S=State, C=Country Code" \
  -alias "AEMForms Cert" -keyalg RSA \
  -keypass key_password -keystore keystorename.keystore
```

次に、CSR を生成して CA に送信します。

```bash
keytool -certreq -alias "AEMForms Cert" \
  -keystore keystorename.keystore \
  -file AEMFormscertRequest.csr
```

`.csr` ファイルを CA に送信します。 署名付き証明書を受け取ったら、次の手順に従います。

### CA 署名証明書の読み込み

最初に CA ルート証明書を読み込みます。

```bash
keytool -import -trustcacerts -file rootcert.pem \
  -keystore keystorename.keystore -alias root
```

ルート証明書がまだブラウザーで信頼されていない場合は、ブラウザーにも読み込みます。 次に、CA 署名証明書を読み込みます。

```bash
keytool -import -trustcacerts -file CACertificateName.crt \
  -keystore keystorename.keystore
```

>[!NOTE]
>
> キーストアに自己署名付きの公開証明書が存在する場合、読み込まれた CA 署名付き証明書によって、既存の自己署名付き公開証明書が置き換えられます。

CA 証明書が読み込まれたら、パート 2 （Elytron 設定）の **手順 6a～6d** に進み、サーバーを再起動し（パート 3）、SSL アクセスを確認します。

## SSL アクセスの検証

サーバーを再起動したら、HTTPS でAEM Forms管理コンソールにアクセスして、SSL が正しく機能していることを確認します。 JBoss のデフォルトの SSL ポートは `8443` です。

```
https://[host name]:8443/adminui
```

管理コンソールが HTTPS 経由で正常に読み込まれる場合、SSL は正しく設定されています。 AEM Formsへのそれ以降のすべての SSL 接続には、ポート `8443` を使用します。
