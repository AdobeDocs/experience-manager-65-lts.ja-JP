---
title: 技術要件
description: Adobe Experience Manager でサポートされるクライアントおよびサーバープラットフォームのリスト。
topic-tags: platform
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: f65dd129-9e28-4de1-acca-dd31eaf3c19b
source-git-commit: 7d40e37a29a426e0e72b233b3aab56b1ba6f1730
workflow-type: tm+mt
source-wordcount: '2870'
ht-degree: 91%

---

# 技術要件{#technical-requirements}

アドビは、このドキュメントの以下の情報に記載されているプラットフォームで、Adobe Experience Manager（AEM）をサポートしています。

プラットフォームに関連する問題については、プラットフォームのベンダーにお問い合わせください。

>[!NOTE]
>
>AEM をインストールするプラットフォームに応じて、ユーザー管理に関する一連の要件が異なる場合があります。

## 前提条件 {#prerequisites}

Adobe Experience Manager をインストールするための最小要件

* Java™ Platform, Standard Edition JDK または他のサポートされている [Java™ 仮想マシン](#java-virtual-machines)がインストールされていること
* Experience Manager Quickstart ファイル（スタンドアロン JAR または web アプリケーションデプロイメント WAR）

### 最小サイズ要件 {#minimum-sizing-requirements}

 Adobe Experience Manager を実行するための最小要件：

* 5 GB の空きディスク領域（インストールディレクトリ内）
* 2 GB メモリ

>[!NOTE]
>
>* デジタルアセットのユースケースには、より多くのベースメモリが必要です。詳しくは、「[デプロイと保守](/help/sites-deploying/deploy.md#default-local-install)」を参照してください。
>* [AEM Forms アドオンパッケージ](/help/forms/using/installing-configuring-aem-forms-osgi.md)には 15 GB の一時領域が必要です。
>

詳しくは、「[ハードウェアのサイズ設定のガイドライン](/help/managing/hardware-sizing-guidelines.md)」を参照してください。

### サポートレベル {#support-levels}

このドキュメントには、Adobe Experience Manager でサポートされるクライアントおよびサーバーのプラットフォームが一覧化されています。アドビでは、推奨設定とその他の設定の両方について、複数のレベルのサポートを提供しています。

### サポートされる設定 {#supported-configurations}

アドビは以下の構成を推奨し、標準ソフトウェア保守契約の一環として完全なサポートを提供しています。

<table>
 <tbody>
  <tr>
   <td>サポートレベル</td>
   <td>説明<br /> </td>
  </tr>
  <tr>
   <td><strong>A：サポート対象</strong></td>
   <td>アドビはこの構成への完全なサポートと保守を提供します。この構成は、アドビの品質保証プロセスでカバーされます。</td>
  </tr>
  <tr>
   <td><strong>R：制限サポート</strong></td>
   <td>お客様のプロジェクトを確実に成功させるために、アドビは特定の条件を満たす必要がある限定的なサポートプログラム内で、完全なサポートを提供します。R レベルのサポートでは、正式なお客様のリクエストとアドビの確認が必要です。詳しくは、アドビカスタマーケアにお問い合わせください。</td>
  </tr>
 </tbody>
</table>

### サポートされていない設定 {#unsupported-configurations}

| サポートレベル | 説明 |
|---|---|
| **Z：サポート対象外** | この設定はサポートされていません。アドビは、この設定が動作するかどうかに関する一切の表明をせず、この設定をサポートしません。 |

## サポートされているプラットフォーム {#supported-platforms}

### Java™ 仮想マシン {#java-virtual-machines}

このアプリケーションを実行するには、Java™ 仮想マシンを必要とし、Java™ デベロップメントキット（JDK）の配布で提供されます。

Adobe Experience Manager は、次のバージョンの Java™ 仮想マシンで動作します。

>[!CAUTION]
>
>Java™ ベンダーからのセキュリティ情報をトラックします。これにより、本番環境の安全性とセキュリティが確保されます。また、常に最新の Java™ アップデートをインストールしてください。

| **プラットフォーム** | **サポートレベル** | **リンク** |
|---|---|---|
| Oracle Java™ SE 17 JDK | A：サポート対象 `[1]` |
| Oracle Java™ SE 21 JDK | A：サポート対象 `[1]` |
| IBM® Semeru J9 VM - ビルド 17.0.13.0 | A：サポート対象 `[2]` |
| IBM® Semeru J9 VM - ビルド 21.0.6.0 | A：サポート対象 `[2]` |

1. Oracle は Oracle Java™ SE 製品の「長期サポート」（LTS）モデルに移行しました。Java™ 9、Java™ 10、Java™ 12、Java™ 13、Java™ 14、Java™ 15m Java™ 16 は、Oracleによる非 LTS でのリリースです（[Oracle Java™ SE サポートロードマップ &#x200B;](https://www.oracle.com/jp/technetwork/java/eol-135779.html) を参照）。 本番環境に AEM をデプロイするために、アドビでは LTS リリース版の Java™ のみサポートします。LTS リリースのすべてのメンテナンスアップデートを含むOracle Java™ SE JDK のサポートと配布が、Adobeによって直接サポートされます。対象となるのは、Oracle Java™ SE テクノロジーを使用するすべてのAEM ユーザーです。 詳しくは、[Adobe Experience Manager 用 Java™ サポートポリシー](assets/Java_Policy_for_Adobe_Experience_Manager.pdf)を参照してください。
   **このリリースでは、Oracle Java™ 17 およびOracle Java™ 21.** がサポートされています

1. IBM® JRE は、WebSphere® Application Server と共に使用する場合にのみサポートされます。

### ストレージと永続性 {#storage-persistence}

Adobe Experience Manager のリポジトリをデプロイするには、様々なオプションがあります。次のリストに、サポートされるテクノロジーとストレージのオプションを示します。

| **プラットフォーム** | **説明** | **サポートレベル** |
|---|---|---|
| **TAR ファイルを使用したファイルシステム** `[1]` | リポジトリ | A：サポート対象 |
| **データストアを使用したファイルシステム** `[1]` | バイナリ | A：サポート対象 |
| ファイルシステムの TAR ファイルへのバイナリの格納 `[1]` | バイナリ | Z：実稼動環境ではサポートされていません |
| Amazon S3 | バイナリ | A：サポート対象 |
| Microsoft® Azure Blob Storage | バイナリ | A：サポート対象 |
| MongoDB Enterprise 8.0 | リポジトリ | A：サポート対象 `[2, 3]` |
| MongoDB Enterprise 7.0 | リポジトリ | A：サポート対象 `[2, 3]` |
| MongoDB Enterprise 6.0 | リポジトリ | A：サポート対象 `[2, 3]` |
| **Apache Lucene（Quickstart ビルトイン）** | 検索サービス | A：サポート対象 |

1. 「ファイルシステム」には、POSIX に準拠したブロックストレージが含まれます。ネットワークストレージテクノロジーが含まれます。ファイルシステムのパフォーマンスは異なり、全体的なパフォーマンスに影響を与える場合があることに注意してください。ネットワーク／リモートファイルシステムを使用してテスト AEM を読み込みます。
1. MongoDB Sharding は AEM ではサポートしていません。
1. MongoDB Storage Engine WiredTiger のみがサポートされています。

>[!NOTE]
>
>MongoDB はサードパーティのソフトウェアで、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB ライセンスポリシー](https://www.mongodb.com/licensing/server-side-public-license/faq)のページを参照してください。
>
>MongoDB を使用した AEM のデプロイメントを最大限に活用するには、プロフェッショナルサポートを受けられるように MongoDB Enterprise バージョンのライセンスを取得することをお勧めします。詳しくは、「[推奨されるデプロイメント](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk)」を参照してください。
>
>ライセンスには、標準レプリカセットが含まれています。このセットは、1 つのプライマリインスタンスと 2 つのセカンダリインスタンスで構成され、オーサーデプロイメントまたはパブリッシュデプロイメントのどちらかに使用できます。
>
>MongoDB でオーサーとパブリッシュの両方を実行したい場合は、2 つのライセンスを個別に購入する必要があります。
>
>アドビカスタマーケアは、MongoDB を AEM で利用することに関連する問題の絞り込みを支援いたします。
>
>詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。

### サーブレットエンジン／アプリケーションサーバー {#servlet-engines-application-servers}

Adobe Experience Manager は、スタンドアロンサーバー（Quickstart JAR ファイル）として、またはサードパーティのアプリケーションサーバー内の web アプリケーション（WAR ファイル）として実行できます。

サーブレット API の必要な最小バージョンは Servlet 3.1 です。さらに、AEM Formsは jar 用に Jakarta サーブレット 5 をサポートしており、war は Jakarta サーブレット API 5/6 を実装するアプリケーションサーバーにデプロイできます。

| Platform | サポートレベル |
|---|---|
| **Quickstart 組み込みサーブレットエンジン（Jetty 11.0.x）** | A：サポート対象 |
| IBM® WebSphere® Application Server Continuous Delivery （LibertyProfile）（Web Profile 24.0.0.7 およびIBM® Sumeru open JRE® 17/21） | R：新規契約向けの制限サポート `[1]` |
| Apache Tomcat 10.0.x/10.1.x | R：新規契約向けの制限サポート `[1]` |

1. アプリケーションサーバーで AEM 6.5 デプロイメントを開始すると、制限付きサポートに移行します。既存のお客様は AEM 6.5 にアップグレードして、引き続きアプリケーションサーバーを使用することができます。新規のお客様には、前述のレベル R の説明にあるサポート基準とサポートプログラムが適用されます。

### サーバーオペレーティングシステム {#server-operating-systems}

Adobe Experience Manager は、本番環境では次のサーバープラットフォームで動作します。

| **プラットフォーム** | **サポートレベル** |
|---|---|
| **Linux®（Red Hat® ディストリビューションに基づく）** | A：サポート対象 `[1]` `[2]` |
| Linux®、Debian ディストリビューションベース（Ubuntu | A：サポート対象 `[1]` |
| Linux®、SUSE® ディストリビューションベース | A：サポート対象 `[1]` |
| Microsoft® Windows Server 2022 | R：サポート対象 |

1. Linux® カーネル 5。 x および 6.x には Red Hat® ディストリビューションの派生 OS （Red Hat® Enterprise Linux®、CentOS、Oracle Linux®、Amazon Linux® など）が含まれます。
1. Adobe Managed Services でサポートされている Linux® ディストリビューション。

   >[!NOTE]
   >
   >Linux ベースのサーバーの場合、AEM Forms アドオンには、次のようなランタイム依存関係が必要です。
   >* glibc.x86_64（2.17-196）
   >* libX11.x86_64（1.6.7-4）
   >* zlib.x86-64（1.2.7-17）
   >* libxcb.x86_64（1.13-1.el7）
   >* libXau.x86_64（1.0.8-2.1.el7）
   >* glibc-locale.x86_64（2.17 以降）
   >* OpenSSL 3 （OS のデフォルトの場所で必要）

   *OpenSSL 3 のインストールの場合：ライブラリ libcrypto.so.3 および libssl.so.3 は、環境変数 LD_LIBRARY_PATH によって表されるデフォルトのライブラリパスで使用できる必要があります。それらが非標準の場所にインストールされている場合は、サーバーを起動する前に、このパスが LD_LIBRARY_PATH に追加されていることを確認してください。*

### 仮想／クラウドコンピューティング環境 {#virtual-cloud-computing-environments}

Adobe Experience Manager は、クラウドコンピューティング環境上の仮想マシンで動作する場合にサポートされます。これらの環境には、このページに記載されている技術要件およびアドビの標準サポート条件に従って動作する Microsoft® Azure や Amazon Web Services（AWS）が含まれています。

クラウドネイティブな環境の場合は、AEM 製品ラインの最新オファー、Adobe Experience Manager as a Cloud Service をご確認ください。詳しくは、[Adobe Experience Manager as a Cloud Service ドキュメント](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=ja)を参照してください。

アドビは、AEM を Azure または AWS にデプロイするための Adobe Managed Services も提供しています。Adobe Managed Services を使用することで、これらのクラウドコンピューティング環境での AEM のデプロイと運用の経験とスキルを持つエキスパートのサポートを活用できます。[Adobe Managed Services に関するドキュメント](https://business.adobe.com/jp/products/experience-manager/managed-services.html?aemClk=t)を参照してください。

AEM を Azure や AWS にデプロイするその他のあらゆる場合、またはその他のクラウドコンピューティング環境にデプロイする場合、アドビによるサポートは、仮想コンピューティング環境に対して提供されます。この仮想環境は、このページに記載されている技術仕様に従って動作する必要があります。これらのクラウド環境のいずれかで動作している AEM に関して報告された問題は、クラウドコンピューティング環境に固有のクラウドサービスとは無関係に再現できる必要があります。つまり、Azure Blob Storage や AWS S3 などのクラウドサービスが、このページに記載されている技術要件の一部としてサポートされている場合を除きます。

Adobe Managed Services の外部で Azure または AWS に AEM をデプロイする場合のレコメンデーションは、クラウドプロバイダーと直接共同作業することです。または、選択したクラウド環境での AEM のデプロイをサポートしているアドビパートナーと協力することをお勧めします。選択したクラウドプロバイダーまたはパートナーは、アーキテクチャのサイズ仕様、設計および実装を担当し、顧客独自のパフォーマンス、負荷、スケーラビリティおよびセキュリティの要件が満たされるように支援します。

### Dispatcher プラットフォーム（web サーバー） {#dispatcher-platforms-web-servers}

Dispatcher は、キャッシュおよびロードバランシングコンポーネントです。[最新バージョンの Dispatcher をダウンロード](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html?lang=ja)します。Experience Manager 6.5 ではバージョン 4.3.2 以降の Dispatcher が必要です。

Dispatcher バージョン 4.3.2 での使用では、次の web サーバーがサポートされています。

| Platform | サポートレベル |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A：サポート対象 |
| Microsoft® IIS 10（Internet Information Server） | A：サポート対象 |
| Microsoft® IIS 8.5（Internet Information Server） | Z：サポート対象外 |

1. Apache httpd のソースコードをベースとして構築された web サーバーは、ベースとした httpd のバージョンと同じサポートを備えています。これらに当てはまるか不明の場合は、アドビに問い合わせて、それぞれのサーバー製品に関するサポートレベルを確認してください。以下の場合に該当します。

   1. HTTP サーバーは、公式の Apache ソース配布のみを使用して構築されています。
   1. HTTP サーバーは、HTTP サーバーが実行されているオペレーティングシステムの一部として配信されました。例：IBM® HTTP Server、Oracle HTTP Server

1. Dispatcher は、Windows オペレーティングシステム用の Apache 2.4.x では使用できません。

## サポートされているクライアントプラットフォーム {#supported-client-platforms}

### オーサリングユーザーインターフェイスでサポートされているブラウザー {#supported-browsers-for-authoring-user-interface}

Adobe Experience Manager のユーザーインターフェイスは、次のクライアントプラットフォームで使用できます。すべてのブラウザーは、デフォルトのプラグインとアドオンのセットを使用してテストされます。

AEM のユーザーインターフェイスは、大きめの画面（通常はノートブックまたはデスクトップコンピューター）およびタブレットフォームファクター（Apple iPad、Microsoft® Surface など）に向けて最適化されています。電話のフォームファクターはサポートされていません。

>[!NOTE]
>
>**リリースサイクルの短いブラウザーのサポート：**
>
>Mozilla Firefox、Google Chrome、Microsoft® Edge のリリースは、数か月ごとにアップデートされます。アドビは、これらのブラウザーの今後のバージョンで以下に示すサポートレベルを維持するために、Adobe Experience Manager のアップデートの提供に取り組んでいます。

<table>
 <tbody>
  <tr>
   <td><strong>ブラウザー</strong></td>
   <td><strong>UI のサポート<br /> </strong></td>
   <td><strong>クラシック UI のサポート</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome（エバーグリーン）</strong></td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>Microsoft® Edge（エバーグリーン）</td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z：サポート対象外</td>
   <td>Z：サポート対象外</td>
  </tr>
  <tr>
   <td>Mozilla Firefox（エバーグリーン）</td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>Mozilla Firefox 最新 ESR [1]</td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>macOS の Apple Safari（エバーグリーン）</td>
   <td>A：サポート対象</td>
   <td>A：サポート対象</td>
  </tr>
  <tr>
   <td>macOS の Apple Safari 11 x</td>
   <td>Z：サポート対象外</td>
   <td>Z：サポート対象外</td>
  </tr>
  <tr>
   <td>Apple Safari（iOS 12.x）</td>
   <td>A：サポート対象 [2]</td>
   <td>Z：サポート対象外</td>
  </tr>
  <tr>
   <td>Apple Safari（iOS 11.x）</td>
   <td>Z：サポート対象外</td>
   <td>Z：サポート対象外</td>
  </tr>
 </tbody>
</table>

1. Firefox の拡張サポートリリース。[詳しくは、mozilla.org を参照してください。](https://www.mozilla.org/en-US/firefox/enterprise/)
1. Apple iPadのサポート

### Web サイトでサポートされているブラウザー {#supported-browsers-for-websites}

一般に、AEM Sites でレンダリングされる web サイトのブラウザーサポートは、AEM ページテンプレートの実装、設計およびコンポーネントの出力に依存するので、これらの部分を実装する当事者の管理下にあります。

## プラットフォームに関するその他の注意事項 {#additional-platform-notes}

このセクションでは、Adobe Experience Manager とそのアドオンの実行に関する特別な注意事項と詳細情報を説明します。

### IPv4 と IPv6 {#ipv-and-ipv}

Adobe Experience Manager（インスタンス、Dispatcher）のすべての要素は、IPv4 と IPv6 の両方のネットワークにインストールできます。

特別な設定が不要なので、操作はシームレスです。必要に応じて、ネットワークの種類に適した形式を使用して、IP アドレスを指定します。

IP アドレスを指定する必要がある場合は、次から（必要に応じて）選択できます。

* IPv6 アドレス。例えば、`https://[ab12::34c5:6d7:8e90:1234]:4502` のように指定します。

* IPv4 アドレス。例えば、`https://123.1.1.4:4502` のように指定します。

* サーバー名。例えば、`https://www.yourserver.com:4502` のように指定します。

* デフォルトの `localhost` は、IPv4 と IPv6 の両方のネットワークインストール用に変換されます。例：`https://localhost:4502`

### AEM Dynamic Media アドオンの要件 {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media はデフォルトで無効になっています。[Dynamic Media の有効化](/help/assets/config-dynamic.md#enabling-dynamic-media)についてはこちらを参照してください。

Dynamic Media を有効にする場合は、以下の追加の技術要件が適用されます。

>[!NOTE]
>
>これらのシステム要件は、Dynamic Media - ハイブリッドモードを使用する場合に&#x200B;**のみ**&#x200B;適用されます。Dynamic Media - ハイブリッドモードには画像サーバーが組み込まれており、特定のオペレーティングシステムでのみ認定されています。
>
>Dynamic Media - Scene7 モード（**dynamicmedia_scene7** 実行モード）で Dynamic Media を実行する場合は、追加のシステム要件はありません。AEM と同じシステム要件が適用されます。Dynamic Media - Scene7 モードのアーキテクチャでは、AEM に埋め込まれたサービスではなく、クラウドベースの画像サービスを使用します。

#### ハードウェア {#hardware}

Linux® と Windows の両方に適用されるハードウェア要件は次のとおりです。

* 4 コア以上の Intel Xeon® または AMD® Opteron CPU
* 16 GB 以上の RAM

#### Linux® {#linux}

Linux® で Dynamic Media を使用する場合は、次の必要条件を満たす必要があります。

* 最新の修正パッチが適用された RedHat® Enterprise 7 または CentOS 7 以降
* 64 ビットオペレーティングシステム
* スワップ無効（推奨）
* SELinux 無効（後述の注意を参照）

>[!NOTE]
>
>LC_CTYPE（ロケール）が `en_US.UTF-8` 以外に設定されている場合、Dynamic Media は機能しません。その値を確認するには、コマンドプロンプトで「locale」と入力します。そのように設定しない場合は、AEM を実行する前に「export LC_CTYPE=」と入力して、LC_CTYPE 環境変数を空の文字列に設定します。

>[!NOTE]
>
>**SELinux の無効化：** SELinux がオンの場合、画像サービングは機能しません。このオプションはデフォルトで有効です。この問題を修正するには、 **/etc/selinux/config** ファイルを開き、SELinux 値を次の値から変更します。
>
>`SELINUX=enforcing`**を、**`SELINUX=disabled` に変更

>[!NOTE]
>
>**NUMA アーキテクチャ：** AMD64 および Intel® EM64Tを搭載したプロセッサを搭載したシステムは、通常、NUMA（Non-Uniform Memory Architecture）プラットフォームとして設定されます。つまり、カーネルは、単一のメモリノードを構築するのではなく、ブート時に複数のメモリノードを構築します。
>
>複数のノード構成体を使用すると、他のノードが消費される前に、1 つまたは複数のノードでメモリが枯渇する可能性があります。メモリが枯渇した場合、使用可能なメモリがあっても、カーネルはプロセス（画像サーバーやプラットフォームサーバーなど）を強制終了する可能性があります。
>
>そのため、そうしたシステムを実行する場合は、**numa=off** 起動オプションを使用して NUMA をオフにし、カーネルがこれらのプロセスを強制終了するのを避けるようにすることをお勧めします。

>[!NOTE]
>
>**サーバーホスト名を解決する必要があります。**&#x200B;サーバーのホスト名が IP アドレスに解決できることを確認します。解決できない場合は、完全修飾ホスト名と IP アドレスを **/etc/hosts** に次のように追加してください。
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* 物理メモリ（RAM）の少なくとも 2 倍の容量に等しいスワップ領域

Windows で Dynamic Media を使用するには、x64 および x86 用の Microsoft® Visual Studio 2010、2013 および 2015 の再頒布可能パッケージをインストールします。

Windows x64 の場合：

* Microsoft® Visual Studio 2010 の再頒布可能パッケージを入手する（[https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/ja-jp/download/details.aspx?id=26999)）
* Microsoft® Visual Studio 2013 の再頒布可能パッケージを入手する（[https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/ja-jp/download/details.aspx?id=40784)）
* Microsoft® Visual Studio 2015 の再頒布可能パッケージを入手する（[https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/ja-jp/download/details.aspx?id=48145)）

Windows x86 の場合：

* Microsoft® Visual Studio 2010 の再頒布可能パッケージを入手する（[https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/ja-jp/download/details.aspx?id=26999)）
* Microsoft® Visual Studio 2013 の再頒布可能パッケージを入手する（[https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)）
* Microsoft® Visual Studio 2015 の再頒布可能パッケージを入手する（[https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/ja-jp/download/details.aspx?id=52685)）

#### macOS {#macos}

* 10.9.x 以降
* 体験版およびデモ版のみサポート

### PDF Generator に関する考慮事項 {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>製品</strong></p> </th>
   <th><p><strong>PDF への変換でサポートされる形式</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat Pro DC</a> 最新バージョン</td>
   <td>XPS、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX、JP2、J2K、J2C、JPC）、HTML、HTM</td>
  </tr>

<tr>
   <td>Microsoft® Office 2021 Professional Plus、小売ライセンスおよびボリュームライセンス</td>
   <td>DOC、DOCX、XLS、XLSX、PPT、PPTX、RTF、TXT</td>
  </tr>
  <tr>
   <td>
    <strong>OpenOffice 4.1.15</strong>   </td>
   <td>
    ODT、ODP、ODS、ODG、ODF、SXW、SXI、SXC、SXD、XLS、XLSX、DOC、DOCX、PPT、PPTX、画像形式（BMP、GIF、JPEG、JPG、TIF、TIFF、PNG、JPF、JPX 、JP2、J2K、J2C、JPC）、HTML、HTM、RTF、TXT<br>

</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* PDF Generator は、サポート対象のオペレーティングシステムとアプリケーションの英語版、フランス語版、ドイツ語版、日本語版のみをサポートしています。
>* PDF Generator で変換を実行するには、Adobe Acrobat Pro DC（32 ビット）が必要です。
>* PDF Generator では、32 ビット版の Microsoft® Office Professional Plus および変換に必要なその他のソフトウェアのみサポートしています。
>* ボリュームライセンスインストールで指定期間内に KMS ホストが見つからないなど、何らかの理由で Microsoft® Office インストールが非アクティブ化またはライセンス解除された場合、インストールのライセンスを再度取得して再アクティブ化するまでは、変換が失敗する場合があります。
>* PDF Generator は Microsoft® Office 365 をサポートしていません。
>* PDF Generatorの OpenOffice 向け変換機能は、Windows と Linux® の両方でサポートされています。
>* OCR PDF、Optimize PDF、Export PDF の各機能は、Windows でのみサポートされます。
>* PDF Generator サービスは、Microsoft® Windows 11 をサポートしていません。

### AEM Forms Designer の要件 {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server、Microsoft® Windows® 10 または Windows® 11
* 1 GHz 以上の高速プロセッサー（PAE、NX、および SSE2 に対応）
* 1 GB の RAM（32 ビット OS の場合）または 2 GB の RAM（64 ビット OS の場合）
* 16 GB のディスク空き容量（32 ビット OS の場合）または 20 GB のディスク空き容量（64 ビット OS の場合）
* グラフィックメモリ - 128 MB の GPU（256 MB 推奨）
* 2.35 GB のハードディスク空き容量
* 1024 x 768 ピクセル以上のモニター解像度
* ビデオハードウェアアクセラレーション（オプション）
* Acrobat Pro DC、Acrobat Standard DC または Adobe Acrobat Reader DC
* Designer をインストールするための管理者権限。
* 32 ビット AEM Forms Designer 用の Microsoft Visual C++ 2019（VC 14.28 以降）32 ビットランタイム
* 64 ビット AEM Forms Designer用Microsoft Visual C++ 2019 （VC 14.28 以降） 64 ビットランタイム

[AEM Forms Designer のインストールと設定](/help/forms/using/installing-configuring-designer.md)

### AEM Assets XMPメタデータの書き戻しの要件 {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP の書き戻しは、次のプラットフォームおよびファイル形式でサポートされ、有効になります。

* **オペレーティングシステム：**

   * Linux®（64 ビットシステムでの 32 ビットおよび 32 ビットアプリケーションのサポート）。
   * Windows Server
   * macOS X（64 ビット）

* **ファイル形式**：JPEG、PNG、TIFF、PDF、INDD、AI、EPS

### AEM Assets がメタデータの多いアセットを Linux® で処理するための要件 {#assetsonlinux}

XMPFilesProcessor プロセスを実行するには、ライブラリ GLIBC_2.14 が必要です。GLIBC_2.14 を含む Linux® カーネルを使用します。例えば、Linux® カーネルバージョン 3.1.x です。PSD ファイルなど、大量のメタデータを含むアセットの処理パフォーマンスが向上します。以前のバージョンの GLIBC を使用するとエラーが発生し、`com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP` で始まるメッセージがログに記録されます。

サポートされている形式やプラットフォームのバージョンに関するご質問については、[AEM Forms サポートにお問い合わせください &#x200B;](https://business.adobe.com/in/support/main.html)
