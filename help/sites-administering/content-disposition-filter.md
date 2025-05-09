---
title: Content Disposition フィルター
description: Content Disposition フィルターを使用して XSS 攻撃を防ぐ方法について説明します。
contentOwner: trushton
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: Security
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
exl-id: 997cb6f3-1ef8-409c-acea-157d5b27a6b2
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 100%

---

# Content Disposition フィルター {#content-disposition-filter}

Content Disposition フィルターは、SVG ファイルへの XSS 攻撃に対するセキュリティ機能です。

インストールが完了すると、フィルターはすべてのアセットへのアクセスをブロックします。例えば、オンラインで PDF を表示することができなくなります。この節では、必要に応じてフィルターを設定する方法について説明します。

## Content Disposition フィルターを設定 {#configure-content-disposition-filter}

[GitHub で Apache Sling の Content Disposition フィルター](https://github.com/apache/sling-org-apache-sling-security/blob/master/src/main/java/org/apache/sling/security/impl/ContentDispositionFilterConfiguration.java)を参照できます。

Content Disposition フィルターのオプションには、次の機能があります。

* **Content Disposition パス**：フィルターが適用されるパスのリストと、そのパスで除外する MIME タイプのリストが続きます。このパスは絶対パスにする必要があり、指定されたパスプレフィックスを持つすべてのリソースパスと一致させるために、末尾にワイルドカード（`*`）を含めることができます。例：`/content/*:image/jpeg,image/svg+xml` は、JPG および SVG 画像を除く、`/content?` のすべてのノードにフィルターを適用します。

* **除外されたリソースパス：**&#x200B;除外されたリソースのリストです。各リソースパスは絶対パスおよび完全修飾パスとして指定する必要があります。プレフィックスマッチング／ワイルドカードはサポートされていません。

* **すべてのリソースパスを有効化：**&#x200B;このフラグは、除外されたリソースパスで定義されたパス以外のすべてのパスに対して、このフィルターを有効にするかどうかを制御します。このフラグを「true」に設定すると、Content Disposition パスが無視されます。設定に関係なく、`jcr:data` または `jcr:content/jcr:data` という名前のプロパティを含むリソースパスのみが対象になります。
