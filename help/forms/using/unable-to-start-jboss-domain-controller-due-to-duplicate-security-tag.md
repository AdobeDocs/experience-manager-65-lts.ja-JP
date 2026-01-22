---
title: JBoss ドメインコントローラーを起動できない
description: JBoss EAP 8 を使用したAEM Forms 6.5.1 LTS クラスターのデプロイメントでは、設定ファイルに重複したタグが含まれている可能性があります。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 1%

---


# JBoss ドメインコントローラーを起動できない

## 問題

**JBoss EAP 8** を使用した **AEM Forms 6.5.1 LTS** クラスターデプロイメントでは、設定ファイルが
`<JBOSS_HOME>/domain/configuration/domain_oracle.xml` （およびデータベース固有のバリアント）に **重複する開始タグ `<security>` タグ** が含まれている場合があります。

これにより、**無効な XML 設定** が発生し、**JBoss ドメインコントローラーの起動が失敗し** クラスターが正常に初期化されなくなります。

## 適用先

* **製品：** AEM Forms 6.5.1 LTS
* **展開の種類：** クラスター
* **Application Server:** JBoss EAP 8.x
* **設定ファイル：**

   * `<JBOSS_HOME>/domain/configuration/domain_oracle.xml`
   * `<JBOSS_HOME>/domain/configuration/domain_mysql.xml`
   * `<JBOSS_HOME>/domain/configuration/domain_mssql.xml`

## トラブルシューティング手順

1. ドメイン コントローラの起動時に、次のエラーが発生することがあります。

   * `WFLYCTL0198: Unexpected element 'security'`
   * `IJ010061: Unexpected element: security`

2. 関連する設定ファイルを開きます。

   ```
   <JBOSS_HOME>/domain/configuration/domain_oracle.xml
   (or domain_mysql.xml / domain_mssql.xml)
   ```

3. 複製した `<security>` の開始タグを見つけます。

   **設定が正しくありません：**

   ```xml
   <security>
       <security>
           <user-name>adobe</user-name>
           <credential-reference store="db-creds" alias="EncryptDBPassword"/>
       </security>
   ```

4. 余分な開口部 `<security>` タグを削除して、次に示すように設定を修正します。

   **正しい設定：**

   ```xml
   <security>
       <user-name>adobe</user-name>
       <credential-reference store="db-creds" alias="EncryptDBPassword"/>
   </security>
   ```

5. ファイルを保存し、JBoss ドメインコントローラーを起動します。

6. 検証済みの同じ設定が、すべてのクラスターノードにわたって一貫して適用されるようにします。
