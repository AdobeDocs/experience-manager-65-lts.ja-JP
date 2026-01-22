---
title: ' [!DNL Adobe Experience Manager] 6.5 LTS SP1 のリリースノート'
description: ' [!DNL Adobe Experience Manager] 6.5 LTS SP1 のリリース情報、新機能、インストール方法、詳細な変更リストを確認します。'
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 3%

---


# Adobe Experience Manager（AEM）Forms 6.5 LTS SP1 on JEE リリースノート


## リリース情報

| **製品** | Adobe Experience Manager Forms |
| -------------------- | ------------------------------------ |
| **バージョン** | 6.5 LTS SP1 |
| **タイプ** | 長期サポートサービスパック（JEE） |
| **リリースカテゴリ** | アップグレードリリース |
| **ダウンロード URL** | ソフトウェア配布 |

## [!DNL Experience Manager] 6.5 LTS SP1 の内容 {#what-is-included-in-aem-65ltssp1}

Adobe Experience Manager（AEM）Forms **6.5 LTS SP1 on JEE** は、製品の安定性と長期的なサポートに重点を置いて、新機能、お客様からリクエストされた主なプラットフォームのアップデート、一般的なバグ修正を提供します。

## AEM Forms 6.5 LTS SP1 の内容

### &#x200B;1. Java サポートアップデート

新しい Java バージョンのサポートが導入されました。

* **Java™ 17**
* **Java™ 21**

### &#x200B;2. アプリケーションサーバーのサポートアップデート

#### JBoss EAP 8 のサポート

* **JBoss EAP 8** のサポートが追加されました。
* 従来の **PicketBox** セキュリティフレームワークは削除されました。
* **Elytron ベースの資格情報ストア** がサポートされるようになり、安全な資格情報管理が可能になりました。

##### 設定：資格情報ストア（Elytron ベース）

JBoss EAP 8 上のAEM Formsは、安全な資格情報の管理に Elytron を使用します。 お客様は、サーバの正常な起動とデータベース認証の保護を確実に行うために、Elytron ベースのクレデンシャル・ストアを構成する必要があります。

設定の詳細については、インストールおよび設定ガイドを参照してください。

### &#x200B;3. プラットフォームと互換性の変更

#### サーブレット仕様のサポート

* **サーブレット仕様 5+** のサポート
* **ジャカルタ EE 9** 準拠に基づく

#### 名前空間の移行要件

* Jakarta EE 9 では、名前空間が `javax.*` から `jakarta.*` に変更されました
* すべての **カスタム DSC** を `jakarta.*` 名前空間に移行する必要があります
* AEM Forms 6.5 LTS SP1 は、**Jakarta EE 9 以降ベースのアプリケーションサーバーのみ** をサポートしています。

詳しくは、**javax から jakarta 名前空間への移行** を参照してください。

## アップグレード

アップグレード手順について詳しくは、**JEE 上のAEM Forms 6.5 LTS SP1 のアップグレードガイド** を参照してください。

## インストール

インストール手順と前提条件については、**AEM Forms 6.5 LTS SP1 （JEE）のインストールガイド** を参照してください。

## サポートされているプラットフォーム

サポートされているプラットフォーム、オペレーティング・システム、データベース、アプリケーション・サーバーの完全なリストについては、次を参照してください。

**サポートされているプラットフォームの一覧 – AEM Forms 6.5 LTS SP1 （JEE）**

## 廃止される機能および削除された機能

* CRX リポジトリ永続性の **RDBMK** のサポートが削除されました。
* クラスター環境の場合、リポジトリの永続性のために **MongoMK のみ** がサポートされています。

## Javax からジャカルタ名前空間への移行

### `javax` から `jakarta` 名前空間への移行

**AEM Forms 6.5 LTS SP1** 以降は、&lbrace;Jakarta Servlet API 5/6 **を実装するアプリケーションサーバーのみがサポートされ** す。 **Jakarta EE 9 以降** では、すべての API が `javax.{}` 名前空間から `jakarta.` 名前空間に移行しました。

その結果、**すべてのカスタム DSC は `jakarta` 名前空間を使用する必要があります**。 `javax.{}` API を使用して作成されたカスタムコンポーネントは、サポートされているアプリケーションサーバーと **互換性がありません**。

### カスタム DSC の移行オプション

次のいずれかの方法を使用して、既存のカスタム DSC を移行できます。

#### オプション 1:Source コードの移行（推奨）

* すべてのインポート文を `javax.{}` から `jakarta.` に更新
* カスタム DSC プロジェクトの再ビルドと再コンパイル
* 更新されたコンポーネントをアプリケーションサーバーに再デプロイします。

**メリット：**

* Jakarta EE 9 以降との長期的な互換性を確保
* アクティブに管理されているプロジェクトに最適

#### オプション 2:Eclipse Transformer を使用したバイナリ移行

* **Eclipse Transformer** ツールを使用して、コンパイル済みのバイナリ（`.jar`、`.war`）を `javax` から `jakarta` に変換します
* ソースコードの変更や再コンパイルは必要ありません
* 変換されたバイナリをアプリケーションサーバーに再デプロイします

>[!NOTE]
>
> バイナリ変換は **バイトコードレベル** で実行されます。

インポートマッピングのサンプル

移行時に必要な名前空間の変更の一般的な例を以下に示します。

前（javax）    後（ジャカルタ）
javax.servlet.*    jakarta.servlet.*
javax.servlet.http。*    jakarta.servlet.http。*

### インポートマッピングのサンプル

次の表に、`javax` から `jakarta` への移行時に必要になる、一般的な名前空間の変更を示します。

| 前（`javax`） | 後（`jakarta`） |
| ---------------------- | ------------------------ |
| `javax.servlet.*` | `jakarta.servlet.*` |
| `javax.servlet.http.*` | `jakarta.servlet.http.*` |

カスタム DSC ソースコードを更新する際や、変換されたバイナリを検証する際には、これらのマッピングを参照として使用してください。

