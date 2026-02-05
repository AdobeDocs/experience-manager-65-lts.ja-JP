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
source-git-commit: cc96a14ebaf9f895a798b5f4904f5b4769b990bb
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 49%

---

# コンテンツのアーキテクチャ{#content-architecture}

## David&#39;s Model に準拠 {#follow-david-s-model}

David Nuescheler は何年も前に David&#39;s Model を書きましたが、その考え方は今でも当てはまります。 David&#39;s Model の主な考えは以下のとおりです。

* データが第一、構造は二の次（おそらくですが）。
* コンテンツ階層は手動で設定します。手動で設定しないでください。
* ワークスペース は `clone()`、`merge()`、`update()` のためのもの。
* 同じ名前の兄弟に注意する。
* 参照は有害であると見なすことができます。
* ファイルはファイルである。
* ID は有害。

David モデルについては、Jackrabbit wiki（[https://wiki.apache.org/jackrabbit/DavidsModel](https://wiki.apache.org/jackrabbit/DavidsModel)）に詳しい解説があります。

### すべてがコンテンツである {#everything-is-content}

あらゆるデータの格納には、データベースなど別個のサードパーティデータソースを利用するのではなく、リポジトリを使用する必要があります。このようなアプローチは、作成したコンテンツ、画像などのバイナリデータ、コード、設定に適用されます。 1 組の API を使用してすべてのコンテンツを管理し、レプリケーションを通じてこのコンテンツの昇格を管理できます。 また、バックアップやログなどの単一ソースも得られます。

### 「コンテンツモデルが第一」のデザイン原則を使用 {#use-the-content-model-first-design-principle}

新機能をビルドするときには、常に JCR コンテンツ構造の設計から始め、次にデフォルトの Sling サーブレットを使用したコンテンツの読み込みおよび書き込みに進みます。このようなアプローチを使用すると、標準のアクセス制御メカニズムで実装が適切に機能できることを確認でき、不要な CRUD 形式のサーブレットの生成を回避できます。

### RESTful に準拠 {#be-restful}

パスではなく resourceType に基づいてサーブレットを定義します。 このアプローチにより、JCR アクセス制御を使用し、REST 原則に準拠し、リクエストで提供されるリソースおよびリソースリゾルバーを使用できるようになります。 このアプローチを使用すると、クライアントサイド URL を変更せずに、サーバーサイドで URL をレンダリングするスクリプトを変更できます。 また、セキュリティを強化するために、サーバーサイドの実装の詳細をクライアントから非表示にします。

### 新しいノードタイプの定義を回避 {#avoid-defining-new-node-types}

ノードタイプは、インフラストラクチャレイヤーの下位レベルで機能します。 `sling:resourceType`、`nt:unstructured`、`oak:Unstructured` または `sling:Folder` ノードタイプに割り当てられた `cq:Page` を使用することで、ほとんどの要件が満たされます。 ノードタイプはリポジトリではスキーマと同等で、ノードタイプを変更すると後でコストがかかる可能性があります。

### JCR の命名規則に準拠 {#adhere-to-naming-conventions-in-the-jcr}

命名規則に準拠することにより、コードベースの一貫性が高まるので、不具合の発生率を低下させ、システムで作業する開発者の速度を高めることができます。AEM の開発においてアドビが使用した規則は次のとおりです。

* ノード名

   * すべて小文字。
   * ハイフンを使用した単語分離。

* プロパティ名

   * キャメルケース（小文字で始まる）。

* コンポーネント（JSP/HTML）

   * すべて小文字。
   * ハイフンを使用した単語分離。
