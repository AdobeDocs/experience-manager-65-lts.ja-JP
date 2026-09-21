---
title: Adobe Experience Manager Forms 6.5 LTS SP1のホットフィックス
description: AEM Forms 6.5 LTSのホットフィックスをダウンロードしてインストールする方法について説明します。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: e485100f-3e16-4fd4-a8ce-af771d765dd1
source-git-commit: 0ce01150bd74eeea7edb6c6127003e1aefda97a9
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 11%
---
# Adobe Experience Manager Forms 6.5 LTSのホットフィックス{#aem-form-hotfix}

この記事では、既知の問題に対処し、システムの安定性を向上させ、AEM Forms 6.5 LTSの全体的なパフォーマンスを向上させるために実装された重要な修正を紹介します。


>[!NOTE]
>
> ホットフィックスは累積的に設計されており、以前のすべての修正が含まれます。 最新のホットフィックスをリリースに適用すると、最新の問題に対処するだけでなく、以前のすべてのバグ修正と機能強化も組み込まれます。

## AEM Forms 6.5 LTSのホットフィックス {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日付</strong></td>
    <td><strong>ホットフィックスのダウンロードリンク（AEM ソフトウェア配布リンク）</strong></td>
    <td><strong>修正された問題</strong></td>
  </tr>
  <tr>
    <td>
      <strong>2026年9月21日</strong><br>
      <em>適用先：</em> AEM Forms 6.5 LTS Service Pack 2 JEE デプロイメント （JBoss、WebLogic、WebSphere）<br>
    </td>
    <td>
    <p><strong>この修正プログラムをインストールするには、次の手順を実行します。</strong></p>
    <p><strong>手順1：パッチのインストール</strong></p>
    <ul>
    <strong>JBoss:</strong>
    <li>Windows - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-jboss.zip">Windows for JBoss JEE サーバー上のAEM Forms 6.5 LTS SP2のホットフィックス </a></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/jboss/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-jboss.tar.gz">JBoss JEE サーバー向けLinux上のAEM Forms 6.5 LTS SP2のホットフィックス </a></li>
    <strong>WebLogic:</strong>
    <li>Windows - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-weblogic.zip">Weblogic JEE サーバー用Windows上のAEM Forms 6.5 LTS SP2のホットフィックス </a></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/weblogic/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-weblogic.tar.gz">Weblogic JEE サーバー向けLinux上のAEM Forms 6.5 LTS SP2のホットフィックス </a></li>
    <strong>WebSphere:</strong>
    <li>Windows - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-win-websphere.zip">Websphere JEE サーバー用Windows上のAEM Forms 6.5 LTS SP2のホットフィックス </a></li>
    <li>Linux - <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/websphere/adobe-aem-forms-jee-hotfix-6.5.LTS.2-linux-websphere.tar.gz">Websphere JEE サーバー向けLinux上のAEM Forms 6.5 LTS SP2のホットフィックス </a></li>
    </ul>
    <p>標準のAEM Forms on JEE パッチインストール手順を使用して、パッチをインストールします。 <!-- TODO: link to the 6.5 LTS JEE patch installation instructions once available --></p>
    <p><strong>手順2：脆弱性修正バンドルのインストール</strong></p>
    <ul>
    <li><a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-lts-sp2-hotfix/SP2LTSBundles_VULN-36670.zip">AEM Forms 6.5 LTS SP2の脆弱性の修正バンドル</a></li>
    </ul>
    <ol>
    <li><code>http://&lt;host&gt;:&lt;port&gt;/lc/system/console/bundles</code>でOSGi コンソールを開きます。</li>
    <li>「<strong> インストール/アップデート </strong>」をクリックします。</li>
    <li>「<strong> バンドルを開始</strong>」と「<strong> パッケージを更新</strong>」チェックボックスを選択します。</li>
    <li>「<strong> ファイルを選択</strong>」をクリックし、ダウンロードしたバンドルをアップロードします。</li>
    <li>ログが解決し、バンドルが<strong> アクティブ </strong>と表示されるまで待ちます。</li>
    </ol>
    <p><strong>手順3:AEM Forms Workbench インストーラーの更新</strong></p>
    <p>最新のAEM Forms Workbench インストーラーに更新する必要があります。 <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/fd/workbench/6-5-0-20260902-1-45/Workbench_DVD.zip">AEM Forms Workbench インストーラー</a>からダウンロードします。</p>
    <p><strong>手順4：クライアントライブラリファイルの更新（開発者）</strong></p>
    <p>このパッチには、SDK クライアントライブラリ <code>adobe-livecycle-client.jar</code>のメジャーアップデートが含まれています（<a href="/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files">AEM Forms Java ライブラリファイルを含む</a>を参照）。 プロジェクトでこのJAR ファイルを使用している場合は、ホットフィックスをインストールした後、プロジェクトのクラスパスで<code>adobe-livecycle-client.jar</code>を更新します。 最新バージョンは<code>&lt;AEM_Forms_Installation_dir&gt;\sdk\client-libs\common\adobe-livecycle-client.jar</code>で入手できます。</p>
    <p>このホットフィックスは累積的であるため、最初にService Pack 2をインストールしなくても、AEM Forms 6.5 LTS Service Pack 2以前のService Packに適用できます。</p>
    </td>
    <td>
    <ul>
    <li><b>FORMS-26818</b> Apache Shiroをバージョン 2.1.0に更新した後、JEE上のAEM Formsは、Shiro セキュリティマネージャーの<code>NoClassDefFoundError</code>でブートストラップに失敗します。 このホットフィックスは、正常なブートストラップを復元します。</li>
    <li>JEE上の<b>FORMS-26819</b> AEM Formsが<code>org.owasp.esapi.reference.JavaLogFactory</code>の「クラスが見つかりません」エラーで失敗します。 このホットフィックスは、見つからないクラスを解決します。</li>
    <li><b>FORMS-26584, FORMS-26589</b> AEM Forms 6.5 LTSにアップグレードすると、TaskManager エンドポイントが削除されます。 このホットフィックスは、TaskManager エンドポイントを復元します。</li>
    <li><b>FORMS-26569</b> JEEでは、セキュアなXML ビルダーが原因で、Configuration Manager MergeEars ステップがDOCTYPE宣言エラー（<code>ALC-LCM-010-200</code>）で失敗します。 このホットフィックスを使用すると、MergeEars ステップを完了できます。</li>
    <li><b>FORMS-25063</b> アプリケーションレベルのログがIBM WebSphere Libertyのデプロイメントにありません。 このホットフィックスは、アプリケーションレベルのログ記録を復元します。</li>
    <li><b>FORMS-24892</b> JBossでは、メールが「IMAPProvider not a subtype」で失敗します。 このホットフィックスは、JBossのメール機能を復元します。</li>
    <li><b>FORMS-24692</b> WebSphere Liberty Profile （WLP）で、メールが「SocketをTLSに変換できませんでした」で失敗します。 このホットフィックスは、WLP上のTLS経由でメールを復元します。</li>
    <li><b>FORMS-26688</b> Gibson ライブラリをバージョン 6.0.29665850に更新します。</li>
    <li><b>FORMS-25222</b>は、SAML アサーション検証の機能強化をバックポートします。</li>
    <li><b>FORMS-26733, FORMS-26734</b> Apache Log4jをバージョン 2.25.5に更新しました。</li>
    <li>このホットフィックスには、セキュリティの修正も含まれています。</li>
    </ul>
    </td>
  </tr>
  <tr>
    <td>
      <strong>2025年9月9日</strong><br>
    <td>
    <ul>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-win-pkg-6.1.176-RHF-002.zip">Windows</a>でのAEM Service Pack 6.5 LTSのホットフィックス 2</li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]hotfix-on-add-on/adobe-aemfd-linux-pkg-6.1.176-RHF-002.zip">Linux上のAEM Service Pack 6.5 LTS用ホットフィックス 2</a></li>
     <li>MacOS- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.1.176-RHF-002.zip">MacOSのAEM Service Pack 6.5 LTS用ホットフィックス 2</a></li>
    <td>
    <ul>
    <li>サーバーサイド検証（SSV）が有効になっている場合に送信が失敗する可能性がある問題に対処することで、フォーム送信の信頼性を向上させます。問題が発生した場合は、[Adobe Experience Manager Forms サポート ] （https://business.adobe.com/in/support/main.html）にお問い合わせください。
    </li>
    </ul>
    </td>    
  </tr>
    </ul>
    </td>    
  </tr>
  <tbody>
</table>

## OSGi ホットフィックスのダウンロードとインストール {#download-install-hotfix}

ホットフィックスをダウンロードしてインストールするには、次の手順を実行します。

1. ソフトウェア配布リンクから[ホットフィックス](#hotfix-for-adaptive-forms)をダウンロードします。
1. ホットフィックスアーカイブファイルを抽出して、Experience Manager パッケージ（.zip）とバンドル（.jar）ファイルを取得できるようにします。
1. [パッケージマネージャー](https://experienceleague.adobe.com/docs/experience-manager-65/content/sites/administering/contentmanagement/package-manager.html?lang=ja#accessing)を通じてパッケージ（.zip）をアップロードしてインストールします。
1. 設定マネージャーのバンドル `https://server:host/system/console/bundles` を開き、バンドル（.jar）をアップロードしてインストールします。 ホットフィックスがインストールされます。
