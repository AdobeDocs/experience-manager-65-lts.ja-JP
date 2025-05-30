---
title: バージョンのパージ
description: この記事では、バージョンのパージで使用できるオプションについて説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
solution: Experience Manager, Experience Manager Sites
role: Admin
hide: true
hidefromtoc: true
exl-id: e3ef1435-d405-482f-9eb5-f9a64ff03322
source-git-commit: f145e5f0d70662aa2cbe6c8c09795ba112e896ea
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 100%

---

# バージョンのパージ{#version-purging}

標準インストールの場合、コンテンツの更新後にページをアクティベートすると、Adobe Experience Manager（AEM）によってページまたはノードのバージョンが作成されます。

>[!NOTE]
>
>コンテンツが変更されない場合は、ページがアクティベート済みで、新しいバージョンが作成されないことを示すメッセージが表示されます。

サイドキックの「**バージョン管理**」タブを使用すると、リクエストに応じて追加のバージョンを作成できます。これらのバージョンはリポジトリに格納され、必要に応じて復元できます。

これらのバージョンはパージされることがなく、時間の経過と共にリポジトリーのサイズが大きくなるので、管理が必要です。

AEM には、リポジトリの管理に役立つ様々なメカニズムが備わっています。

* [バージョンマネージャー](#version-manager)
新しいバージョンが作成されると古いバージョンをパージするように設定できます。

* [バージョンのパージ](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)ツール
リポジトリの監視と保守の一部で使用されます。
このツールを使用すると、次のパラメーターに従って、ノードの古いバージョンまたはノードの階層を削除するためにユーザーが介入できます。

   * リポジトリに保持するバージョンの最大数
この数値を超えると、最も古いバージョンが削除されます。

   * リポジトリに保持するバージョンの期間の最大値
バージョンの期間がこの値を超えると、リポジトリからパージされます。

* [バージョンパージのメンテナンスタスク](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks)。バージョンのパージメンテナンスタスクをスケジュールして、古いバージョンを自動的に削除できます。これにより、バージョンのパージツールを手動で実行する必要性を最小限に抑えることができます。

>[!CAUTION]
>
>リポジトリサイズを最適化するには、バージョンのパージタスクを頻繁に実行します。トラフィック量が限られている場合は、このタスクを営業時間外にスケジュールする必要があります。

## バージョンマネージャー {#version-manager}

パージツールを使用した明示的なパージに加えて、新しいバージョンの作成時に古いバージョンをパージするようにバージョンマネージャーを構成できます。

バージョンマネージャーを設定するには、次の[設定を作成](/help/sites-deploying/configuring-osgi.md)します。

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

以下のオプションが利用できます。

* `versionmanager.createVersionOnActivation`（ブール値、デフォルト：true）
ページがアクティベートされた際に、バージョンを作成するかどうかを指定します。
レプリケーションエージェントがバージョンの作成を抑制するように設定されていない限り、バージョンが作成されます。これはバージョンマネージャーで順守されます。
アクティベーションが `versionmanager.ivPaths` に含まれているパスで行われた場合にのみバージョンが作成されます（以下を参照）。

* `versionmanager.ivPaths`（String[]、デフォルト：`{"/"}`）
`versionmanager.createVersionOnActivation` が true の場合に、アクティベーションによりバージョンが暗黙的に作成されるパスを指定します。

* `versionmanager.purgingEnabled`（ブーリアン、デフォルト：false）
新しいバージョンの作成時にパージを有効にするかどうかを定義します。

* `versionmanager.purgePaths`（文字列[]、デフォルト：{&quot;/content&quot;}）
新しいバージョンの作成時にバージョンをパージするパスを指定します。

* `versionmanager.maxAgeDays`（整数、デフォルト：30）
バージョンパージで、設定した値より古いバージョンが削除されます。この値が 1 未満の場合、バージョンの期間に基づいたパージは実行されません。

* `versionmanager.maxNumberVersions`（整数、デフォルト：5）
バージョンパージで、n 番目に新しいバージョンより古いバージョンが削除されます。この値が 1 未満の場合、バージョンの数に基づいたパージは実行されません。

* `versionmanager.minNumberVersions`（整数、デフォルト：0）
期間にかかわらず保持するバージョン数の最小数。この値を 1 未満に設定すると、保持するバージョン数の最小数は設定されません。

>[!NOTE]
>
>リポジトリに多数のバージョンを保存することはお勧めできません。そのため、バージョンのパージ操作を設定する際は、パージ対象から多くのバージョンを除外しすぎないでください。そうしないと、リポジトリサイズが適切に最適化されません。業務上の要件で多数のバージョンを保持する場合は、アドビサポートに連絡して、リポジトリサイズを最適化する代替方法をご相談ください。

### 保持オプションの組み合わせ {#combining-retention-options}

どのバージョンを保持するかを定義するオプション（`maxAgeDays`、`maxNumberVersions`、`minNumberVersions`）は、要件に応じて組み合わせることができます。

例えば、保持するバージョンの最大数と保持する最も古いバージョンを組み合わせて定義する場合は、次のようになります。

* 設定:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* シナリオは以下の通りです。

   * 過去 60 日以内に 10 個のバージョンが作成されました。
   * そのうちの 3 個が過去 30 日以内に作成されました。

* 結果は次の通りです。

   * 最新の 3 個のバージョンが保持されます。

例えば、保持するバージョン数の最大数と最小数、および保持する最も古いバージョンを組み合わせて定義する場合は、次のようになります。

* 設定:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* シナリオは以下の通りです。

   * 60 日前に 5 個のバージョンが作成されました。

* 結果は次の通りです。

   * 最新の 3 個のバージョンが保持されます。

## バージョンのパージツール {#purge-versions-tool}

[バージョンのパージ](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)ツールを使用すると、リポジトリ内のノードまたはノードの階層のバージョンをパージすることができます。このツールの主な目的は、古いバージョンのノードを削除してリポジトリのサイズを縮小することです。
