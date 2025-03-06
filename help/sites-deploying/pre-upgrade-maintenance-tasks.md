---
title: アップグレード前のメンテナンスタスク
description: AEM に推奨されるアップグレード前のタスクについて説明します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 1dd5d370-d1d4-4d15-9663-35b941b9076b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 81%

---

# アップグレード前のメンテナンスタスク{#pre-upgrade-maintenance-tasks}

アップグレードの開始前に、次のメンテナンスタスクに従って、システムの準備が完了し、問題が発生した場合にロールバックができる状態にしておくことが重要です。

* [インデックスの定義](#index-definitions)
* [十分なディスク領域の確保](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#ensure-sufficient-disk-space)
* [AEM の完全なバックアップ](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#fully-back-up-aem)
* [quickstart.properties ファイルの生成](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#generate-quickstart-properties)
* [ワークフローおよび監査ログのパージの設定](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#configure-wf-audit-purging)
* [アップグレード前のタスクのインストール、設定および実行](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#install-configure-run-pre-upgrade-tasks)
* [/install ディレクトリからの更新の削除](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#remove-updates-install-directory)
* [すべてのコールドスタンバイインスタンスの停止](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#stop-tarmk-coldstandby-instance)
* [カスタムのスケジュール済みジョブの無効化](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#disable-custom-scheduled-jobs)
* [オフラインでのリビジョンクリーンアップの実行](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-offline-revision-cleanup)
* [データストアのガベージコレクションの実行](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#execute-datastore-garbage-collection)
* [必要に応じてデータベーススキーマをアップグレード](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#upgradethedatabaseschemaifneeded)
* [ログファイルのローテーション](/help/sites-deploying/pre-upgrade-maintenance-tasks.md#rotate-log-files)

## インデックスの定義 {#index-definitions}

AEM サービスパック 22 以前に提供されたAEM 6.5 サービスパックでリリースされた必須のインデックス定義がインストールされていることを確認してください。 （詳しくは、[AEM 6.5 servicepack リリースノート ](https://experienceleague.adobe.com/ja/docs/experience-manager-65/content/release-notes/release-notes) を参照してください）。

## 十分なディスク領域の確保 {#ensure-sufficient-disk-space}

アップグレードを実行する際は、十分なディスク容量があることを確認します。

## AEM の完全なバックアップ {#fully-back-up-aem}

アップグレードの開始前に、AEM を完全にバックアップする必要があります。該当する場合は、リポジトリ、アプリケーションのインストール、データストア、Mongo インスタンスを必ずバックアップします。AEM インスタンスのバックアップと復元についての詳細情報は、[バックアップと復元](/help/sites-administering/backup-and-restore.md)を参照してください。

## quickstart.properties ファイルの生成 {#generate-quickstart-properties}

jar ファイルから AEM を起動すると、`crx-quickstart/conf` の下に `quickstart.properties` ファイルが生成されます。これまで AEM を起動スクリプトでのみ起動していた場合、このファイルは存在せず、アップグレードは失敗します。このファイルが存在するかどうかを確認し、存在しない場合は jar ファイルから AEM を再起動します。

## ワークフローおよび監査ログのパージの設定 {#configure-wf-audit-purging}

`WorkflowPurgeTask` タスクと `com.day.cq.audit.impl.AuditLogMaintenanceTask` タスクには個別の OSGi 設定が必要であり、この設定がない場合は機能しません。アップグレード前のタスクの実行中にこれらのタスクが失敗した場合、最も考えられる原因は、タスクに設定がないことです。したがって、これらのタスクに OSGi 設定を追加するか、タスクを実行しない場合はアップグレード前の最適化タスクリストから完全に削除してください。ワークフローのパージタスクの設定に関するドキュメントは[ワークフローインスタンスの管理](/help/sites-administering/workflows-administering.md)で、監査ログのメンテナンスタスクの設定に関するドキュメントは [AEM 6 の監査ログのメンテナンス](/help/sites-administering/operations-audit-log.md)で参照できます。


## アップグレード前のタスクのインストール、設定および実行 {#install-configure-run-pre-upgrade-tasks}

以前は手動で実行する必要があった、アップグレード前のメンテナンスタスクの最適化と自動化が進められています。アップグレード前のメンテナンスの最適化により、統合されたこれらのタスクのトリガーが可能になり、その結果をオンデマンドで調べることができます。

### 使用方法 {#how-to-use-it}

`PreUpgradeTasksMBean` OSGI コンポーネントは、アップグレード前のメンテナンスタスクのリストで事前設定されており、それらのすべてのタスクを一度に実行できます。以下の手順に従ってタスクを設定できます。

1. *https://serveraddress:serverport/system/console/configMgr* にブラウジングして web コンソールに移動

1. 「**preupgradetasks**」を検索し、最初に一致したコンポーネントをクリックします。コンポーネントのフルネームは `com.adobe.aem.upgrade.prechecks.mbean.impl.PreUpgradeTasksMBeanImpl` です。

1. 次に示すように、実行が必要なメンテナンスタスクのリストを変更します。

   ![1487758925984](assets/1487758925984.png)

各メンテナンスタスクの設計対象となる実行モードの説明を次に示します。

| タスク | メモ |
|---|---|
| WorkflowPurgeTask | 実行前に、Adobe Granite のワークフローのパージ設定 OSGi を設定する必要があります。 |
| GenerateBundlesListFileTask |   |
| RevisionCleanupTask |   |
| com.day.cq.audit.impl.AuditLogMaintenanceTask | 実行前に、監査ログのパージスケジューラー OSGi 設定を設定する必要があります。 |

### アップグレード前のヘルスチェックのデフォルトの設定 {#default-configuration-of-the-pre-upgrade-health-checks}

`PreUpgradeTasksMBeanImpl` OSGI コンポーネントは、`runAllPreUpgradeHealthChecks` メソッドが呼び出されたときに実行されるアップグレード前のヘルスチェックタグのリストで事前設定されています。

* **system** - Granite のメンテナンスヘルスチェックで使用するタグです。

* **pre-upgrade** - アップグレード前に実行するように設定できるすべてのヘルスチェックに追加できるカスタムタグです。

**MBean メソッド**

マネージド Bean 機能には、[JMX コンソール](/help/sites-administering/jmx-console.md)を使用してアクセスできます。

以下の手順で MBean にアクセスできます。

1. JMX コンソール（*https://serveraddress:serverport/system/console/jmx*）に移動
1. 「**PreUpgradeTasks**」を検索し、結果をクリックします。

1. 「**操作**」セクションからメソッドを選択し、次のウィンドウで「**呼び出し**」を選択します。

`PreUpgradeTasksMBeanImpl` によって公開されている使用可能なすべてのメソッドのリストを以下に示します。

| メソッド名 | タイプ | 説明 |
|---|---|---|
| runAllPreUpgradeTasks （） | アクション | リストに含まれるアップグレード前のメンテナンスタスクをすべて実行します。 |
| runPreUpgradeTask （preUpgradeTaskName） | アクション | パラメーターで名前が指定されたアップグレード前のメンテナンスタスクを実行します。 |
| getPreUpgradeTaskLastRunTime （preUpgradeTaskName） | アクション | パラメーターで名前が指定されたアップグレード前のメンテナンスタスクの正確な実行時間を表示します。 |
| getPreUpgradeTaskLastRunState （preUpgradeTaskName） | アクション | パラメーターで名前が指定されたアップグレード前のメンテナンスタスクの最終実行状態を表示します。 |
| runAllPreUpgradeHealthChecks （shutDownOnSuccess） | アクション | アップグレード前のすべてのヘルスチェックを実行して、sling ホームパスの preUpgradeHCStatus.properties というファイルにそれらのステータスを保存します。 shutDownOnSuccess が true に設定されていると、AEM インスタンスがシャットダウンされますが、これはアップグレード前のすべてのヘルスチェックのステータスが OK の場合のみです。 properties ファイルは今後のアップグレードの前提条件として使用され、アップグレード前のヘルスチェックの実行に失敗した場合は、アップグレードプロセスが停止されます。 アップグレード前のヘルスチェックの結果を無視してアップグレードを開始する場合は、このファイルを削除できます。 |
| detectUsageOfUnavailableAPI （aemVersion） | アクション | 指定されたAEMのバージョンにアップグレードしたときに適合しなくなる読み込み済みパッケージをすべてリストします。 対象のAEMのバージョンは、パラメーターとして指定する必要があります。 |

>[!NOTE]
>
>MBean メソッドは、以下から呼び出すことができます。
>
>* JMX コンソール
>* JMX に接続する外部アプリケーション
>* cURL
>

## /install ディレクトリからの更新の削除 {#remove-updates-install-directory}

>[!NOTE]
>
>パッケージは、AEM インスタンスをシャットダウンした後でのみ crx-quickstart/install ディレクトリから削除します。これは、インプレースアップグレード手順を開始する前の最後の手順の 1 つです。

ローカルファイルシステムの `crx-quickstart/install` ディレクトリを介してデプロイされたサービスパック、機能パックまたはホットフィックスを削除します。これにより、更新が完了した後に、新しい AEM バージョンに古いホットフィックスおよびサービスパックが誤ってインストールされることを防止できます。

## すべてのコールドスタンバイインスタンスの停止 {#stop-tarmk-coldstandby-instance}

TarMK コールドスタンバイを使用している場合は、すべてのコールドスタンバイインスタンスを停止します。これにより、アップグレードで問題が発生した場合でも、効率的にオンラインに戻すことができます。アップグレードが正常に完了したら、アップグレードされたプライマリインスタンスからコールドスタンバイインスタンスを再構築する必要があります。

## カスタムのスケジュール済みジョブの無効化 {#disable-custom-scheduled-jobs}

アプリケーションコードに含まれている OSGi スケジュール済みジョブを無効にします。

## オフラインでのリビジョンクリーンアップの実行 {#execute-offline-revision-cleanup}

>[!NOTE]
>
>この手順は、TarMK インストール環境でのみ必要です。

TarMK を使用している場合は、アップグレードの前にオフラインでのリビジョンクリーンアップを実行してください。これにより、リポジトリの移行ステップが作成され、後続のアップグレードタスクがより迅速に実行されます。また、アップグレード完了後に、オンラインでのリビジョンクリーンアップが正常に実行されるようになります。オフラインでのリビジョンクリーンアップの実行について詳しくは、[オフラインでのリビジョンクリーンアップの実行](/help/sites-deploying/revision-cleanup.md#revision-cleanuprevision-cleanup)を参照してください。

## データストアのガベージコレクションの実行 {#execute-datastore-garbage-collection}

CRX3 インスタンスでリビジョンクリーンアップを実行した後は、データストアのガベージコレクションを実行して、データストア内の参照されていない BLOB を削除する必要があります。手順については、[データストアのガベージコレクション](/help/sites-administering/data-store-garbage-collection.md)に関するドキュメントを参照してください。

## ログファイルのローテーション {#rotate-log-files}

アップグレードを開始する前に、現在のログファイルをアーカイブすることをお勧めします。これにより、アップグレード中やアップグレード後にログファイルを監視およびスキャンして、発生する可能性のある問題を特定および解決することが容易になります。
