---
title: JEE 6.5 LTS SP2上のAEM Formsのサーバーサイド要求フォージェリー（SSRF）の脆弱性を軽減する
description: JEE 6.5 LTS サービスパック 2のデプロイメントがJBossで実行されているAEM Forms上のサーバーサイドリクエストフォージェリー（SSRF）の脆弱性の緩和手順。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin
exl-id: 7c4a9e12-3b8f-4d6a-9f1e-2a5c8d7e6b04
source-git-commit: 314aafaec6b45d7ea929f32d47e73da293800d4b
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 28%

---

# サーバーサイド要求フォージェリー（SSRF）の脆弱性の軽減

## クイックリファレンス {#quick-reference}

| 影響レベル | 影響を受けるバージョン | アクションの提案 |
| --- | --- | --- |
| 重大 | JEE 6.5 LTS サービスパック 2 （6.5 LTS SP2）上のAEM Forms | 手動で[&#x200B; ホットフィックス &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear)をインストールする |
| 影響なし | AEM Forms on OSGi、Workbench、Cloud Service | アクションは必要ありません |

**対処された脆弱性：**

* サーバーサイド リクエストフォージェリー（SSRF）（CWE-918）

## 概要 {#overview}

### 影響を受けるもの {#whats-affected}

| 脆弱性 | 影響 | 影響を受けるコンポーネント |
| --- | --- | --- |
| サーバーサイド リクエストフォージェリー（SSRF）（CWE-918） | 攻撃者は、内部または外部のリソースに意図しないリクエストを行うようにサーバーを誘導する可能性があります | JEE 6.5 LTS SP2上のAEM Forms |

### 影響を受けないもの {#whats-not-affected}

* Experience Manager Forms ワークベンチ（すべてのバージョン）
* OSGi 版 Experience Manager Forms（すべてのバージョン）
* Experience Manager Forms as a Cloud Service

## 解決策オプション {#resolution-options}

### 始める前に {#before-you-start}

変更を加える前に、置き換えようとしているEAR ファイルのバックアップを取ります。

* デプロイメントディレクトリで`adobe-edcserver-jboss.ear`を見つけます。

  ```text
  [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
  ```

* ファイルをデプロイメントディレクトリの外部の安全なバックアップ場所にコピーします。
* 更新を進める前に、バックアップが完了し、アクセス可能であることを確認します。

この予防措置により、更新プロセス中に問題が発生した場合に元の状態を復元できます。

### JEE 6.5 LTS SP2 （JBoss）でのAEM Formsの手動ホットフィックスのインストール

1. [Adobe Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/adobe-edcserver-jboss.ear)から`adobe-edcserver-jboss.ear`をダウンロードします。

1. デプロイメントディレクトリの`adobe-edcserver-jboss.ear`を見つけ、ダウンロードしたファイルに置き換えます。

   ```text
   [AEM installation directory]/deploy/adobe-edcserver-jboss.ear
   ```

1. AEM Forms Configuration Managerを起動して、更新されたEARを再デプロイし、ホットフィックスを適用します。

1. アプリケーションサーバーを再起動し、サーバーログからデプロイメントが正常に完了したことを確認します。

## 参照 {#references}

* [Adobe Experience Manager Formsのセキュリティのベストプラクティス](/help/forms/using/hardening-securing-aem-forms-environment.md)
