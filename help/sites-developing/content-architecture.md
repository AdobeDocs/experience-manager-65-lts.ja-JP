---
title: コンテンツのアーキテクチャ
description: コンテンツをアーカイブするためのヒント（ヒント：すべてがコンテンツ）
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
exl-id: eb47f730-ac26-47a0-9bd7-3b7e94c79ecd
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 50%
---
# コンテンツのアーキテクチャ{#content-architecture}

## David&#39;s Model に準拠 {#follow-david-s-model}

David Nueschelerは何年も前にDavid&#39;s Modelを書きましたが、そのアイデアは今日でも真実です。 David&#39;s Model の主な考えは以下のとおりです。

* データが第一、構造は二の次 （おそらくですが）。
* コンテンツ階層を促進します。それを起こさせないでください。
* ワークスペース は `clone()`、`merge()`、`update()` のためのもの。
* 同じ名前の兄弟に注意する。
* 参照は有害と見なすことができます。
* ファイルはファイルである。
* ID は有害。

David モデルについては、Jackrabbit wiki（[https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)）に詳しい解説があります。

### すべてがコンテンツである {#everything-is-content}

あらゆるデータの格納には、データベースなど別個のサードパーティデータソースを利用するのではなく、リポジトリを使用する必要があります。 このようなアプローチは、作成されたコンテンツ、画像、コード、設定などのバイナリデータに適用されます。 これにより、1つのAPI セットを使用してすべてのコンテンツを管理し、レプリケーションを通じてこのコンテンツのプロモーションを管理できます。 また、バックアップやログなどの単一ソースも得られます。

### 「コンテンツモデルが第一」のデザイン原則を使用 {#use-the-content-model-first-design-principle}

新機能をビルドするときには、常に JCR コンテンツ構造の設計から始め、次にデフォルトの Sling サーブレットを使用したコンテンツの読み込みおよび書き込みに進みます。 このようなアプローチにより、実装がすぐに使用できるアクセス制御メカニズムで適切に機能することを確認し、不要なCRUD スタイルのサーブレットの生成を回避できます。

### RESTful に準拠 {#be-restful}

パスではなくresourceTypeに基づいてサーブレットを定義します。 このアプローチにより、JCR アクセス制御を使用し、RESTの原則に従い、リクエストで提供されるリソースとリソースリゾルバーを使用することが可能になります。 この方法では、クライアントサイド URLを変更することなく、サーバーサイドでURLをレンダリングするスクリプトを変更できます。 また、セキュリティを強化するために、クライアントからサーバーサイド実装の詳細を非表示にします。

### 新しいノードタイプの定義を回避 {#avoid-defining-new-node-types}

ノードタイプは、インフラストラクチャ層で低レベルで動作します。 ほとんどの要件は、`nt:unstructured`、`oak:Unstructured`、`sling:Folder`または`cq:Page` ノードタイプに割り当てられた`sling:resourceType`を使用することで満たされます。 ノードタイプはリポジトリではスキーマと同等で、ノードタイプを変更すると後でコストがかかる可能性があります。

### JCR の命名規則に準拠 {#adhere-to-naming-conventions-in-the-jcr}

命名規則に準拠することにより、コードベースの一貫性が高まるので、不具合の発生率を低下させ、システムで作業する開発者の速度を高めることができます。 AEM の開発においてアドビが使用した規則は次のとおりです。

* ノード名

  * すべて小文字です。
  * ハイフンを使用した単語の分離。

* プロパティ名

  * 小文字で始まるキャメルケース。

* コンポーネント（JSP/HTML）

  * すべて小文字です。
  * ハイフンを使用した単語の分離。
