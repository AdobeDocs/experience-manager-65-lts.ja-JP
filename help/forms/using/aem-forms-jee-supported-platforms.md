---
title: JEE 上の AEM Forms でサポートされているプラットフォーム
description: JEE 上の AEM Forms のインストールに必要な（およびサポートされた）インフラストラクチャコンポーネントのリスト
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE,Platform Matrix
source-git-commit: 4097adf1dd533bbf21c8635a1948f9ef4c294896
workflow-type: tm+mt
source-wordcount: '2982'
ht-degree: 95%

---


# JEE 上の AEM Forms でサポートされているプラットフォーム {#supported-platforms-for-aem-forms-on-jee}

## サポートレベル {#support-levels}

JEE サーバー上の AEM Forms は、サポートされているオペレーティングシステム、アプリケーションサーバー、データベース、データベースドライバー、JDK、LDAP サーバー、およびメールサーバーを自由に組み合わせて設定できます。

このドキュメントでは、JEE 上の AEM Forms でサポートされているクライアントおよびサーバーのプラットフォームを示します。アドビは、推奨構成とその他の構成の両方について、複数のレベルのサポートを提供しています。このドキュメントでは、その他のサポートされているソフトウェアとバージョン、例外事項、パッチ定義、およびサードパーティソフトウェアパッチサポートポリシーも示します。

>[!NOTE]
>
>- サポートされているサーバープラットフォームへの例外エラーの完全リストについては、[サポートされているサーバープラットフォームへの例外エラー](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p)を参照してください。
>- JEE 上の AEM Forms でサポートされるのは、英語、フランス語、ドイツ語および日本語版のサポート対象のオペレーティングシステムとアプリケーションのみです。

### アップグレードおよびサポートポリシー

#### 完全なインストーラー

- **完全なインストーラーのアップグレードサポート**：完全なインストーラーは、6 回目のAEM サービスパックごとにリリースされます。 完全なインストーラーベースのアップグレードは、AEM 6.5.23.0 以降のみサポートされます。

- **非推奨と削除**：プラットフォームのサポートは、完全なインストーラーリリースごとに更新されます。完全なインストーラーリリース中にプラットフォーム一覧で非推奨としてマークされたソフトウェアは、後続の完全なインストーラーリリースでサポートされるプラットフォーム一覧から削除され、ソフトウェアのサポートが終了することが示されます。

#### サービスパック

- **サービスパックの対象範囲**：アドビでは、最新の 6 つのサービスパックのいずれかを使用して、AEM Forms 環境のテクニカルサポートを提供します。現在のバージョンが最新の 6 つのサービスパックよりも古い場合、最適なパフォーマンス、セキュリティ、継続的なサポートを実現するために、アドビでは最新バージョンにアップグレードすることを強くお勧めします。

- **パッチインストーラーのガイドライン**：パッチインストーラーを使用してアップデートする場合、基になる完全なインストーラーバージョンが 2 リリース以内のものであることを確認することが重要です。例えば、サービスパック 6.5.19.0 のインストール中に、基になる完全なインストーラーのバージョンが 6.5.18.0 または 6.5.12.0 であることを確認します。

- **パッチアップグレードのサポート**：サポートされている最新のプラットフォームにアップグレードするまで、最新のサービスパックへのアップグレードを続行できます。例えば、6.5.19.0 でサポートされているプラットフォームの組み合わせに移行する場合、サービスパック 6.5.12.0 から 6.5.19.0 へのアップグレードが可能です。

### 推奨設定 {#recommendedconfigurations}

アドビはこれらの設定を推奨し、標準ソフトウェア保守契約の一部として全面的または制限的サポートを提供します。

<table>
 <tbody>
  <tr>
   <th>サポートレベル</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>A：サポート対象<br /> </td>
   <td>Adobe ではこの構成への完全なサポートと保守を提供します。この構成は、Adobe の品質保証プロセスでカバーされます。</td>
  </tr>
  <tr>
   <td>R：限定サポート</td>
   <td>アドビは、特定の前提条件が満たされている場合、この設定に対して全面的なサポートを提供します。前提条件およびサポートのご依頼については、アドビエンタープライズサポートにお問い合わせください。</td>
  </tr>
  <tr>
   <td>L：限定的サポート</td>
   <td>特定の条件が満たされている場合、アドビは、この設定に対して全面的なサポートと保守サービスを提供します。この設定の場合、一部の機能については使用できません。前提条件およびサポートのご依頼については、アドビエンタープライズサポートにお問い合わせください。<br /> </td>
  </tr>
 </tbody>
</table>

### サポート対象外の設定 {#unsupported-configurations}

| サポートレベル | 説明 |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E：動作する見込み | この構成は動作する見込みであり、動作しないという報告はありません。 |
| Z：サポート対象外 | この構成はサポートされません。Adobe では、この構成が動作するかどうかに関する一切の表明をせず、この構成をサポートしません。 |

>[!NOTE]
>
>AEM Forms をご利用のお客様がオーナーシップのコストを削減し、開発アーキテクチャを簡略化し、開発スタックを近代化できるようにするために、Adobe Experience Manager のエンタープライズプラットフォームはアプリケーションサーバーベースのデプロイメントから、スタンドアロンの OSGi ベースのデプロイメントに移行します。対応するインフラストラクチャコンポーネントは削減されますが、アドビは引き続き AEM Forms JEE スタックをサポートします。
>新規インストールに関しては、可能な場合は AEM Forms を最新の OSGi スタックでデプロイし、モバイル向けのレスポンシブなアダプティブフォーム、マルチチャンネルのインタラクティブなコミュニケーション、そしてフォームデータモデルを使用したバックエンドのデータ統合などの最新技術を活用することが推奨されます。
>
>既存のお客様は、AEM Forms を引き続き JEE スタック上でデプロイしていただく必要があります。そのような場合は、AEM Forms JEE を本文書に記載されている対応インフラストラクチャでデプロイしていただく必要があります。AEM 6.5 Forzms にアップグレードする場合、および以前のAEM Forms リリースでサポートされていないプラットフォームを使用している場合、サポートされているプラットフォームへのアップグレード方法についてヘルプを表示するには、Adobe サポートにお問い合わせください。

### Java™ 仮想マシン（JVM） {#java-virtual-machines-jvm}

Adobe Experience Manager Forms を使用するには、Java™ 仮想マシンが必要です。Java 仮想マシンは、Java™ Development Kit（JDK）ディストリビューションに付属しています。Adobe Experience Manager は、次のバージョンの Java™ 仮想マシンで動作します。

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>サポートレベル</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
   <tr> 
   <td><p>Oracle Java™ SE 21（64 ビット）<sup> [8] </sup> </p>  </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>マイナーリリースとアップデート </p> </td>
  </tr>
  <tr> 
   <td><p>Oracle Java™ SE 17（64 ビット）<sup> [8] </sup> </p>  </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>マイナーリリースとアップデート </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- Java™ ベンダーが発表するセキュリティ情報を常に確認し、本番環境の安全性とセキュリティを確保すること、および最新の Java™ アップデートをインストールすることをお勧めします。
>- JEE 上の AEM Forms では、本番環境に対して 64 ビットの JVM のみがサポートされています。

### データベースと CRX の永続性 {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>プラットフォーム</strong></p> </td>
   <td><p><strong> 説明</strong></p> </td>
   <td><p><strong>サポートレベル</strong></p> </td>
  </tr>
  <tr>
   <td><p>ファイルシステム</p> </td>
   <td><p>Repository Microkernel（TAR MK ファイル）</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 9.0 </p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 8.0</p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
    <tr>
   <td><p> MongoDB Enterprise 7.0 </p> </td>
   <td><p>リポジトリ Microkernel</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
   <tr>
   <td>Oracle Database 19c（Standard、Real Application Clusters（RAC）および Enterprise エディション） </td>
   <td>-</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2022 </p> </td>
   <td><p>-</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td>MySQL 8.4</td>
   <td>-</td>
   <td>R：限定サポート</td>
  </tr>
 </tbody>
</table>

- MongoDB はサードパーティのソフトウェアで、AEM ライセンスパッケージには含まれていません。詳しくは、[MongoDB ライセンスポリシー](https://www.mongodb.org/about/licensing/)を参照してください。
- AEM のデプロイメントを最大限に活用するには、プロフェッショナルサポートを受けられるように MongoDB Enterprise バージョンのライセンスを取得することをお勧めします。
- アドビカスタマーケアは、MongoDB を AEM で利用することに関連する問題の絞り込みを支援いたします。詳しくは、[MongoDB for Adobe Experience Manager のページ](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)を参照してください。
- 「ファイルシステム」には、POSIX に準拠したブロックストレージが含まれます。これには、ネットワークストレージテクノロジーが含まれます。ファイルシステムのパフォーマンスは異なり、全体的なパフォーマンスに影響を与える場合があることに注意してください。ネットワーク上またはリモートのファイルシステムを使用してテスト AEM を読み込むことをお勧めします。
- MongoDB Storage Engine WiredTiger のみがサポートされています。
- MongoDB Sharding は AEM ではサポートしていません。
- Document Security モジュールは、コンテンツリポジトリを使用しません。つまり、Document Security のみを使用していて、HTML Workspace、HTML5 フォーム、アダプティブフォームを使用する予定がない場合は、コンテンツリポジトリをインストールしないでください。

### データベースドライバー {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>データベース </th>
   <th><p><strong>プラットフォーム</strong></p> </th>
   <th><p><strong>サポートしているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 8.4</p> </td>
   <td><p>JEE のインストールで AEM Forms に付属</p> </td>
  </tr>
  <tr>
   <td>Microsoft® SQL Server<br /> </td>
   <td><p>Microsoft® SQL Server JDBC ドライバー 12.10.0<br /> </p> <p>sqljdbc12.10.0.jar</p> </td>
   <td><p>Microsoft® の web サイトからダウンロードします。</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Oracle Database 19.3.0.0.0 JDBC ドライバー</p> <p>ojdbc8.jar（バージョン 19.3.0.0.0）<br /> </p> </td>
   <td><p><a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Oracle web サイト</a>からダウンロードします。</p> </td>
  </tr>
 </tbody>
</table>

### アプリケーションサーバー {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> プラットフォーム</strong></p> </td>
   <td><p><strong>サポートレベル</strong></p> </td>
   <td><p><strong>サポートされているパッチ定義</strong></p> </td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform （EAP） 8.0.6 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>対応の EAP バージョンのパッチと累積パッチ</p> </td>
  </tr>
 </tbody>
</table>

### サーバーオペレーティングシステム {#server-operating-systems}

#### 本番環境 {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> プラットフォーム</strong></p> </th>
   <th><p><strong>サポートレベル</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
     <tr>
   <td>Microsoft® Windows Server 2022（64 ビット版）</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>A：サポート対象</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 9 （Kernel 5.x）（64 ビット版）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>マイナーリリース、累積アップデート、需要なアップデート</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux 8（Kernel 4.x）（64 ビット版）</td>
   <td><p>A：サポート対象</p> </td>
   <td><p>マイナーリリース、累積アップデート、需要なアップデート</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 15-SP6 （64 ビット版）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>サービスパック、累積パッチ、重要なセキュリティアップデート</p> </td>
  </tr>
 </tbody>
</table>

#### 仮想化環境 {#virtualized-environment}

AEM Forms on JEE は、物理マシンまたは仮想環境で実行できます。ただし、仮想環境での AEM Forms の使用に問題が発生した場合は、物理マシン上で問題を再現してみてください。物理マシン上でも問題が発生する場合は、アドビサポートにお問い合わせいただき、解決を試みてください。物理マシン上で再現することができない問題に関しては、バーチャル環境のベンダーにお問い合わせください。

#### 開発環境 {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>プラットフォーム（基本バージョン）</strong></p> </th>
   <th>サポートレベル</th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 64 ビット版</p> </td>
   <td>E：動作する見込み</td>
   <td><p>サービスパックと重要なアップデート</p> </td>
  </tr>
 </tbody>
</table>

### 対応のサーバープラットフォームの例外事項 {#exceptions-to-supported-server-platforms}

AEM Forms on JEE サーバーの設定でプラットフォームを選択するときは、次の例外事項を考慮してください。

1. CRX リポジトリは、TarMK および MongoDB タイプの永続性をサポートします。
1. AEM Forms on JEE では、JBoss® ロールベースのアクセス制御（RBAC）をサポートしていません。

<!-- 
1. [!DNL Microsoft&reg; Windows Server 2019] does not support [!DNL MySQL 5.7] and [!DNL JBoss&reg; EAP 7.1], [!DNL Microsoft&reg; Windows Server 2019] does not support turnkey installations for [!DNL Experience Manager Forms Service Pack 6.5.10.0 and later]. (CQDOC-18312) 
-->

この他に、AEM Forms on JEE の導入のためにソフトウェアを選択する際には、次の項目を考慮してください。

- AEM Forms on JEE では、対応ソフトウェアの指定されたメジャーおよびマイナーバージョンに加えて、アップデート、パッチ、および修正パックをサポートしています。ただし、次のメジャーバージョンまたはマイナーバージョンに対するアップデートは、特に記載がない限りサポートされていません。
- クラスターベースのインストールは、TarMK 永続性をサポートしていません。サポートされている永続性については、[AEM Forms のインストールでの永続性タイプの選択](/help/forms/using/choosing-persistence-type-for-aem-forms.md)を参照してください。
- AEM Forms on JEE では、弊社の[サードパーティソフトウェアサポートポリシー](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p)に従い、様々なサードパーティソフトウェアをサポートしています。
- AEM Forms on JEE では、サードパーティベンダーが提供するサポートに基づいて、プラットフォームをサポートします。組み合わせによっては、サードパーティベンダーが許可しない場合があります。例えば、多くのベンダーが、自社のアプリケーションサーバーを Oracle で使用することを認めていません。そのため、AEM Forms on JEE でもこれらの組み合わせをサポートしていません。対応のソフトウェアバージョンを確実に選択するには、サードパーティベンダーのサポート一覧も確認してください。
- AEM Forms on JEE では TarMK コールドスタンバイをサポートしていません。
- AEM Forms on JEE では垂直クラスタリングをサポートしていません。
- AEM Forms on JEE では、クラスター環境での MySQL データベースをサポートしていません。

### LDAP サーバー（オプション） {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>製品（基本バージョン）</strong></p> </th>
   <th><p><strong>サポートしているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft® Active Directory 2022</td>
   <td>メンテナンスリリースと修正パック</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Directory Server 6.4</p> </td>
   <td><p>フィーチャーパックと暫定フィックス</p> </td>
  </tr>
 </tbody>
</table>

### メールサーバー（オプション） {#email-servers-optional}

| 製品 |
| ----------------------- |
| Microsoft® Exchange 2013 |
| Microsoft® Office 365 |

### コンテンツマネージャーと対応するコネクタ {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>製品<br /> </strong></td>
   <td><strong>バージョン</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum®</td>
   <td>7.3</td>
  </tr>
  <tr>
   <td>IBM® FileNet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM® Content Manager サーバー（非推奨） </td>
   <td>8.5 Fix pack 2</td>
  </tr>
  <tr>
   <td> IBM® Content Manager クライアント</td>
   <td>8.7 </td>
  </tr>
  <tr>
   <td> IBM® Content Manager クライアント（非推奨）</td>
   <td>8.5 </td>
  </tr>
   <td>Microsoft® Sharepoint </td>
   <td>2019<br /> </td>
  </tr>
 </tbody>
</table>

### Cordova のサポート {#support-for-cordova}

AEM Forms アプリケーションで Apache Cordova がサポートされるようになりました。サポートされている Cordova プラットフォームのバージョンは以下のとおりです。

- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android™ 6.0.0
- Cordova Windows 4.4.3

### PDF Generator のソフトウェアサポート {#software-support-for-pdf-generator}

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
>- PDF Generator は、サポート対象のオペレーティングシステムとアプリケーションの英語版、フランス語版、ドイツ語版、日本語版のみをサポートしています。
>- PDF Generator で変換を実行するには、Adobe Acrobat Pro DC（32 ビット）が必要です。
>- PDF Generator では、32 ビット版の Microsoft® Office Professional Plus および変換に必要なその他のソフトウェアのみサポートしています。
>- ボリュームライセンスインストールで指定期間内に KMS ホストが見つからないなど、何らかの理由で Microsoft® Office インストールが非アクティブ化またはライセンス解除された場合、インストールのライセンスを再度取得して再アクティブ化するまでは、変換が失敗する場合があります。
>- PDF Generator は Microsoft® Office 365 をサポートしていません。
>- PDF Generatorの OpenOffice 向け変換機能は、Windows と Linux® の両方でサポートされています。
>- OCR PDF、Optimize PDF、Export PDF の各機能は、Windows でのみサポートされます。
>- PDF Generator サービスは、Microsoft® Windows 11 をサポートしていません。

<!-- Removed lines: >- PDF Generator fails to convert files using Microsoft&reg; Visio 2019. You can continue to use Microsoft&reg; Visio 2016 to convert .VSD and .VSDX files.
>- PDF Generator fails to convert files using Microsoft&reg; Project 2019. You can continue to use Microsoft&reg; Project 2016 to convert .MPP files.-->

### アクセシビリティサポートの例外事項 {#exceptions-to-accessibility-support}

AEM Forms の以下のサブシステムは、[リハビリテーション法 508 条](https://www.section508.gov/)に準拠していません。

- アダプティブフォームオーサリング UI
- Forms Manager オーサリング UI
- Correspondence Management オーサリング UI
- 管理 UI（管理コンソール UI）

## AEM Forms on JEE の必要システム構成 {#system-requirements-for-aem-forms-on-jee}

### 最小ハードウェア要件 {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>プラットフォーム</td>
   <td>最小ハードウェア要件</td>
  </tr>
  <tr>
   <td>Microsoft® Windows Server</td>
   <td>インテル Xeon® E5-2680、2.4 GHz プロセッサーまたは同等の <br />VMWare ESX 5.1 以降<br /> RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br />空きディスク容量：15 GB の一時的空き容量のほかに、22 GB の容量<br />（JEE 上の AEM Forms 用）</td>
  </tr>
  <tr>
   <td>SUSE® Linux® Enterprise Server</td>
   <td>インテル Xeon® E5-2670v2、1 vCPU、2.5 GHz プロセッサー <br />AWS m3.medium（3 つの ECU）<br />RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br />空きディスク容量：6 GB の一時的空き容量のほかに、22 GB の容量<br />（JEE 上の AEM Forms 用）</td>
  </tr>
  <tr>
   <td>Red Hat® Enterprise Linux®</td>
   <td>Intel Xeon® E5-2670v2、1 vCPU、2.5 GHz プロセッサー <br />AWS m3.medium（3 つの ECU）<br />RAM：6 GB（64 ビット JVM が付属している 64 ビット OS）<br />空きディスク容量：6 GB の一時的空き容量のほかに、22 GB の容量<br />（JEE 上の AEM Forms 用）<br /> </td>
  </tr>
  <tr>
   <td>小規模な本番環境向けのハードウェア要件</td>
   <td>
    <ul>
     <li><strong>Intel® 搭載環境</strong>：Intel Xeon® E5-2680、2.4 GHz 以上。デュアルコアプロセッサーを使用するとパフォーマンスがさらに向上します。</li>
     <li><strong>メモリ：</strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

上記以外の要件については、以下を参照してください。

- [JEE デプロイメント上でのシングルサーバー AEM Forms の導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_single_65_jp)
- [クラスター化された AEM Forms on JEE の導入に必要なシステム構成](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65_jp)

### Adobe Acrobat と Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat および Adobe Reader（Base）</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020（クラシックトラック）</td>
   <td>バージョン 20.004.30006 以降<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
>
>Acrobat DC 製品ファミリーでは、異なる製品である Acrobat と Reader のそれぞれに、「Classic」と「Continuous」の 2 種類のトラックが用意されています。2 つのトラックについての詳細や比較については、[https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html) を参照してください。

## JEE 上の AEM Forms でサポートされているクライアント {#supported-clients-for-aem-forms-on-jee}

### ワークベンチ {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>プラットフォーム</strong></p> </th>
   <th><p><strong>サポートしているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10（Enterprise、Pro、Basic）</p> <p>32 または 64 ビット版</p> <p> </p> </td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2022 Server</td>
   <td>サービスパックと重要なアップデート</td>
  </tr>
 </tbody>
</table>

- インストールのためのディスク空き容量：1.7 GB（ワークベンチのみ）、2.7 GB（ワークベンチ、Designer、およびサンプルアセンブリのフルインストールを単一ドライブで行う場合）、400 MB（一時的インストールディレクトリ）、200 Mb（ユーザー一時ディレクトリ）、および 200 MB（Windows 一時ディレクトリ）。これらの場所がすべて 1 つのドライブ上にある場合は、インストール時に 1.5 GB の空き容量が必要です。一時ディレクトリにコピーされるファイルは、インストールが完了すると削除されます。

- ワークベンチを実行するためのメモリ：2 GB の RAM
- ハードウェア要件： Intel® Pentium® 4 または AMD® の同等の 1 GHz プロセッサー
- 1024 X 768 ピクセル以上のモニター解像度、16 ビットカラー以上
- JEE サーバー上の AEM Forms に対する TCP/IPv4 または TCP/IPv6 ネットワーク接続
- ワークベンチを Windows にインストールするには、管理者権限が必要です。管理者以外のアカウントを使用してインストールする場合は、適切なアカウントの資格情報が求められます。

### Designer {#designer}

- Microsoft® Windows® 2016 Server、Microsoft® Windows® 2019 Server、Microsoft® Windows® 10 または Windows® 11
- 1 GHz 以上の高速プロセッサー（PAE、NX、および SSE2 に対応）
- 1 GB の RAM（32 ビット OS の場合）または 2 GB の RAM（64 ビット OS の場合）
- 16 GB のディスク空き容量（32 ビット OS の場合）または 20 GB のディスク空き容量（64 ビット OS の場合）
- グラフィックメモリ - 128 MB の GPU（256 MB 推奨）
- 2.35 GB のハードディスク空き容量
- 1024 x 768 ピクセル以上のモニター解像度
- ビデオハードウェアアクセラレーション（オプション）
- Acrobat Pro DC、Acrobat Standard DC または Adobe Acrobat Reader DC
- Designer をインストールするための管理者権限。
- Microsoft® Visual C++ 2019（VC 14.28 以降）32 ビットランタイム

### ブラウザー {#browsers}

#### デスクトップ {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>ブラウザー（ベース）</strong></p> </th>
   <th><p><strong>サポートレベル</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Edge（エバーグリーン）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td><p>サービスパックとアップデート</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox（エバーグリーン）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E：動作する見込み</td>
   <td> すべてのアップデート</td>
  </tr>
  <tr>
   <td><p>Google Chrome（Evergreen）</p> </td>
   <td><p>A：サポート対象</p> </td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>macOS の Apple Safari</td>
   <td>A：サポート対象</td>
   <td>すべてのアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>以下にデスクトップに対する一部のブラウザー関連の例外事項を示します。
>
>- Safari は Macintosh OS X でのみサポートされています。
>- Acrobat DC 以降のバージョンでは、Workspace は Macintosh OS X 10.6 および 10.7 上の Safari 5.1 をサポートしています。Safari 5.1 の Adobe Reader、Acrobat との互換性については、[https://helpx.adobe.com/jp/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/jp/x-productkb/multi/safari-5-1-incompatible-reader.html) を参照してください。
>- 管理コンソールは Safari ではサポートされていません。
>- Correspondence Management は、AEM 6.1 Forms で Windows® Internet Explorer 9.0 をサポートしていません。
>- フォームポータルは、アクセシビリティのために、JAWS 14.0 画面読み上げソフトウェアを Internet Explorer 11 でサポートしています。

#### モバイルクライアント {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>ブラウザー（ベース）</strong></p> </th>
   <th><p><strong>サポートされているパッチ定義</strong></p> </th>
  </tr>
  <tr>
   <td><p>Chrome（Android™ 4.1.2 以降）</p> </td>
   <td><p>すべてのアップデート</p> </td>
  </tr>
  <tr>
   <td>Safari（iOS 15.1 以降）</td>
   <td>すべてのアップデート</td>
  </tr>
  <tr>
   <td>Microsoft® Edge<br /> </td>
   <td>すべてのアップデート<br /> </td>
  </tr>
  <tr>
   <td>Android™ 4.4 以降のネイティブ Android ブラウザー</td>
   <td>すべてのアップデート</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- Forms Portal は iPad の Safari でのみサポートされています。

### AEM Forms アプリケーション {#aem-forms-workspace-app}

#### モバイルデバイスのサポート {#mobile-device-support}

AEM Forms アプリケーションは次のプラットフォームで利用可能です。

| **プラットフォーム** | **サポートされているデバイス** |
| --- | --- |
| Apple iOS | Apple の iPhone、iPad、iPad Air、iPad mini [iOS 15.1 以降] |
| Google Android™ | Android™ 5.1 以降。AEM Forms アプリケーションは、7 インチと 10 インチの Samsung Galaxy タブレット、および主要なスマートフォンで動作確認されています。 |
| Microsoft® Windows | Microsoft の Windows 10 オペレーティングシステムを実行している Microsoft® Surface のデバイス、タブレット、ノートパソコン、およびデスクトップ PC |

### Adobe Document Security Extension for Microsoft® Office {#adobe-rights-management-extension-for-microsoft-office}

Adobe Document Security Extension for Microsoft® Office の必要システム構成を確認するには、[ここ](https://www.adobe.com/jp/products/livecycle/rightsmanagement/extension/downloads.html)をクリックしてください。

### クライアントサポートの例外事項 {#exceptions-to-client-support}

AEM Forms on JEE では、対応ソフトウェアの指定されたメジャーおよびマイナーバージョンに加えて、アップデート、パッチ、および修正パックをサポートしています。ただし、次のメジャーバージョンまたはマイナーバージョンに対するアップデートは、特に記載がない限りサポートされていません。

## サードパーティパッチサポートポリシー {#third-party-patch-support-policy}

JEE 版 AEM Forms のサードパーティソフトウェア要件は、それぞれの製品ドキュメントの「必要システム構成」の節に記載されています。すべてのドキュメントは、[https://adobe.com/go/learn_aemforms_documentation_65_jp](https://adobe.com/go/learn_aemforms_documentation_65_jp) からアクセスすることができます。

JEE 上の AEM Forms のサードパーティ参照プラットフォームは、JEE 上の AEM Forms の開発とリリースの時点において最新だったサードパーティ製インフラストラクチャの特定のパッチレベルを、そのバージョンの JEE 上の AEM Forms でサポートしているインフラストラクチャの最小のパッチまたはサービスパックのレベルから記載しています。

アドビでは、サードパーティベンダーがリリース時に JEE 上の AEM Forms がサポートするバージョンとの後方互換性を保証していると仮定して、サードパーティベンダーの緊急および推奨パッチをサポートします。JEE 上の AEM Forms ドキュメントに記載の最小パッチレベル後にリリースされたパッチのみが、アドビのサポート対象です。

場合によっては、主要な機能を変更しそのために完全な後方互換性をサポートしなくなったサードパーティアップデートはサポートされません。サポートされているアップデートの詳細については、[サポートされているパッチ定義](https://helpx.adobe.com/jp/aem-forms/aem-forms-third-party-software-patch.html)で特定のベンダー製品とアドビがサポートするパッチタイプを参照してください。

アドビの管理の及ばない状況においては、後方互換性を主張しているサードパーティ製パッチによって、アドビ製品またはお客様の環境に悪い影響を及ぼす可能性があります。このような場合、お客様がサードパーティからの緊急パッチを重要なシステムに適用する前に、その影響を評価することが推奨されます。アドビはサードパーティと共に妥当なビジネス努力を払って、通常のアドビサポートプログラムを通してあるいはサードパーティがパッチの問題を修正することによって、そのような問題を解決します。このことは、アドビによってサポートされる新たにリリースされたサードパーティパッチが、ベンダーによってマニュアルに記載されているように、または JEE 上の AEM Forms と機能することを保証するものではありません。

アドビは、任意の時点で、JEE 上の AEM Forms リリースおよびそれらのサポートされているパッチ定義によってサポートされているサードパーティリファレンスプラットフォームを変更する権利を留保します。

サードパーティパッチの追加情報は、アドビのエンタープライズサポートサイトで、ご使用の製品に関するナレッジベース記事を検索することでも確認できます。

<!--

## Platform updates {#platform-updates}

The following platforms are marked as deprecated with AEM Forms 6.5.18.0 release on August 31, 2023:

- Microsoft&reg; Windows Server 2019 (64-bit)
- Microsoft&reg; Active Directory 2016

The following platforms are marked as deprecated with AEM Forms 6.5.13.0 release on June 2, 2022:
- Microsoft&reg; SharePoint 2016

The following platforms are marked as deprecated with AEM Forms 6.5.10.0 release on September 7, 2021:

- Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/support/programs/eol-matrix.html).
- Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
- Microsoft&reg; Windows Server 2016 (64-bit) 
- Microsoft&reg; Office 2016
- OpenOffice 4.1.2

-->


<!--## Revision History {#revision-history}-->

<!--

- 6.5.18.0 (Aug 31, 2023)
  - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
    - MongoDB Enterprise 4.4
    - Oracle WebLogic Server 14c
    - My SQL JDBC connector 8
    - Active Directory 2022
    - Microsoft&reg; Windows Server 2022 (64-bit)

  - **Removed support**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
    - Windows Server 2016 (64-bit)
    - MongoDB Enterprise 4.0
    - Oracle Database 12c Release 2 (12.2.0.1.0)
    - MySQL 5.7.35
    - Microsoft&reg; SQL Server 2016
    - JBoss&reg; EAP 7.1.4
    - My SQL JDBC connector 5.1.44
    - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
    - Microsoft&reg; SQL Server JDBC driver 6.2.2.0
    - Microsoft&reg; JDBC Driver 8.x for SQL Server

    The release has also removed support for the following platforms for PDF Generator and in-general:
    - Microsoft&reg; Sharepoint 2016
    - Microsoft&reg; Office 2016
    - Microsoft&reg; Office Visio 2016 
    - Microsoft&reg; Publisher 2016
    - Microsoft&reg; Project 2016
    - OpenOffice 4.1.2
    - Acrobat 2017 (Classic track) Version 17.011.30078 or later

  - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
    - Microsoft&reg; Windows Server 2019 (64-bit)
    - Microsoft&reg; Active Directory 2016
    
- 6.5.13.0 (June 2, 2022)

  The following platforms are deprecated with AEM Forms 6.5.13.0 release on:
 
  - Microsoft&reg; SharePoint 2016

- 6.5.12.0 (March 3, 2022)

    - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
      - IBM&reg; J9 Virtual Machine (build 2.8, JRE 1.8.0)
      - Oracle Database 12c Release 1
      - Oracle Database 18c
      - Oracle Unified Directory (OUD) 11g Release 2
      - IBM&reg; Lotus Domino 9.0
      - IBM&reg; FileNet 5.2
      - Adobe Flash Player

    - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:

      - MongoDB Enterprise 4.0
      - MongoDB Enterprise 4.2
      - IBM&reg; DB2&reg; 11.1
      - Oracle Database 12c Release 2
      - MySQL 5.7.35
      - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
      - JBoss&reg; Enterprise Application Platform (EAP) 7.1.4
      - IBM&reg; Content Manager Server 8.5 Fix pack 2
      - IBM&reg; Content Manager Client 8.5
      - Microsoft&reg; SQL Server 2016

- 6.5.10.0 (Sep 01, 2022)

  - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platform:
  
    - Oracle Java&trade; SE 11 (64 bit) SDK for application server JBoss&reg; EAP 7.4.
  - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:

    - Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/support/programs/eol-matrix.html).
    - Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
    - Microsoft&reg; Windows Server 2016 (64-bit) 
    - Microsoft&reg; Office 2016
    - OpenOffice 4.1.2


-->
<!--
### Release 6.5.19.1 (Dec 15, 2023)

| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 6.0 |MongoDB Enterprise 4.4   |  |
| MongoDB Enterprise 5.0 |  |  |
|  | |  |

### Release 6.5.18.0 (Aug 31, 2023)

| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 4.4 | Windows Server 2016 (64-bit) | Microsoft&reg; Windows Server 2019 (64-bit) |
| Oracle WebLogic Server 14c | MongoDB Enterprise 4.0 | Microsoft&reg; Active Directory 2016 |
| My SQL JDBC connector 8 | Oracle Database 12c Release 2 (12.2.0.1.0) |  |
| Active Directory 2022 | MySQL 5.7.35 |  |
| Microsoft&reg; Windows Server 2022 (64-bit) | Microsoft&reg; SQL Server 2016 |  |
|  | JBoss&reg; EAP 7.1.4 |  |
|  | My SQL JDBC connector 5.1.44 |  |
|  | Microsoft&reg; SQL Server JDBC driver 6.2.1.0 |  |
|  | Microsoft&reg; SQL Server JDBC driver 6.2.2.0 |  |
|  | Microsoft&reg; JDBC Driver 8.x for SQL Server |  |
|  |  |  |
|  | **Removed Support (PDF Generator and In-General):** |  |
|  | Microsoft&reg; Sharepoint 2016 |  |
|  | Microsoft&reg; Office 2016 |  |
|  | Microsoft&reg; Office Visio 2016 |  |
|  | Microsoft&reg; Publisher 2016 |  |
|  | Microsoft&reg; Project 2016 |  |
|  | OpenOffice 4.1.2 |  |
|  | Acrobat 2017 (Classic track) Version 17.011.30078 or later |  |


### Release 6.5.13.0 (June 2, 2022)

| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
|  |  | Microsoft&reg; SharePoint 2016 |


### Release 6.5.12.0 (March 3, 2022)

| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
|  | IBM&reg; J9 Virtual Machine (build 2.8, JRE 1.8.0) | MongoDB Enterprise 4.0 |
|  | Oracle Database 12c Release 1 | MongoDB Enterprise 4.2 |
|  | Oracle Database 18c | IBM&reg; DB2&reg; 11.1 |
|  | Oracle Unified Directory (OUD) 11g Release 2 | Oracle Database 12c Release 2 |
|  | IBM&reg; Lotus Domino 9.0 | MySQL 5.7.35 |
|  | IBM&reg; FileNet 5.2 | Microsoft&reg; SQL Server JDBC driver 6.2.1.0 |
|  | Adobe Flash Player | JBoss&reg; Enterprise Application Platform (EAP) 7.1.4 |
|  | | IBM&reg; Content Manager Server 8.5 Fix pack 2 |
|  | | IBM&reg; Content Manager Client 8.5 |
|  | | Microsoft&reg; SQL Server 2016 |
|  | | Microsoft&reg; Windows Server 2016 |

### Release 6.5.10.0 (September 01, 2022)

| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
| Oracle Java&trade; SE 11 (64 bit) SDK for application server JBoss&reg; EAP 7.4. | | [Adobe Acrobat 2017 - Core support for Adobe Acrobat 2017 ends on June 6, 2022.](https://helpx.adobe.com/support/programs/eol-matrix.html)|
|  | Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)| |
|  | | Microsoft&reg; Windows Server 2016 (64-bit)|
|  | | Microsoft&reg; Office 2016 |
|  | | OpenOffice 4.1.2 |


>[!NOTE]
>
> A deprecated platform continue to receive support until the next full installer release or until third-party vendor support for the platform reaches its end-of-life, whichever is earlier.
-->
<!-- 
- Oct 10, 2021

  - Changed supported version of iOS for AEM Forms App to iOS 15.1. The previous version was iOS 12.

- Sep 07, 2021
  - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
    - [!DNL Adobe Acrobat 2020]
    - [!DNL Ubuntu 20.04]
    - [!DNL Open Office 4.1.10]
    - [!DNL Microsoft&reg;&reg; Office 2016]
    - [!DNL Microsoft&reg;&reg; Windows Server 2016]
    - [!DNL RHEL8]

- Dec 03, 2020
  - Support added with AEM Forms 6.5.7.0 or later for the following platform:
    - [!DNL Microsoft&reg;&reg; SQL Server 2019]

- Sep 09, 2020

    - Changed supported version of iOS for AEM Forms App to iOS 12. The previous version was iOS 11.

-->
