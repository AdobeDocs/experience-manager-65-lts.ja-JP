---
title: SAML 2.0 認証ハンドラー
description: AEM での SAML 2.0 認証ハンドラーについて説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
exl-id: ee438c55-88cd-4f55-873e-16376b36fa7b
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 100%

---

# SAML 2.0 認証ハンドラー {#saml-authentication-handler}

AEM には、[SAML](https://saml.xml.org/saml-specifications) 認証ハンドラーが付属しています。このハンドラーによって、`HTTP POST` バインディングを使用した [SAML](https://saml.xml.org/saml-specifications) 2.0 認証リクエストプロトコル（Web-SSO プロファイル）がサポートされます。

サポート対象は次のとおりです。

* メッセージの署名と暗号化
* ユーザーの自動作成
* AEM でグループを既存のグループに同期させる
* サービスプロバイダーと ID プロバイダーで開始される認証

このハンドラーは、暗号化された SAML 応答メッセージをユーザーノード（`usernode/samlResponse`）に格納して、サードパーティのサービスプロバイダーとの通信を容易にします。

>[!NOTE]
>
>[AEM と SAML の統合のデモンストレーション](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17481.html?lang=ja)を参照してください。

## SAML 2.0 認証ハンドラーの設定 {#configuring-the-saml-authentication-handler}

[Web コンソール](/help/sites-deploying/configuring-osgi.md)を使用すると、[SAML](https://saml.xml.org/saml-specifications) 2.0 認証ハンドラーの設定（**Adobe Granite SAML 2.0 Authentication Handler**）にアクセスできます。設定可能なプロパティを以下に示します。

>[!NOTE]
>
>SAML 2.0 認証ハンドラーはデフォルトでは無効になっています。このハンドラーを有効にするには、少なくとも次のどちらかのプロパティを設定します。
>
>* ID プロバイダーの POST URL または IDP URL。
>* サービスプロバイダーのエンティティ ID
>

>[!NOTE]
>
>SAML アサーションは署名されます。オプションとして暗号化することもできます。そのためには、少なくとも ID プロバイダーの公開証明書を TrustStore に指定する必要があります。詳しくは、[TrustStore への IdP 証明書の追加](/help/sites-administering/saml-2-0-authenticationhandler.md#add-the-idp-certificate-to-the-aem-truststore)のセクションを参照してください。

**パス** この認証ハンドラーが Sling によって使用される場合のリポジトリのパスです。このプロパティが空の場合は、認証ハンドラーが無効になります。

**サービスランキング** このサービスを呼び出す順序を示す OSGi フレームワークサービスランキングの値です。これは整数値で、値が大きいほど優先順位が高くなります。

**IDP 証明書エイリアス** グローバル TrustStore における IdP の証明書のエイリアスです。このプロパティが空の場合は、認証ハンドラーが無効になります。設定方法は、以下の「AEM TrustStore への IdP 証明書の追加」を参照してください。

**IDP URL** SAML 認証要求を送信する必要のある IDP の URL です。このプロパティが空の場合は、認証ハンドラーが無効になります。

>[!CAUTION]
>
>ID プロバイダーのホスト名は **Apache Sling Referrer Filter** の OSGi 設定に追加する必要があります。詳しくは、[Web コンソール](/help/sites-deploying/configuring-osgi.md)の節を参照してください。

**サービスプロバイダーのエンティティ ID** このサービスプロバイダーを ID プロバイダーとして一意に識別する ID です。このプロパティが空の場合は、認証ハンドラーが無効になります。

**デフォルトのリダイレクト** 認証が成功した後のデフォルトのリダイレクト先です。

>[!NOTE]
>
>この場所は、`request-path` の Cookie が設定されていない場合にのみ使用されます。有効なログイントークンを使用せずに、設定済みのパスの下にあるページを要求すると、要求されたパスは Cookie に格納され、
>認証が成功した後にブラウザーは再びこの場所にリダイレクトされます。

**ユーザー ID 属性** CRX リポジトリでのユーザーの認証および作成に使用されるユーザー ID を格納する属性の名前です。

>[!NOTE]
>
>ユーザー ID は SAML アサーションの `saml:Subject` ノードではなく、この `saml:Attribute` から取得されます。

**暗号化を使用** この認証ハンドラーが暗号化された SAML アサーションを使用するかどうかを示します。

**CRX ユーザーを自動作成** 認証が成功した後に、リポジトリで既存のユーザー以外のユーザーを自動的に作成するかどうかを示します。

>[!CAUTION]
>
>CRX ユーザーの自動作成が無効な場合は、ユーザーを手動で作成する必要があります。

**グループに追加** 認証が成功した後に、CRX グループにユーザーを自動的に追加する必要があるかどうかを示します。

**グループメンバーシップ** このユーザが追加されるべき CRX グループのリストを含む saml:Attribute の名前です。

## AEM TrustStore への IdP 証明書の追加 {#add-the-idp-certificate-to-the-aem-truststore}

SAML アサーションは署名されます。オプションとして暗号化することもできます。そのためには、少なくともリポジトリ内の IDP の公開証明書を指定する必要があります。それには、次を実行する必要があります。

1. *http:/serveraddress:serverport/libs/granite/security/content/truststore.html* に移動します。
1. **[!UICONTROL TrustStore リンクを作成]** を押します。
1. TrustStore のパスワードを入力して「**[!UICONTROL 保存]**」を押します。
1. 「**[!UICONTROL TrustStore を管理]**」をクリックします。
1. IdP 証明書をアップロードします。
1. 証明書エイリアスを記録します。以下の例では、エイリアスは **[!UICONTROL admin#1436172864930]** です。

   ![chlimage_1-372](assets/chlimage_1-372.png)

## AEM キーストアへのサービスプロバイダーキーと証明書チェーンを追加 {#add-the-service-provider-key-and-certificate-chain-to-the-aem-keystore}

>[!NOTE]
>
>以下のステップは必須です。実行しないと、次の例外が発生します。`com.adobe.granite.keystore.KeyStoreNotInitialisedException: Uninitialised system trust store`

1. [http://localhost:4502/libs/granite/security/content/useradmin.html](http://localhost:4502/libs/granite/security/content/useradmin.html) に移動します。
1. `authentication-service` ユーザーを編集します。
1. **アカウント設定** の **キーストアを作成** をクリックしてキーストアを作成します。

>[!NOTE]
>
>以下のステップは、ハンドラーが署名またはメッセージを複合化できるようにする必要がある場合にのみ必須です。

1. AEM の証明書／鍵のペアを作成します。OpenSSL を使用して生成するコマンドは、次の例のようになります。

   `openssl req -newkey rsa:2048 -new -x509 -days 3652 -nodes -out certificate.crt -keyout key.pem`

1. キーを DER エンコードを使用して PKCS#8 形式に変換します。これは、AEM キーストアで必要な形式です。

   `openssl pkcs8 -topk8 -inform PEM -outform DER -in key.pem -out key.der -nocrypt`

1. **秘密鍵ファイルを選択** をクリックして秘密鍵ファイルをアップロードします。
1. 「**証明書チェーンファイルを選択**」をクリックして証明書ファイルをアップロードします。
1. 以下のようにエイリアスを割り当てます。

   ![chlimage_1-373](assets/chlimage_1-373.png)

## SAML 用のロガーの設定 {#configure-a-logger-for-saml}

SAML の設定ミスにより発生する可能性があるすべての問題をデバッグするようにロガーを設定できます。手順は次のとおりです。

1. Web コンソール（*http://localhost:4502/system/console/configMgr*）に移動
1. **Apache Sling Logging Logger Configuration** という名前のエントリを検索してクリックします。
1. 次の設定でロガーを作成します。

   * **Log Level：** Debug
   * **Log File：** logs/saml.log
   * **Logger：** com.adobe.granite.auth.saml
