---
title: Adobe Experience Manager Forms 6.5 LTS SP1 ホットフィックス
description: AEM Forms 6.5 LTS のホットフィックスをダウンロードしてインストールする方法について説明します。
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 979a817293034d09189417cdf729f476c77cdde3
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 45%

---


# Adobe Experience Manager Forms 6.5 LTS ホットフィックス{#aem-form-hotfix}

この記事では、既知の問題への対処、システムの安定性の向上、AEM Forms 6.5 LTS の全体的なパフォーマンスの向上のために実装された重要な修正を一覧表示しています。


>[!NOTE]
>
> ホットフィックスは累積的に設計されており、以前のすべての修正が含まれます。 最新のホットフィックスをリリースに適用すると、最新の問題に対処するだけでなく、以前のすべてのバグ修正と機能強化も組み込まれます。

## AEM Forms 6.5 LTS のホットフィックス {#hotfix-for-aem-forms}

<table>
  <tbody>
  <tr>
    <td><strong>日付</strong></td>
    <td><strong>ホットフィックスのダウンロードリンク（AEM ソフトウェア配布リンク）</strong></td>
    <td><strong>修正された問題</strong></td>
  </tr>
  <tr>
    <td>
      <strong>2025 年 9 月 9 日 </strong><br>
    <td>
    <ul>
    <li>Windows- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-win-pkg-6.1.176-RHF-002.zip">Windows のAEM サービスパック 6.5 LTS のホットフィックス 2</a></li>
    <li>Linux- <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]hotfix-on-add-on/adobe-aemfd-linux-pkg-6.1.176-RHF-002.zip">Linux のAEM サービスパック 6.5 LTS のホットフィックス 2</a></li>
     <li>MacOS- MacOSのAEM サービスパック 6.5 LTS の <a href="https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]1-hotfix-on-add-on/adobe-aemfd-osx-pkg-6.1.176-RHF-002.zip">Hotfix2</a></li>
    <td>
    <ul>
    <li>サーバーサイド検証（SSV）が有効になっている場合に送信が失敗する可能性がある問題に対処して、フォーム送信の信頼性を向上しました。問題が発生した場合は、[Adobe Experience Manager Forms サポート ] （https://business.adobe.com/in/support/main.html）にお問い合わせください
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
