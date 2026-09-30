---
title: JBoss ドメインコントローラーを開始できません
description: JBoss EAP 8を使用したAEM Forms 6.5.1 LTS クラスターのデプロイメントでは、コンフィギュレーションファイルに重複したタグが含まれている場合があります。
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: f24e7245-7b43-4b1c-ba7a-162344ef545c
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 1%
---
# JBoss ドメインコントローラーを開始できません

## 問題

**JBoss EAP 8**&#x200B;を使用した&#x200B;**AEM Forms 6.5.1 LTS** クラスターのデプロイメントでは、設定ファイル
`<JBOSS_HOME>/domain/configuration/domain_oracle.xml` （およびデータベース固有のバリアント）には、**重複する開始`<security>` タグ**&#x200B;が含まれている場合があります。

これにより、**無効なXML設定**&#x200B;が発生し、**JBoss Domain Controllerの起動エラー**&#x200B;が発生し、クラスターの初期化が正常に行われなくなります。

## 適用先

* **製品：** AEM Forms 6.5.1 LTS
* **デプロイメントの種類：** クラスター
* **アプリケーションサーバー：** JBoss EAP 8.x
* **設定ファイル：**

  * `<JBOSS_HOME>/domain/configuration/domain_oracle.xml`
  * `<JBOSS_HOME>/domain/configuration/domain_mysql.xml`
  * `<JBOSS_HOME>/domain/configuration/domain_mssql.xml`

## トラブルシューティング手順

1. Domain Controllerの起動時に、次のエラーが発生する場合があります。

   * `WFLYCTL0198: Unexpected element 'security'`
   * `IJ010061: Unexpected element: security`

2. 関連する設定ファイルを開きます。

   ```
   <JBOSS_HOME>/domain/configuration/domain_oracle.xml
   (or domain_mysql.xml / domain_mssql.xml)
   ```

3. 重複する`<security>`開始タグを見つけます。

   **設定が正しくありません：**

   ```xml
   <security>
       <security>
           <user-name>adobe</user-name>
           <credential-reference store="db-creds" alias="EncryptDBPassword"/>
       </security>
   ```

4. 次に示すように、構成が修正されるように、追加の開始`<security>` タグを削除します。

   **正しい設定：**

   ```xml
   <security>
       <user-name>adobe</user-name>
       <credential-reference store="db-creds" alias="EncryptDBPassword"/>
   </security>
   ```

5. ファイルを保存し、JBoss ドメインコントローラーを起動します。

6. すべてのクラスターノードに同じ検証済み設定が一貫して適用されていることを確認します。
