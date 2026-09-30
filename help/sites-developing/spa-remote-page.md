---
title: RemotePage コンポーネント
description: RemotePage コンポーネントは、AEM 内のリモート React SPA を編集するためのカスタムページコンポーネントです。
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
exl-id: 9c8dff52-3860-4f71-a0d9-993574f1d654
index: false
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: a9f7d31e-bbe1-4475-966a-5f213546fcd9
    internal-label: SPA Editor
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 96%
---

# RemotePage コンポーネント {#remote-page-component}

外部 SPA と AEM の間でどのレベルの統合を行うかを決める際に、AEM 内で SPA を表示して編集できる必要があることは、多くの場合、明らかです。 RemotePage コンポーネントは、この目的のためのカスタムページコンポーネントです。

## 概要 {#overview}

RemotePage コンポーネントは、アプリケーションで生成された `asset-manifest.json` から必要なアセットをすべて取得し、これを使用して AEM 内の SPA +をレンダリングします。

* RemotePage を使用すると、AEM ページコンポーネントの本文に SPA のスクリプトやスタイルシートを挿入できます。
* 仮想フロントエンドコンポーネントを使用すると、AEM SPA エディターでセクションを編集可能としてマークできます。
* これとともに、異なるドメインでホストされている SPA を AEM で編集可能にすることができます。

AEM の編集可能な外部 SPA の詳細については、[AEM 内の外部 SPA の編集](spa-edit-external.md)を参照してください。

{{ue-over-spa}}

## 要件 {#requirements}

* 開発での CORS の有効化
* ページプロパティでのリモート URL の設定
* AEM での SPA のレンダリング
* web アプリケーションは、次のようなバンドラーアセットマニフェストを使用して、読み込まれるすべての CSS ファイルおよび JS ファイルをエントリポイントプロパティにリストする asset-manifest.json ファイルをドメインルートに公開する必要があります。
  * https://github.com/shellscape/webpack-manifest-plugin
  * https://github.com/webdeveric/webpack-assets-manifest
  * https://github.com/mugi-uno/parcel-plugin-bundle-manifest

  ![エントリポイント](assets/asset-manifest-entrypoints.png)

* アプリケーションは、body 要素の下の `<div id="root"></div>` で初期化できる必要があります。 アプリケーションで異なるマークアップをインスタンス化する必要がある場合は、`sling:resourceSuperType="spa-project-core/components/remotepage` を持つプロキシコンポーネントの HTL スクリプトで適宜調整する必要があります。

## 制限事項 {#limitations}

* RemotePage コンポーネントは、実装がここで見つかった[のようなアセットマニフェストを提供することを想定しています。](https://github.com/shellscape/webpack-manifest-plugin) ただし、RemotePage コンポーネントは React フレームワーク（および remote-page-next コンポーネントを介した Next.js）で動作するようにのみテストされているので、Angular など他のフレームワークからのアプリケーションのリモート読み込みはサポートされていません。
* AEM でリモートレンダリングを行う場合、アプリケーションのルート HTML ファイルに定義された内部 CSS およびルート DOM ノードのインライン CSS は使用できません。

## 技術的詳細 {#technical-details}

AEM SPA プロジェクトの他の部分と同様、RemotePage コンポーネントもオープンソースです。 RemotePage コンポーネントの技術的な詳細については、[GitHub リポジトリを参照してください。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)
