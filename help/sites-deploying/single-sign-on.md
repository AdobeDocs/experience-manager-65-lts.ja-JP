---
title: シングルサインオン
description: Adobe Experience Manager（AEM）のインスタンスにシングルサインオン（SSO）を設定する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring, Security
content-type: reference
feature: Security
solution: Experience Manager, Experience Manager Sites
role: Admin
exl-id: 1c437771-cec5-48b8-8d77-a66c269420ec
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 100%

---

# シングルサインオン {#single-sign-on}

シングルサインオン（SSO）では、ユーザーが認証の資格情報（ユーザー名、パスワードなど）を一度入力すると、複数のシステムにアクセスできるようになります。別個のシステム（信頼された認証と呼ばれます）が認証を実行し、Experience Manager にユーザーの資格情報を提供します。Experience Manager は、ユーザーのアクセス権限を確認および強制します（つまり、ユーザーがアクセスできるリソースを決定します）。

SSO 認証ハンドラーサービス（`com.adobe.granite.auth.sso.impl.SsoAuthenticationHandler`）は、信頼された認証が提供する認証結果を処理します。SSO 認証ハンドラーは、次の順序で特別な属性の値として SSO 識別子（SSID）を検索します。

1. リクエストヘッダー
1. Cookie
1. リクエストパラメーター

値が見つかると検索が終了し、この値が使用されます。

この SSID を格納する属性の名前を認識できるように次の 2 つのサービスを設定します。

* ログインモジュール。
* SSO 認証サービス。

両方のサービスに同じ属性名を指定します。属性は `Repository.login` に提供される `SimpleCredentials` が含められます。属性の値は無関係で無視されます。単に存在していることが重要で検証されます。

## SSO の設定 {#configuring-sso}

AEM インスタンスの SSO を設定するには、[SSO 認証ハンドラー](/help/sites-deploying/osgi-configuration-settings.md#adobegranitessoauthenticationhandler)を設定します。

1. AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項について詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

   例えば、NTLM の場合は次のように設定します。

   * **パス：**&#x200B;必要に応じて設定します（`/` など）。
   * **ヘッダー名**：`LOGON_USER`
   * **ID 形式**：`^<DOMAIN>\\(.+)$`

     ここで、`<*DOMAIN*>` は、独自のドメインの名前に置き換えられます。

   CoSign の場合：

   * **パス：**&#x200B;必要に応じて設定します（`/` など）。
   * **ヘッダー名**：remote_user
   * **ID 形式**：AsIs

   SiteMinder の場合：

   * **パス**：必要に応じて設定します（`/` など）。
   * **ヘッダー名**：SM_USER
   * **ID 形式**：AsIs

1. 認証を含め、シングルサインオンが要求どおりに動作していることを確認します。

>[!CAUTION]
>
>SSO を設定した場合は、ユーザーが直接 AEM にアクセスできないことを確認します。
>
>SSO システムのエージェントを実行する web サーバー経由でアクセスするようにユーザーに要求することで、ユーザーが AEM に信頼されるように導くヘッダー、Cookie またはパラメーターを直接送信できなくなります。そのような情報が外部から送信された場合には、エージェントがフィルタリングするからです。
>
>Web サーバーを経由せずに AEM インスタンスに直接アクセスできるユーザーは、別の既知のユーザーのヘッダー、Cookie またはパラメーターを送信することで、そのユーザーとして行動できます。
>
>また、ヘッダー、Cookie、リクエストパラメーター名のうち、SSO 設定に必要なものだけを設定します。
>

>[!NOTE]
>
>シングルサインオンは、多くの場合、[LDAP](/help/sites-administering/ldap-config.md) で使用されます。

>[!NOTE]
>
>Microsoft® Internet Information Server（IIS）と共に [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) も使用している場合は、次に追加の設定を行う必要があります。
>
>* `disp_iis.ini`
>* IIS
>
>`disp_iis.ini` で次のように設定します。
>（詳しくは、[Dispatcher を Microsoft® Internet Information Server と共にインストールする方法に関するページ](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html?lang=ja#microsoft-internet-information-server)を参照してください）
>
>* `servervariables=1`（IIS サーバー変数をリクエストヘッダーとしてリモートインスタンスに転送します）
>* `replaceauthorization=1`（「Basic」を除く、「Authorization」という名前のすべてのヘッダーを「Basic」と同等のものに置き換えます）
>
>IIS では、次のように設定します。
>
>* **匿名アクセス**&#x200B;を無効にする
>
>* **統合 Windows 認証**&#x200B;を有効にします
>

Felix コンソールの「**Authenticator**」オプションを使用すると、コンテンツツリーのすべてのセクションに適用される認証ハンドラーを確認できます。次に例を示します。

`http://localhost:4502/system/console/slingauth`

パスに最適なハンドラーが最初に照会されます。例えば、パス `/` に handler-A を設定し、パス `/content` に handler-B を設定すると、`/content/mypage.html` へのリクエストに対して handler-B が最初に照会されます。

![screen_shot_2012-02-15at21006pm](assets/screen_shot_2012-02-15at21006pm.png)

### 例 {#example}

cookie リクエスト（URL `http://localhost:4502/libs/wcm/content/siteadmin.html` を使用）の例を次に示します。

```xml
GET /libs/cq/core/content/welcome.html HTTP/1.1
Host: localhost:4502
Cookie: TestCookie=admin
```

次の設定を使用します。

* **パス**：`/`

* **ヘッダー名**：`TestHeader`

* **cookie 名**：`TestCookie`

* **パラメーター名**：`TestParameter`

* **ID 形式**：`AsIs`

応答は次のようになります。

```xml
HTTP/1.1 200 OK
Connection: Keep-Alive
Server: Day-Servlet-Engine/4.1.24
Content-Type: text/html;charset=utf-8
Date: Thu, 23 Aug 2012 09:58:39 GMT
Transfer-Encoding: chunked

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "https://www.w3.org/TR/html4/strict.dtd">
<html>
<head>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <title>Welcome to Adobe&reg; CQ5</title>
....
```

これは、次をリクエストした場合にも機能します。
`http://localhost:4502/libs/cq/core/content/welcome.html?TestParameter=admin`

または、次の curl コマンドを使用して、`TestHeader` ヘッダーを `admin:` に送信します
`curl -D - -H "TestHeader: admin" http://localhost:4502/libs/cq/core/content/welcome.html`

>[!NOTE]
>
>ブラウザーでリクエストパラメーターを使用すると、HTML の一部のみが表示されます（CSS は表示されません）。これは、HTML からのリクエストはすべてリクエストパラメーターなしで行われるからです。

## AEM ログアウトリンクの削除 {#removing-aem-sign-out-links}

SSO を使用する場合、ログインとログアウトは外部で処理されるので、AEM 独自のログアウトリンクは使用できなくなり、削除する必要があります。

ようこそ画面のログアウトリンクは、次の手順で削除できます。

1. `/libs/cq/core/components/welcome/welcome.jsp` を `/apps/cq/core/components/welcome/welcome.jsp` にオーバーレイします
1. jsp の以下の部分を削除します。

   `<a href="#" onclick="signout('<%= request.getContextPath() %>');" class="signout"><%= i18n.get("sign out", "welcome screen") %>`

右上隅にあるユーザーの個人メニューのログアウトリンクを削除するには、次の手順に従います。

1. `/libs/cq/ui/widgets/source/widgets/UserInfo.js` を `/apps/cq/ui/widgets/source/widgets/UserInfo.js` にオーバーレイします

1. ファイルの以下の部分を削除します。

   ```
   menu.addMenuItem({
       "text":CQ.I18n.getMessage("Sign out"),
       "cls": "cq-userinfo-logout",
       "handler": this.logout
   });
   menu.addSeparator();
   ```
