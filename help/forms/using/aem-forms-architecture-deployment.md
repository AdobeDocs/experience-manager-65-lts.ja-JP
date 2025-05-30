---
title: AEM Forms のアーキテクチャとデプロイメントトポロジー
description: AEM Forms のアーキテクチャ詳細と、新規または継続で AEM をご利用になるお客様および LiveCycle ES4 からアップグレードしたお客様向けに推奨されるトポロジー。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
exl-id: 23ffbaa6-1bd9-48c3-afa3-19737bb15de0
source-git-commit: 060bb23d64a90f0b2da487ead4c672cbf471c9a8
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 95%

---

# AEM Forms のアーキテクチャとデプロイメントトポロジー {#architecture-and-deployment-topologies-for-aem-forms}

| バージョン | 記事リンク |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [ここをクリックしてください](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture.html?lang=ja) |
| AEM 6.5 | この記事 |

## アーキテクチャ {#architecture}

AEM Formsは、1 つの AEMパッケージとして AEM にデプロイされるアプリケーションです。このパッケージは、AEM Forms アドオンパッケージと呼ばれます。AEM Forms アドオンパッケージには、AEM OSGi コンテナに読み込まれるサービス（API プロバイダー）と、AEM Sling フレームワークで管理されるサーブレットまたは JSP（フロントエンド機能と REST API 機能の両方を提供）が含まれています。次の図は、このセットアップを示しています。

![アーキテクチャ](assets/architecture.png)

AEM Forms のアーキテクチャには、次のコンポーネントが含まれています。

* **AEM のコアサービス：**&#x200B;デプロイされたアプリケーションに対して提供される AEM の基本サービス。これらのサービスには、JCR に準拠したコンテンツリポジトリ、OSGI サービスコンテナ、ワークフローエンジン、トラストストア、キーストアなどがあります。これらのサービスは AEM Forms アプリケーションで使用できますが AEM Forms パッケージには含まれていません。これらのサービスは、AEM Forms の様々なコンポーネントで使用される、AEM スタック全体の不可欠な構成要素です。
* **Forms サービス：** PDF ドキュメントの作成、アセンブリ、配布、アーカイブなどのフォーム関連の機能を提供し、デジタル署名を追加してドキュメントへのアクセスを制限し、バーコードフォームをデコードします。これらのサービスは、AEM にカスタムコードを組み込んで利用する形で公開されています。
* **Web レイヤー：**&#x200B;共通のサービスおよびフォームのサービス上に構築された JSP またはサーブレットで、次の機能を提供します。

   * **フロントエンドのオーサリング**：フォームのオーサリングと管理に使用されるユーザーインターフェイス。
   * **フォームのレンディションおよび送信のフロントエンド**：AEM Forms のエンドユーザー向けユーザーインターフェイス（行政機関の web サイトにアクセスするユーザー向けのユーザーインターフェイスなど）。これにより、フォームのレンディション（web ブラウザーでのフォームの表示）と送信を行うことができます。
   * **REST API**：JSP および サーブレットにより、モバイル SDK フォームなど、HTTP ベースのクライアントによるリモートでの利用向けにフォームサービスのサブセットがエクスポートされます。

**AEM Forms on OSGi：** OSGi 環境上の AEM Forms は、AEM Forms パッケージがデプロイされた標準の AEM オーサーまたは AEM パブリッシュです。OSGi 上の AEM Forms は、[単一サーバー環境、ファーム設定、クラスター設定](/help/sites-deploying/recommended-deploys.md)で実行できます。クラスターを設定できるのは、AEM オーサーインスタンスの場合だけです。

<!--

**AEM Forms on JEE:** AEM Forms on JEE is AEM Forms server running on JEE stack. It has AEM Author with AEM Forms add-on packages and additional AEM Forms JEE capabilities co-deployed on a single JEE stack running on an application server. You can run AEM Forms on JEE in single-server and clustered setups. AEM Forms on JEE is required only to run document security, process management, and for LiveCycle customers upgrading to AEM Forms. Here are a few additional scenarios to use AEM Forms on JEE:

* **HTML workspace support (for customers using HTML workspace):** AEM Forms on JEE enables single sign-on with Processing instances, serves certain assets rendered on Processing instances, and handles submission of forms rendered within the HTML workspace.
* **Advanced additional form/interactive communication data processing**: AEM Forms on JEE can be utilized for additionally processing form/interactive communication data (and saving the results to a suitable data store) in complex use-cases where advanced process-management capabilities are required.

AEM Forms on JEE also includes provides following supporting services to the AEM components:

* **Integrated user management:** Allows users of AEM Forms on JEE to be recognized as AEM forms on OSGi users and helps enable SSO for both OSGi and JEE users. This is required for scenarios where single sign-on between AEM forms on OSGi and AEM Forms on JEE is required (for example, HTML workspace).
* **Asset hosting:** AEM Forms on JEE can serve assets (for example, HTML5 forms) rendered on AEM Forms on OSGi.

-->

AEM Forms オーサリングユーザーインターフェイスは、レコードのドキュメント（DOR）、PDF forms、HTML5 Forms の作成をサポートしていません。このようなアセットは、スタンドアロンのForms Designer アプリケーションを使用して設計され、AEM Forms Manager に個別にアップロードされます。<!--Alternatively, for AEM Forms on JEE, forms can be designed as application (in AEM Forms Workbench) assets and deployed into AEM Forms on JEE server.-->

OSGi 上のAEM Formsにはワークフロー機能 <!--and AEM Forms on JEE both--> 備わっています。 OSGi.<!--, without having to install the full-fledged Process Management capability of AEM Forms on JEE. There is some difference in the [features of Form-centric workflow on AEM Forms on OSGi and Process Management capability of AEM Forms on JEE](capabilities-osgi-jee-workflows.md). The development and management of Form-centric workflows on AEM Forms on OSGi uses the familiar AEM Workflow and AEM Inbox capabilities.--> 上のAEM フォームでは、様々なタスクに対する基本的なワークフローを迅速に構築し、デプロイできます。

## 用語 {#terminologies}

以下の図は、AEM Forms の一般的なデプロイメント環境で使用される AEM Forms サーバーの様々な設定とそのコンポーネントを示しています。

![aem_forms_-_recommendedtopology](assets/aem_forms_-_recommendedtopology.png)

**オーサー：**&#x200B;オーサーインスタンスは、標準のオーサー実行モードで稼働する AEM Forms サーバーです。<!--It can be AEM Forms on JEE or AEM Forms on OSGi environment.--> 内部ユーザー、フォームおよびインタラクティブ通信のデザイナー、開発者を対象としています。 次の機能が有効になります。

* **フォームとインタラクティブ通信の作成機能と管理機能：**&#x200B;設計者と開発者は、アダプティブフォームやインタラクティブ通信の作成および編集したり、外部で作成された他のタイプのフォームをアップロードしたりできます。例えば、Adobe Forms Designer で作成されたフォームなど、Forms Manager コンソールを使用してこれらのアセットを管理します。
* **フォームとインタラクティブ通信の公開機能：**&#x200B;オーサーインスタンス上でホストされるアセットをパブリッシュインスタンスに公開して、ランタイム操作を実行することができます。AEM のレプリケーション機能を使用して、アセットが公開されます。パブリッシュしたフォームを処理インスタンスに手動でプッシュするために、レプリケーションエージェントをすべてのオーサーインスタンス上で設定すること、および受信したフォームをパブリッシュインスタンスに自動で複製するために、別のレプリケーションエージェントを&#x200B;*受信時*&#x200B;トリガーが有効になっている処理インスタンス上で設定することをお勧めします。

**パブリッシュ：**&#x200B;パブリッシュインスタンスは、標準のパブリッシュ実行モードで稼働する AEM Forms サーバーです。パブリッシュインスタンスは、フォームベースのアプリケーションを使用するエンドユーザー向けのインスタンスです。例えば、公開 web サイトにアクセスしてフォームを送信するユーザーなどが、このインスタンスを使用します。次の機能が有効になります。

* エンドユーザー用のフォームのレンダリングと送信。
* 送信済みフォームの生データを処理インスタンスに転送してさらに処理を行い、最終的な記録システムに保存する機能。AEM Forms に付属するデフォルトの実装では、AEM のリバースレプリケーション機能を使用してこれを実現します。代替の実装として、最初にフォームデータをローカルに保存するのではなく、フォームデータを処理インスタンスに直接プッシュすることもできます（後者はリバースレプリケーションをアクティベートするための前提条件です）。通常、処理インスタンスはパブリッシュインスタンスよりも安全な場所に配置されるため、顧客が機密データをパブリッシュインスタンスに保存することに不安を感じている場合は、上記の[代替実装](/help/forms/using/configuring-draft-submission-storage.md)を実行してもかまいません。
* インタラクティブ通信とレターのレンダリングと送信：インタラクティブ通信とレターはパブリッシュインスタンス上でレンダリングされ、対応するデータがストレージと後処理用に処理インスタンスに送信されます。このデータは、パブリッシュインスタンスにローカルで保存して、処理インスタンスに逆複製すること（デフォルトのオプション）も、処理インスタンスに直接プッシュして、パブリッシュインスタンスには保存しないこともできます。セキュリティを意識している顧客の場合は、後者の実装をお勧めします。

**処理：** forms-manager グループにユーザーが割り当てられていない状態の作成者実行モードで実行される AEM Forms のインスタンスです。OSGi 上 <!--AEM Forms on JEE or-->AEM Formsを処理インスタンスとしてデプロイできます。 ユーザーが割り当てられていない場合、フォームのオーサリングと管理のアクティビティは、処理インスタンスで実行されることはなく、オーサーインスタンスでのみ実行されます。処理インスタンスでは、次の機能が有効になります。

* **パブリッシュインスタンスから送信された未加工のフォームデータの処理：**&#x200B;この機能は、データの到着時にトリガーされる AEM ワークフロー経由の処理インスタンスで主に実現されます。このワークフローでは、標準搭載の「フォームデータモデル」の手順を使用して、データまたはドキュメントを適切なデータストアにアーカイブできます。
* **フォームデータの安全な保存**：処理インスタンスには、ファイアウォールの背後に配置されたリポジトリが用意されています。未加工のフォームデータは、このリポジトリに保存することにより、ユーザーから隔離できます。オーサーインスタンス上の設計者も、パブリッシュインスタンス上のエンドユーザーも、このリポジトリにアクセスすることはできません。

  >[!NOTE]
  >
  >アドビは、AEM リポジトリを使用する代わりに、サードパーティのデータストアを使用して、最終的に処理されたデータを保存することをお勧めします。

* **パブリッシュインスタンスから送信された通信データの保存と後処理：** AEM ワークフローは、対応するレター定義の後処理をオプションで実行します。これらのワークフローで、最終的な処理済みデータを、適切な外部データストアに保存することができます。

* **HTML ワークスペースのホスティング**：処理インスタンスは、HTML ワークスペースのフロントエンドをホストします。HTML ワークスペースは、レビューと承認のプロセスに関連するタスクやグループを割り当てるための UI を提供します。

次の理由から、処理インスタンスは、オーサー実行モードで稼働するように設定されています。

* パブリッシュインスタンスから未加工のフォームデータを逆複製できます。デフォルトのデータストレージハンドラーを使用するには、逆複製機能が必要になります。
* AEM ワークフローは、パブリッシュインスタンスから送信される未加工のフォームデータの主要な処理手段であるため、オーサースタイルのシステムで AEM ワークフローを実行することをお勧めします。

<!--

## Sample physical topologies for AEM Forms on JEE {#sample-physical-topologies-for-aem-forms-on-jee}

The AEM Forms on JEE topologies recommended below are mainly for customers upgrading from LiveCycle or a previous version of AEM Forms on JEE. Adobe recommends using AEM Forms on OSGi for fresh installations. A fresh installation of AEM Forms on JEE only recommended for using Document Security and Process Management capabilities.

### Topology for using document services or document security capabilities {#topology-for-using-document-services-or-document-security-capabilities}

AEM Forms customers planning to use only document services or document security capabilities can have a topology similar to the one displayed below. This topology recommends using a single instance of AEM Forms. You can also create a cluster or farm of AEM Forms servers, if necessary. This topology is recommended when most users programmatically access capabilities of AEM Forms server and intervention through the user interface is minimum. The topology is helpful in batch processing operations of document services. For example, using output service to create hundreds of non-editable PDF documents on daily basis.

Although, AEM Forms lets you set up and run all the functionalities from a single server, yet, you should do capacity planning, load balancing, and set up dedicated servers for specific capabilities in a production environment. For example, for an environment using the PDF Generator service to convert thousands of pages a day and add digital signatures to limit access to documents, set up separate AEM Forms servers for the PDF Generator service and digital signature capabilities. It helps provide optimum performance and scale the servers independent of each other.

![basic-features](assets/basic-features.png)

### Topology for using AEM Forms process management {#topology-for-using-aem-forms-process-management}

AEM Forms customers planning to use AEM Forms process management features, for example, HTML Workspace can have a topology similar to the one displayed below. The AEM Forms on JEE server can be in a single server or cluster configuration.

If you are upgrading from LiveCycle ES4, this topology closely mirrors with what you already have in LiveCycle except for the addition of AEM Author built-in to AEM Forms on JEE. Moreover, there is no change in the clustering requirements for customers performing an upgrade. If you were using AEM Forms in a clustered environment, you can continue with same in AEM 6.5 Forms. For a fresh installation of AEM Forms of JEE for using HTML Workspace, running AEM author instance built-in to the JEE environment is an additional requirement.

Form data store is a third-party data store used for storing final processed data of forms and interactive communications. This is an optional element in the topology. You can also choose to set up a processing instance and use its repository as the final system-of-record system, if necessary.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

The topology is recommended to the customers planning to use AEM Forms on JEE server for process management capabilities (HTML Workspace) without using any post-processing, adaptive forms, HTML5 forms, and interactive communication capabilities.

### Topology for using adaptive forms, HTML5 forms, interactive communication capabilities {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

AEM Forms customers planning to use AEM Forms data capture capabilities, for example, adaptive forms, HTML5 Forms, PDF Forms, can have a topology similar to the one displayed below. This topology is also recommended for using interactive communication capabilities of AEM Forms.

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

You can make the following changes/customizations to the above-suggested topology:

* Using HTML Workspace and AEM Forms app requires an AEM author or processing instance. You can use the AEM author instance built-in to AEM Forms on JEE server instead of setting up an additional external AEM author server.
* An AEM Author or Processing instance is required only for Forms-centric workflows on OSGi, adaptive forms, forms portal, and interactive communication.
* interactive communication Agent UI is generally run within the organization. So, you can keep a publish server for Agent UI within the private network.
* AEM forms on OSGi instance built-in to AEM Forms on JEE server can also run Forms-centric workflows on OSGi and Watched Folders.

-->

## OSGi 上の AEM Forms を使用する場合の物理的なトポロジーの例 {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### データ取得機能、インタラクティブ通信機能、OSGi 上のフォーム中心ワークフロー機能を使用する場合のトポロジー {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

アダプティブフォーム、HTML5 フォーム、PDF フォームなど、AEM Forms のデータ取得機能を使用する場合は、以下のようなトポロジーを構成することをお勧めします。インタラクティブ通信機能と OSGi 上のフォームベースワークフロー機能を使用する場合も、このトポロジーを構成することをお勧めします。例えば、ビジネスプロセスワークフローで AEM インボックスと AEM Forms アプリケーションを使用する場合などです。

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### オフラインのバッチ処理で監視フォルダー機能を使用する場合のトポロジ {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

バッチ処理に監視フォルダーの使用を計画している AEM Forms のお客様は、以下に示すようなトポロジーを構成することができます。このトポロジーではクラスター環境が構成されていますが、AEM Forms サーバーを 1 つのインスタンスで使用するか、ファームで使用するかは、負荷に応じて決定します。サードパーティ製のデータソースを、専用の記録システムとして使用することになります。このデータソースが、監視フォルダーの入力元になります。トポロジでは、印刷ファイルの形式で出力も表示されます。また、出力コンテンツをファイルシステムに保存し、メールで送信し、他のカスタムメソッドを使用して出力を使用することもできます。

![offline-batch-processing-via-watched-folders](assets/offline-batch-processing-via-watched-folders.png)

### API ベースのオフライン処理でドキュメントサービス機能を使用する場合のトポロジ {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

ドキュメントサービス機能のみの使用を計画している AEM Forms のお客様は、以下に示すようなトポロジを構成することができます。このトポロジでは、OSGi サーバー上で AEM Forms のクラスターを使用することをお勧めします。多くのユーザーがプログラムで（API を使用して）AEM Forms サーバーの機能にアクセスし、ユーザーインターフェイス上ではほとんど操作を実行しない場合は、このトポロジを構成することをお勧めします。複数のソフトウェアクライアントを使用する場合は、このトポロジを構成すると非常に便利です。例えば、PDF Generator サービスを使用する複数のクライアントにより、オンデマンドで PDF ドキュメントを作成するような場合です。

AEM Forms では、すべての機能を 1 台のサーバーで設定して実行できますが、実稼働環境ではキャパシティプラニングと負荷分散を行い、特定の機能に専用のサーバーをセットアップする必要があります。例えば、PDF Generator サービスを使用して、1 日に数千のページと複数のアダプティブフォームをデータ取得用に変換する環境の場合、PDF Generator サービスとアダプティブフォームの機能を実行するための AEM Forms サーバーを個別にセットアップする必要があります。これにより、パフォーマンスが最適化され、各サーバーを個別にスケーリングできるようになります。

![offline-api-based-processing](assets/offline-api-based-processing.png)
