---
title: プロセスレポートの概要
description: JEE 上の AEM Forms Process Reporting の概要と主な機能
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 755df7e2-3603-4c0d-ad07-ec6f27de8c64
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 96%

---

# プロセスレポートの概要{#introduction-to-process-reporting}

![process-reporting](assets/process-reporting.png)

プロセスレポートは、AEM Forms のプロセスとタスクに関するレポートを作成および表示するために使用する、ブラウザーベースのツールです。

プロセスレポートは、標準の一連のレポートを提供し、長時間実行中のプロセス、プロセス期間、ワークフローの量に関する情報のフィルタリングと表示を行います。

さらに、プロセスレポートには、アドホッククエリを実行し、カスタムレポートビューをプロセスレポートユーザーインターフェイスに統合するためのインターフェイスが用意されています。

サポートされているブラウザーの一覧については、[AEM Forms サポートプラットフォームを参照してください ](/help/sites-deploying/technical-requirements.md)

プロセスレポートは、以下のモジュールにもとづいて構築されています。

* AEM Forms Database からプロセスデータを読み取る
* 埋め込みプロセスレポートリポジトリーにプロセスデータを公開
* レポートを表示するためのブラウザーベースのユーザーインターフェイスを提供

## 主な機能 {#key-capabilities}

### 常時稼動のレポート {#always-on-reporting}

![site-management](assets/site-management.png)

長時間実行されているプロセスのリスト、期間グラフの処理、およびフィルターを使用したカスタムクエリの実行を表示します。

また、レポートおよびクエリデータを CSV 形式でエクスポートするオプションも提供されます。

### アドホックレポート {#adhoc-reports}

![print-&amp;-color](assets/print-&-colour.png)

フィルターを使用して、データの特定の表示を取得します。

ID、期間、開始日と終了日、プロセス開始者などで、プロセスまたはタスクを検索できます。

複数のフィルターを組み合わせて、特定のレポートを作成できます。

その後、後で実行するようにレポートフィルターを保存できます。

### プロセス／タスクの履歴 {#process-task-history}

![file-management](assets/file-management.png)

AEM Forms サーバーは、多数のプロセスを並行して実行します。これらのプロセスは、ある状態から別の状態への移行を続けます。Forms のデータを一定の間隔でプロセスレポートリポジトリーに公開すると、プロセスレポートには、AEM Forms で実行中のプロセスに関する移行情報が保持されます。

### アクセス制御 {#access-control-br}

![名称未設定](assets/untitled.png)

プロセスレポートは、ユーザーインターフェイスへの権限ベースのアクセスを提供します。

つまり、レポート権限を持つユーザーのみがプロセスレポートのユーザーインターフェイスにアクセスできます。
