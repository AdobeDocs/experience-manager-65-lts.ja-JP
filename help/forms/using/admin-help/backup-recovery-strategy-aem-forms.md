---
title: AEM forms のバックアップと回復方法
description: データをバックアップするための戦略を実装し、AEM Forms データと同期させる方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 2f34b48a-0b95-4994-ac4f-616620a5b211
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '1518'
ht-degree: 100%

---

# AEM forms のバックアップと回復方法{#backup-and-recovery-strategy-for-aem-forms}

AEM Forms の実装で、追加のカスタムデータを異なるデータベースに格納する場合、そのカスタムデータをバックアップするための戦略を実装し、AEM Forms データと同期させる必要があります。また、追加のデータベースを同期しないシナリオにも対処できるように、アプリケーションを堅牢な方法で設計する必要があります。一貫性のある状態を維持するために、実行するデータベース操作をトランザクションコンテキストで行うことを強くお勧めします。

AEM Forms の使用方法を特定したら、バックアップの必要があるファイル、バックアップの頻度、使用可能にするバックアップウィンドウを決定します。

>[!NOTE]
>
>AEM Forms 実装の他の側面と同様に、バックアップと回復の戦略は、実稼動環境で使用する前に開発環境またはステージング環境で作成およびテストし、データ損失が発生せずにソリューション全体が期待どおり機能することを確認する必要があります。

Adobe Experience Manager（AEM）は AEM Forms の統合機能の一部です。したがって、Correspondence Management Solution とサービス（例えば Forms Manager）は AEM Forms の AEM 部分に保存されているデータを基にしているので、AEM のバックアップを取ることと、AEM Forms バックアップと同期することが必要です。データの喪失を防ぐために、AEM Forms 固有データのバックアップを何らかの方法で取り、GDS および AEM（リポジトリ）をデータベースリファレンスと相関させる必要があります。データベース、GDS、AEM、および Content Storage Root ディレクトリは、元と同じ DNS 名でコンピューターに復元する必要があります。

## バックアップの種類 {#types-of-backups}

AEM Forms のバックアップ戦略には、次の 2 種類のバックアップがあります。

**システムイメージ：**&#x200B;ハードドライブまたはコンピューター全体の機能が停止した場合に、コンピューターの内容を復元するのに使用できる完全なシステムバックアップ。システムイメージバックアップは、AEM Forms の実稼動用デプロイメントより前にのみ必要です。社内ポリシーで、システムイメージバックアップが必要な頻度を示します。

**AEM Forms 固有のデータ：**&#x200B;アプリケーションデータは、データベース、グローバルドキュメントストレージ（GDS）、AEM リポジトリに存在し、リアルタイムにバックアップされる必要があります。GDS は、プロセス内で使用される長期間有効なファイルの保存に使用されるディレクトリです。該当するファイルには、PDF、ポリシー、フォームテンプレートなどがあります。

>[!NOTE]
>
>Content Services（非推奨）をインストールする場合、コンテンツ保存場所のルートディレクトリもバックアップします。[コンテンツ保存場所のルートディレクトリ（Content Services のみ）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only)を参照してください。

データベースは、フォームの生成結果、サービス設定、プロセスの状態、および GDS ファイルへのデータベース参照を保存するために使用されます。データベースへのドキュメントの保存を有効にすると、GDS 内の永続データと永続ドキュメントもデータベースに保存されます。データベースは、次の方法でバックアップおよび回復できます。

* **スナップショットバックアップ**&#x200B;モードでは、AEM Forms システムが無制限にバックアップモードになるか、または指定された時間（分）だけバックアップモードになり、その時間が経過するとバックアップモードが無効になります。スナップショットバックアップモードを開始または終了するには、次のいずれかのオプションを使用します。回復シナリオの後、スナップショットバックアップモードは有効になりません。

   * 管理コンソールのバックアップ設定ページを使用します。スナップショットモードを開始するには、「セーフバックアップモードで稼動する」チェックボックスをオンにします。スナップショットモードを終了するには、このチェックボックスの選択を解除します。
   * LCBackupMode スクリプト（[データベース、GDS およびコンテンツ保存場所のルートディレクトリのバックアップ](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)を参照）を使用します。スナップショットバックアップモードを終了するには、スクリプトの引数で `continuousCoverage` パラメーターを `false` に設定するか、`leaveContinuousCoverage` オプションを使用します。
   * 提供されたバックアップ／リカバリ API を使用します。<!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **ローリングバックアップ**&#x200B;モードでは、システムが常にバックアップモードになり、前のセッションが解放されるとすぐに新しいバックアップモードセッションが初期化されます。ローリングバックアップモードにはタイムアウトは関連付けられません。LCBackupMode スクリプトまたは API を呼び出してローリングバックアップモードを終了すると、新しいローリングバックアップモードセッションが開始します。このモードでは継続的なバックアップがサポートされ、GDS ディレクトリから古いドキュメントや不要なドキュメントを消去できるので便利です。ローリングバックアップモードは、「バックアップと回復」ページではサポートされません。回復シナリオの後、ローリングバックアップモードは引き続き有効になります。継続的なバックアップモード（ローリングバックアップモード）を終了するには、LCBackupMode スクリプトで `leaveContinuousCoverage` オプションを使用します。

>[!NOTE]
>
>ローリングバックアップモードを終了すると、すぐに新しいバックアップモードセッションが開始します。ローリングバックアップモードを完全に無効にするには、スクリプトで `leaveContinuousCoverage` オプションを使用します。これによって、既存のローリングバックアップセッションが上書きされます。スナップショットバックアップモードでは、バックアップモードを通常の操作と同じように終了できます。

データ損失を防ぐために、AEM Forms 固有のデータは、GDS およびコンテンツ保存場所のルートディレクトリのドキュメントがデータベース参照と関連付けられるような方法でバックアップする必要があります。

>[!NOTE]
>
>GDS がデータベース内ではなく、ファイルシステムに保存されている場合は、GDS バックアップの前にデータベースバックアップを実行します。

## バックアップと回復に関する考慮事項 {#special-considerations-for-backup-and-recovery}

AEM Forms を異なる環境に回復する場合、次のような変更点があるので、ここで説明するガイドラインに従ってください。

* AEM Forms サーバーの IP アドレス、ホスト名またはポートの変更
* ドライブ文字またはディレクトリパスの変更
* 異なるデータベースのホスト、ポートまたは名前への変更

通常、このような回復シナリオは、アプリケーションサーバー、データベースサーバーまたは Forms サーバーをホストするサーバーのハードウェアエラーにより発生します。AEM Forms サーバーのホスト名または IP アドレスが変わる場合、ここで説明する AEM Forms 固有の設定に加え、必要に応じて、ロードバランサーやファイアウォールなど AEM Forms デプロイメントの他の部分についても変更する必要があります。

### 変更できないもの {#what-cannot-be-changed}

バックアップから AEM Forms を回復するとき、データベースサーバーや他の多くのパラメーターを変更できる場合でも、アプリケーションサーバーの種類とデータベースの種類は変更できません。例えば、AEM Forms バックアップを回復する場合、アプリケーションサーバーを JBoss から WebLogic に変更することや、データベースを Oracle から DB2 に変更することはできません。さらに、回復した AEM Forms では、フォントディレクトリなど、同じファイルシステムパスを使用する必要があります。

### 回復後の再起動 {#restarting-after-a-recovery}

回復後に Forms サーバーを再起動する前に、次の手順を実行します。

1. メンテナンスモードでシステムを起動します。
1. 次の操作を実行して、Form Manager をメンテナンスモードで AEM Forms と同期させます。

   1. https://&lt;*サーバー*>:&lt;*ポート*>/lc/fm にアクセスし、管理者／パスワードの資格情報を使用してログインします。
   1. 右上隅にあるユーザーの名前（この場合は Super Administrator）をクリックします。
   1. 「**Admin Options**」をクリックします。
   1. 「**Start**」をクリックして、リポジトリのアセットを同期します。

1. クラスター環境では、AEM のプライマリノードはセカンダリノードよりも前に立ち上げる必要があります。
1. システムの通常処理が検証されるまで、web、SOAP、EJB のプロセスイニシエーターなど、内部ソースまたは外部ソースからプロセスが開始されないようにします。

メイン AEM Forms データベースを移動または変更した場合は、ご使用のアプリケーションサーバーに対応するインストールガイドを参照して、AEM Forms データソースの IDP_DS および EDC_DS のデータベース接続情報を更新します。

>[!NOTE]
> 
> 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

### AEM Forms のホスト名または IP アドレスの変更 {#changing-the-aem-forms-hostname-or-ip-address}

クラスター環境でキャッシュに UDP ではなく TCP を使用している場合、キャッシュロケーターの設定を更新する必要があります。ご使用のアプリケーションサーバーに対応する設定ガイドの「キャッシュロケーターの設定（TCP を使用するキャッシュのみ）」を参照してください。

### AEM Forms ノードのファイルシステムパスの変更 {#changing-the-aem-forms-node-file-system-paths}

スタンドアロンノードのファイルシステムパスを変更する場合、環境設定内の該当する参照、他のシステム設定、カスタムアプリケーションおよびデプロイされた AEM Forms アプリケーションを更新する必要があります。一方、クラスターの場合、すべてのノードに同じファイルシステムパス設定を使用する必要があります。また、グローバルドキュメントストレージ（GDS）のルートディレクトリを設定し、回復したデータベースと同期している回復した GDS のコピーを示すようにします。アプリケーションサーバーを再起動しても存続する必要があるデータが GDS に含まれる可能性があるので、GDS パスの設定は重要です。

クラスター環境では、リポジトリのファイルシステムパス設定は、バックアップの前と回復の後で、すべてのクラスターノードに対して同じでなければなりません。

ファイルシステムのパスを変更した後に GDS のパスを設定するには、`[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` フォルダーにある `LCSetGDS` スクリプトを使用します。詳しくは、同じフォルダー内の `ReadMe.txt` ファイルを参照してください。古い GDS ディレクトリパスを使用できない場合は、AEM forms を起動する前に、`LCSetGDS` スクリプトを使用して GDS に新しいパスを設定する必要があります。

>[!NOTE]
>
>この状況は、このスクリプトを使用して GDS の場所を変更する必要がある唯一の状況です。AEM Forms の実行中に GDS の場所を変更するには、管理コンソールを使用します。（[一般的な AEM Forms の設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)を参照）。

GDS パスの設定後、メンテナンスモードで Forms サーバーを起動し、管理コンソールを使用して、新しいノードについて残りのファイルシステムパスを更新します。すべての必要な設定が更新されたことを確認してから、AEM Forms を再起動し、テストします。
