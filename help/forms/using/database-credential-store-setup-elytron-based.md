---
title: データベース資格情報ストアの設定（Elytron ベース）
description: JBoss EAP 8は、ドメインモードの設定のためにAEM Formsでセキュアデータベースのパスワード管理を行うためのElytron資格情報ストアをサポートしています。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: d7a9502b-8d6a-4d83-9b1f-0c82cbf34b70
source-git-commit: 58f549aaf5f248c2382477790c825bba1d737137
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 2%

---

# データベース資格情報ストアの設定（Elytron ベース）

## Elytronを使用したデータベース資格情報ストアの設定

JBoss EAP 8では、**Elytron資格情報ストア**&#x200B;を使用して、AEM Forms デプロイメント用のデータベースパスワードを安全に管理します。 Adobeには、ドメインモードでのElytron ベースの資格情報ストアの作成と設定を簡素化するための&#x200B;**自動化スクリプト**&#x200B;が用意されています。


JBoss Domain Controller **を開始する前に、この設定を**&#x200B;完了する必要があります。

### 前提条件

* 資格情報ストア作成スクリプトを実行する前に、**JBoss サーバーを完全に停止する必要があります**。
* 資格情報ストアの作成は、**オフラインモードでのみ**&#x200B;実行する必要があります。

実行中のJBossを停止するには：

* **Windows**

  ```
  <JBOSS_HOME>\bin\jboss-cli.bat --connect command=:shutdown
  ```

* **Linux / UNIX**

  ```
  <JBOSS_HOME>/bin/jboss-cli.sh --connect command=:shutdown
  ```

### スクリプトのダウンロード

オペレーティングシステムに基づいて適切なスクリプトをダウンロードします。

| スクリプト名 | オペレーティングシステム |
| -------------------------------- | ---------------- |
| `create-elytron-cred-domain.bat` | Windows |
| `create-elytron-cred-domain.sh` | Linux/UNIX |

Linuxの場合は、スクリプトを実行可能にします。

```
chmod +x create-elytron-cred-domain.sh
```

### 設定手順

#### 手順1：スクリプトのダウンロードと配置

適切なスクリプトをダウンロードし、次のディレクトリに配置します。

```
<JBOSS_HOME>/bin
```

#### ステップ 2: スクリプトを実行する

* **Windows**

  ```
  cd <JBOSS_HOME>\bin
  create-elytron-cred-domain.bat
  ```

* **Linux / UNIX**

  ```
  cd <JBOSS_HOME>/bin
  ./create-elytron-cred-domain.sh
  ```

#### 手順3：必要な情報の提供

実行時に、スクリプトは次の入力を求めます。

1. **JBOSS_HOME パス**
JBoss インストールディレクトリへのフルパスを入力します。

2. **データベース設定ファイル名**
データベースに基づいて、次のいずれかを入力します。

   * `domain_oracle.xml`
   * `domain_mysql.xml`
   * `domain_mssql.xml`

3. **資格情報ストアのパスワード**
資格情報ストアを保護するための強力なパスワードを入力します。

   > このパスワードは入力中は非表示になっており、後の手順で記憶する必要があります。

4. **データベースパスワード**
実際のデータベース接続パスワードを入力します。

#### 手順4：スクリプトの実行と検証

スクリプトは、次のアクションを自動的に実行します。

* `cred-store.p12`を次の場所に作成します：

  ```
  <JBOSS_HOME>/domain/configuration/
  ```

* 次の資格情報エイリアスを作成します。

   * `EncryptDBPassword`
   * `EncryptDBPassword_IDP_DS`
   * `EncryptDBPassword_EDC_DS`
   * `EncryptDBPassword_AEM_DS`
* すべてのエイリアスが正常に追加されたことを確認します

実行が成功すると、資格情報ストアの作成とエイリアスの検証が確認されます。

#### 手順5:JVM オプションの設定

JBoss ドメインの起動設定を更新して、資格情報ストアのパスワードを指定します。

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

`YourCredStorePassword`を、資格情報ストアの作成中に入力されたパスワードに置き換えます。

ドメイン設定ファイルは、`${CS_PASS}`変数を使用してこの値を参照します。


#### 手順6：ドメイン設定の確認

データベースドメイン設定ファイルを開きます。

```
<JBOSS_HOME>/domain/configuration/<domain_*.xml>
```

データソースがElytron資格情報ストアを参照していることを確認します。

```xml
<security>
    <user-name>your_database_username</user-name>
    <credential-reference store="db-creds" alias="EncryptDBPassword_IDP_DS"/>
</security>
```

各データソースは特定のエイリアスを使用します。

* **IDP_DS:** `EncryptDBPassword_IDP_DS`
* **EDC_DS:** `EncryptDBPassword_EDC_DS`
* **AEM_DS:** `EncryptDBPassword_AEM_DS`
* **DefaultDS / ExampleDS:** `EncryptDBPassword`

すべてのエイリアスは、資格情報ストアに保存されている同じデータベースパスワードを参照します。

>[!NOTE]
>
>* プライマリで作成された資格情報ストアファイル（cred-store.p12）を各スレーブノードにコピーします。

