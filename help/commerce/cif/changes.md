---
title: コマース統合フレームワーク（CIF）アドオンの主な変更点
description: 以前のバージョンと比較した、コマース統合フレームワーク（CIF）アドオンの主な変更点です。
solution: Experience Manager,Commerce
feature: Commerce Integration Framework
role: Admin, Developer
exl-id: aced89a0-dec1-49fe-afbc-3ddf1318b900
source-git-commit: 79cce324382bada2e9aec107b8e494723bf490e9
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 99%

---

# コマース統合フレームワーク（CIF）アドオンの主な変更点{#notable-changes}

このドキュメントでは、主に CIF Classic（Quickstart）と CIF Open-source と呼ばれる、コマース統合フレームワーク（CIF）アドオンと古い CIF バージョンの重要な相違点について説明します。

## インストールとアップデート

AEM Package Manager で AEM CIF アドオンパッケージがインストールされ更新されます。

**以前の CIF バージョン**

* CIF Classic：インストールは不要で、CIF は Quickstart の一部でした。CIF のアップデートは、通常の AEM またはサービスパックのアップデートに含まれていました。
* CIF オープンソース：GitHub を介したインストールアップデートは、手動アップデートやメンテナンス作業の一部でした。

## エンドポイントの設定

エンドポイントは OSGi コンソールを介して設定されます。

**以前の CIF バージョン**

* CIF Classic：AEM の OSGi 設定を使用
* CIF Open-source：CIF 設定ブラウザーを使用

## CIF Venia プロジェクトのデプロイメント

プロジェクトは [GitHub AEM Guides - CIF Venia Project](https://github.com/adobe/aem-cif-guides-venia) で入手可能で、デプロイメントは AEM Package Manager で行われます。

**以前の CIF バージョン**

* CIF Classic：AEM パッケージのインストールを使用

## 製品カタログデータ

製品カタログデータは、必要な GraphQL API をサポートする外部エンドポイントへのリアルタイム呼び出しを通じて、オンデマンドでリクエストされます。これらの API は、任意の日付のライブデータまたはステージングデータへのアクセスをサポートします。レプリケーションは不要です。

**以前の CIF バージョン**

* CIF Classic：ライブおよびステージングされた製品データは、完全または差分の製品読み込みを通じて AEM オーサー上の JCR に読み込まれ、保持されます。ライブ製品データが AEM パブリッシュにレプリケートされます。

## AEM レンダリングを使用した製品カタログエクスペリエンス

AEM は、製品やカテゴリに割り当てられた AEM カタログテンプレートを使用して、製品カタログエクスペリエンスをその場でレンダリングします。レプリケーションは不要です。

**以前の CIF バージョン**

* CIF Classic：AEM オーサーは、カタログのブループリントツールを使用して、各カテゴリ／製品の AEM ページを作成します。これらのページは AEM パブリッシュにレプリケートされます。

>[!NOTE]
>
>AEM Managed Service または AEM オンプレミスで CIF を使用する方法に関する追加ドキュメントについて詳しくは、[コマース統合フレームワーク](https://developer.adobe.com/apis/experiencecloud/commerce-integration-framework/getting-started.html)を参照してください。
