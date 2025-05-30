---
title: AEM でのシリアル化の問題の軽減
description: AEM でのシリアル化の問題を軽減する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
exl-id: eef69d02-2e88-4f44-98bb-d98fa297e3a2
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 100%

---

# AEM でのシリアル化の問題の軽減{#mitigating-serialization-issues-in-aem}

## 概要 {#overview}

アドビの AEM チームは、オープンソースプロジェクト [NotSoSerial](https://github.com/kantega/notsoserial) と緊密に連携して、**CVE-2015-7501** で説明されている脆弱性の軽減を支援しています。NotSoSerial は [Apache 2 ライセンス](https://www.apache.org/licenses/LICENSE-2.0)でライセンスが付与され、[BSD に似た独自のライセンス](https://asm.ow2.io/)でライセンスが付与される ASM コードが含まれます。

このパッケージに含まれるエージェント JAR は、アドビが変更を加えて配布する NotSoSerial です。

NotSoSerial は Java™ レベルの問題を解決する Java™ レベルのソリューションであり、AEM に固有のものではありません。これは、オブジェクトのシリアル化を解除するときに、プリフライトのチェックを追加します。このチェックでは、ファイアウォールスタイルの許可リスト、ブロックリスト、またはその両方と照合してクラス名をテストします。デフォルトのブロックリスト内のクラス数は限られているので、このテストがシステムやコードに影響を与える可能性はほとんどありません。

エージェントはデフォルトで、現在知られている脆弱なクラスに対してブロックリストチェックを実行します。このブロックリストの目的は、現在リストに掲載されている、このタイプの脆弱性を悪用した攻撃からユーザーを保護することです。

ブロックリストと許可リストは、この記事の[エージェントの設定](/help/sites-administering/mitigating-serialization-issues.md#configuring-the-agent)セクションの手順に従って設定できます。

このエージェントの目的は、最新の既知のクラスの脆弱性を軽減することです。プロジェクトで信頼できないデータを逆シリアル化している場合でも、サービス拒否攻撃、メモリ不足攻撃、将来的な未知の逆シリアル化攻撃に対しては依然として脆弱である可能性があります。

アドビは、Java™ 6、7、8 を公式にサポートしています。ただし、アドビでは、NotSoSerial が Java™ 5 もサポートしていると理解しています。

## エージェントのインストール {#installing-the-agent}

>[!NOTE]
>
>以前に AEM 6.1 向けのシリアル化ホットフィックスをインストールしている場合は、Java™ を実行する行からエージェントの開始コマンドを削除します。

1. **com.adobe.cq.cq-serialization-tester** バンドルをインストールします。

1. Bundle Web コンソール（`https://server:port/system/console/bundles`）にアクセスします。
1. シリアル化バンドルを探して起動します。これにより、NotSoSerial エージェントが動的に自動でロードされます。

## アプリケーションサーバーへのエージェントのインストール {#installing-the-agent-on-application-servers}

NotSoSerial エージェントは、アプリケーションサーバーの AEM の標準配布版には含まれていません。ただし、AEM jar 配布から抽出して、アプリケーションサーバーの設定で使用することができます。

1. まず、AEM クイックスタートファイルをダウンロードして抽出します。

   ```shell
   java -jar aem-quickstart-6.2.0.jar -unpack
   ```

1. AEM クイックスタートを展開した場所に移動し、`crx-quickstart/opt/notsoserial/` フォルダーを AEM アプリケーションサーバーのインストールの `crx-quickstart` フォルダーにコピーします。

1. `/opt` の所有者を、サーバーを実行しているユーザーに変更します。

   ```shell
   chown -R opt <user running the server>
   ```

1. この記事の次の節に示すように、エージェントを設定し、適切にアクティベートされていることを確認します。

## エージェントの設定 {#configuring-the-agent}

ほとんどのインストールにおいて、デフォルトの設定で十分です。この設定には、リモート実行の既知の脆弱性があるクラスのブロックリストや、信頼できるデータの逆シリアル化が安全なパッケージの許可リストが含まれています。

ファイアウォールの設定は動的であり、次の手順でいつでも変更できます。

1. Web コンソール（`https://server:port/system/console/configMgr`）にアクセスします。
1. **逆シリアル化ファイアウォール設定**&#x200B;を検索してクリックします。

   >[!NOTE]
   >
   >次の URL にアクセスして、設定ページに直接アクセスすることもできます。
   >
   >* `https://server:port/system/console/configMgr/com.adobe.cq.deserfw.impl.DeserializationFirewallImpl`

この設定には、許可リスト、ブロックリスト、逆シリアル化ログが含まれています。

**許可リストへの登録**

許可リストへの登録セクションには、逆シリアル化を許可されたクラスやパッケージの接頭辞が一覧表示されます。独自のクラスを逆シリアル化する場合は、クラスまたはパッケージのいずれかをこの許可リストに加えます。

**ブロックリストへの登録**

ブロックリストへの登録セクションには、逆シリアル化が許可されないクラスが表示されます。これらのクラスの初期セットは、リモート実行の攻撃に脆弱であると見なされるクラスに限定されています。ブロックリストは、許可リストに登録されたエントリの前に適用されます。

**診断ログ**

「診断ログ」セクションでは、逆シリアル化の実行中にログに記録される内容を、複数のオプションから選択できます。これらのオプションは、最初の使用時にのみログに記録され、次回以降の使用時には記録されません。

デフォルトの **class-name-only** を使用すると、逆シリアル化されるクラスを確認できます。

**full-stack** オプションを選択すると、最初にシリアル化の解除が試行されたときの Java™ スタックがログに記録され、シリアル化の解除が行われている場所を示します。これは、自身の環境からシリアル化が解除されたクラスを探して削除するときに便利です。

## エージェントのアクティベートの検証 {#verifying-the-agent-s-activation}

次の URL にアクセスしてシリアル化を解除するエージェントの設定を確認できます。

* `https://server:port/system/console/healthcheck?tags=deserialization`

URL にアクセスすると、エージェントに関連するヘルスチェックのリストが表示されます。ヘルスチェックに合格しているかを確認することで、エージェントが正しくアクティベートされているか判断できます。不合格の場合は、エージェントを手動で読み込む必要があります。

エージェントの問題のトラブルシューティングについて詳しくは、以下の[動的なエージェントの読み込みによるエラー処理](#handling-errors-with-dynamic-agent-loading)を参照してください。

>[!NOTE]
>
>`org.apache.commons.collections.functors` を許可リストに追加すると、ヘルスチェックは常に失敗します。

## 動的なエージェントの読み込みによるエラー処理 {#handling-errors-with-dynamic-agent-loading}

ログにエラーがある場合や、検証ステップでエージェントの読み込み時に問題が検出された場合は、エージェントを手動で読み込みます。これは、JDK（Java™ Development Toolkit）ではなく、動的な読み込みを行うツールがない JRE（Java™ Runtime Environment）を使用している場合にも推奨されます。

エージェントを手動で読み込むには、次の手順を実行します。

1. 次のオプションを追加して、CQ JAR の JVM スタートアップパラメーターを編集します。

   ```shell
   -javaagent:<aem-installation-folder>/crx-quickstart/opt/notsoserial/notsoserial.jar
   ```

   >[!NOTE]
   >
   >エージェントはフォークされた JVM では有効にできないので、CQ／AEM の -nofork オプションを、適切な JVM メモリ設定で使用する必要があります。

   >[!NOTE]
   >
   >Adobe 配布版の NotSoSerial エージェント JAR は、AEM インストールの `crx-quickstart/opt/notsoserial/` フォルダーにあります。

1. JVM を停止して再開します。

1. 前述の[エージェントのアクティベートの検証](/help/sites-administering/mitigating-serialization-issues.md#verifying-the-agent-s-activation)のステップに従って、エージェントのアクティベートをもう一度検証します。

## その他の注意点 {#other-considerations}

IBM® JVM 上で実行している場合は、[こちら](https://www.ibm.com/docs/en/sdk-java-technology/8?topic=documentation-java-attach-api)の Java™ Attach API のサポートに関するドキュメントを参照してください。
