---
title: データベース資格情報ストアの設定（Elytron ベース）
description: JBoss EAP 8 は、ドメインモード設定用のAEM Formsで、安全なデータベースパスワード管理のための Elytron 資格情報ストアをサポートしています。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
source-git-commit: f093f39fb535209297940cff13a99c7631812152
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 2%

---


# データベース資格情報ストアの設定（Elytron ベース）

## Elytron を使用したデータベース資格情報ストアの設定

JBoss EAP 8 では、**Elytron 資格情報ストア** を使用して、AEM Forms デプロイメントのデータベースパスワードを安全に管理します。 Adobeには、ドメインモードでの Elytron ベースの資格情報ストアの作成と設定を簡単に行うための **自動スクリプト** が用意されています。


この設定は、（JBoss ドメインコントローラーを起動する前に **完了する必要があり** す。

### 前提条件

* 資格情報ストア作成スクリプトを実行する前に **** JBoss サーバーを完全に停止する必要があります。
* 資格情報ストアの作成は、**オフラインモードのみ** で実行する必要があります。

JBoss が実行中の場合に停止するには：

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux/UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

### ダウンロードスクリプト

オペレーティングシステムに応じた適切なスクリプトをダウンロードします。

| スクリプト名 | オペレーティングシステム |
| -------------------------------- | ---------------- |
| `create-elytron-cred-domain.bat` | Windows |
| `create-elytron-cred-domain.sh` | Linux/UNIX |

Linux の場合、スクリプトを実行可能にします。

```
chmod +x create-elytron-cred-domain.sh
```

### 設定手順

#### 手順 1：スクリプトをダウンロードして配置する

適切なスクリプトをダウンロードして、次のディレクトリに配置します。

```
<JBOSS_HOME>/bin
```

#### 手順 2：スクリプトの実行

* **Windows**

  ```
  cd <JBOSS_HOME>\bin
  create-elytron-cred-domain.bat
  ```

* **Linux/UNIX**

  ```
  cd <JBOSS_HOME>/bin
  ./create-elytron-cred-domain.sh
  ```

#### 手順 3：必要な情報の提供

実行時に、スクリプトでは次の入力を求められます。

1. **JBOSS_HOME パス**
JBoss インストールディレクトリのフルパスを入力します。

2. **データベース構成ファイル名**
データベースに基づいて、次のいずれかを入力します。

   * `domain_oracle.xml`
   * `domain_mysql.xml`
   * `domain_mssql.xml`

3. **資格情報ストアのパスワード**
資格情報ストアを保護するための強力なパスワードを入力してください。

   > このパスワードは入力時には非表示になっており、後の手順で覚えておく必要があります。

4. **データベース パスワード**
実際のデータベース接続パスワードを入力します。

#### 手順 4：スクリプトの実行と検証

スクリプトは、次のアクションを自動的に実行します。

* `cred-store.p12` を次の場所に作成します。

  ```
  <JBOSS_HOME>/domain/configuration/
  ```

* 次の秘密鍵証明書のエイリアスを作成します。

   * `EncryptDBPassword`
   * `EncryptDBPassword_IDP_DS`
   * `EncryptDBPassword_EDC_DS`
   * `EncryptDBPassword_AEM_DS`
* すべてのエイリアスが正常に追加されたことを確認します

正常に実行されると、資格情報ストアの作成とエイリアスの検証が確認されます。

#### 手順 5:JVM オプションの設定

JBoss ドメインの起動設定を更新して、資格情報ストアパスワードを指定します。

* **Linux**
編集：

  ```
  <JBOSS_HOME>/bin/domain.conf
  ```

  次の行を追加します。

  ```
  JAVA_OPTS="$JAVA_OPTS -DCS_PASS=YourCredStorePassword"
  ```

* **Windows**
編集：

  ```
  <JBOSS_HOME>/bin/domain.conf.bat
  ```

  次の行を追加します。

  ```
  set "JAVA_OPTS=%JAVA_OPTS% -DCS_PASS=YourCredStorePassword"
  ```

`YourCredStorePassword` を、資格情報ストアの作成時に入力したパスワードに置き換えます。

ドメイン設定ファイルは、`${CS_PASS}` 変数を使用してこの値を参照します。


#### 手順 6：ドメイン設定の確認

データベース・ドメイン構成ファイルを開きます。

```
<JBOSS_HOME>/domain/configuration/<domain_*.xml>
```

データソースで Elytron 資格情報ストアが参照されていることを確認します。

```xml
<security>
    <user-name>your_database_username</user-name>
    <credential-reference store="db-creds" alias="EncryptDBPassword_IDP_DS"/>
</security>
```

各データソースは、特定のエイリアスを使用します。

* **IDP_DS:** `EncryptDBPassword_IDP_DS`
* **EDC_DS:** `EncryptDBPassword_EDC_DS`
* **AEM_DS:** `EncryptDBPassword_AEM_DS`
* **DefaultDS / ExampleDS:** `EncryptDBPassword`

すべてのエイリアスは、秘密鍵証明書ストアに保存されている同じデータベースパスワードを参照します。

>[!NOTE]
>
>* 資格情報ストアをプライマリノードのみで設定します。
>* セカンダリノードは、プライマリノードから同期されたドメイン設定を自動的に使用します。
