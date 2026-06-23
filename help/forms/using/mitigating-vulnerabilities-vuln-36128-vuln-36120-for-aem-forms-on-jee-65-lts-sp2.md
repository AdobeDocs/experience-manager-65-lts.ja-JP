---
title: JEE 6.5 LTS SP2上のAEM FormsのVULN-36128およびVULN-36120の脆弱性の軽減
description: JEE 6.5 LTS サービスパック 2のデプロイメントがJBossで実行されているAEM Forms上のVULN-36128およびVULN-36120の緩和手順。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 1b876f20cbc3a00a02a4449f0d353fb858695235
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 14%

---

# JEE 6.5 LTS SP2上のAEM FormsのVULN-36128およびVULN-36120の脆弱性の軽減

## クイックリファレンス {#quick-reference}

| 影響レベル | 影響を受けるバージョン | アクションの提案 |
| --- | --- | --- |
| 重大 | JEE 6.5 LTS サービスパック 2 （6.5 LTS SP2）上のAEM Forms | 手動で[&#x200B; ホットフィックス &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear)をインストールする |
| 影響なし | AEM Forms on OSGi、Workbench、Cloud Service | アクションは必要ありません |

**対処された脆弱性：**

* **VULN-36128**：不正なリモート攻撃者が任意のコードを実行できるようにするリモート コード実行の脆弱性。
* **VULN-36120**：機密情報への不正アクセスを許可する可能性のある、不適切な入力検証の脆弱性です。

## 緩和ステップ {#mitigation-steps}

### 始める前に {#before-you-start}

変更を加える前に、置き換えるEAR ファイルをバックアップします。

* デプロイメントディレクトリで`adobe-edcserver-jboss.ear`を見つけます。

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* ファイルをデプロイメントディレクトリの外部の安全なバックアップ場所にコピーします。
* 更新を進める前に、バックアップが完了し、アクセス可能であることを確認します。

この予防策により、更新プロセス中に問題が発生した場合は、元の状態を復元できます。

### JEE 6.5 LTS SP2 （JBoss）でのAEM Formsの手動ホットフィックスのインストール {#manual-hotfix-installation-aem-forms-jee-65-lts-sp2-jboss}

1. [Adobe Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear)から`adobe-edcserver-jboss.ear`をダウンロードします。

1. デプロイメントディレクトリの`adobe-edcserver-jboss.ear`を見つけ、ダウンロードしたファイルに置き換えます。

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. AEM Forms Configuration Managerを起動して、更新されたEARを再デプロイし、パッチを完全に適用します。

1. アプリケーションサーバーを再起動し、サーバーログからデプロイメントが正常に完了したことを確認します。

## 参照 {#references}

* [Adobe Experience Manager Formsのセキュリティのベストプラクティス](/help/forms/using/hardening-securing-aem-forms-environment.md)
