---
title: OWASP Top 10
description: AEM で OWASP Top 10 のセキュリティリスクに対処する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: c49a9876-3a8e-4837-a1a7-e0e62bc60e32
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 100%

---

# OWASP Top 10{#owasp-top}

[Open Web Application Security Project](https://owasp.org/)（OWASP）は、[Top 10 Web Application Security Risks](https://owasp.org/www-project-top-ten/)（Web アプリケーションに関する上位 10 件のセキュリティリスク）のリストを保持しています。

これらのリスクおよび CRX での対処方法を以下に示します。

## 1. インジェクション {#injection}

* SQL - 設計により防止されます。デフォルトのリポジトリ設定には従来のデータベースが含まれず、また必要でもありません。データはすべてコンテンツリポジトリに格納されます。すべてのアクセスは認証されたユーザーに制限され、JCR API を介してのみ実行可能です。SQL は検索クエリ（SELECT）のみをサポートします。さらに、SQL は値バインディングをサポートします。
* LDAP - 認証モジュールによって入力にフィルターが適用され、バインドメソッドを使用してユーザーの読み込みが実行されるので、LDAP インジェクションは不可能です。
* OS - アプリケーション内からのシェル実行はありません。

## 2. クロスサイトスクリプティング（XSS） {#cross-site-scripting-xss}

このリスクを軽減する一般的な方法は、[OWASP Encoder](https://owasp.org/www-project-java-encoder/) と [AntiSamy](https://wiki.owasp.org/index.php/Category:OWASP_AntiSamy_Project) に基づくサーバー側の XSS 保護ライブラリを使用して、ユーザーが生成したコンテンツのすべての出力をエンコードすることです。

XSS はテスト時および開発時における最優先事項であり、検出された問題は（通常）すぐに解決されます。

## 3. 認証とセッション管理の不備 {#broken-authentication-and-session-management}

AEM では、[Apache Jackrabbit](https://jackrabbit.apache.org/jcr/index.html) と [Apache Sling](https://sling.apache.org/) に基づく、堅実で実績のある認証手法を利用しています。ブラウザー／HTTP セッションは AEM では使用されません。

## 4. 安全でないオブジェクト直接参照 {#insecure-direct-object-references}

データオブジェクトへのすべてのアクセスは、リポジトリが介在するので、役割に基づくアクセス制御によって制限されます。

## 5. クロスサイトリクエストフォージェリー（CSRF） {#cross-site-request-forgery-csrf}

クロスサイトリクエストフォージェリ（CSRF）は、暗号トークンをあらゆる形式および AJAX リクエストに自動的に注入し、すべての POST についてこのトークンをサーバー上で検証することで軽減されます。

さらに、AEM に搭載されているリファラーヘッダーベースのフィルターを設定して、特定のホスト（リストで定義）からの POST リクエスト&#x200B;*のみ*&#x200B;を許可することができます。

## 6. セキュリティ設定のミス {#security-misconfiguration}

すべてのソフトウェアを常に正しく設定した状態にしておくことは不可能です。しかし、アドビでは、できるだけ多くのガイダンスを提供し、設定をできるだけシンプルにするよう努めています。さらに、AEM に搭載されている[セキュリティヘルスチェック機能](/help/sites-administering/operations-dashboard.md)により、一目でセキュリティ設定を監視できます。

詳しくは、[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を参照してください。セキュリティ強化の手順を段階的に説明します。

## 7. 安全でない暗号化データの保管 {#insecure-cryptographic-storage}

パスワードは暗号化ハッシュとしてユーザーノードに格納されます。デフォルトでは、このようなノードは管理者とユーザー自身だけが確認できます。

サードパーティの資格情報などのような重要な情報は、FIPS 140-2 認定を受けた暗号ライブラリを使用して、暗号化された形式で保存されます。

## 8. URL アクセス制限の失敗 {#failure-to-restrict-url-access}

リポジトリでは、アクセス制御エントリを使用して、特定のパスの特定のユーザーまたはグループに対して[（JCR で指定された）詳細な権限](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html)を設定できます。アクセス制限はリポジトリによって適用されます。

## 9. 不十分なトランスポート層の保護 {#insufficient-transport-layer-protection}

サーバー設定（例：HTTPS のみの使用）によって軽減されます。

## 10. 未検証のリダイレクトとフォワード {#unvalidated-redirects-and-forwards}

ユーザーが指定した宛先へのすべてのリダイレクトを内部の場所に制限することで軽減されます。
