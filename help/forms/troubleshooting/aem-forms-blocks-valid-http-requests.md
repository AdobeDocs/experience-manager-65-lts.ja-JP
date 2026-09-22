---
title: AEM Formsは有効なHTTP リクエストをブロックします
description: AEM Forms XSS検証チェックは、カスタムコンポーネントを使用して、お客様に対する有効なHTTP リクエストをブロックできます。 問題を特定し、検証チェックを一時的に緩和する方法について説明します。
solution: Experience Manager, Experience Manager Forms
feature: Security
role: Admin,Developer
exl-id: 10a02e57-7ff8-42d8-b31e-f714c0dd8338
source-git-commit: 4df5a9888532afd86562678a76c35841ac5634b8
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 8%
---
# AEM Formsは有効なHTTP リクエストをブロックします {#aem-forms-blocks-valid-http-requests}

## 問題 {#issue}

AEM Formsでは、クロスサイトスクリプティング（XSS）攻撃を防止するためのセキュリティチェックが用意されています。 これらのチェックは、AEM Formsでカスタムコンポーネントを使用するお客様に対して、有効なHTTP リクエストの一部をブロックする可能性があります。 リクエストがブロックされると、サーバーログに次のメッセージが表示されます。

```text
Got Exception while Validating XSS: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000: org.owasp.esapi.errors.ValidationException: HTTP parameter name: params[browserLocale]: Invalid input. Please conform to regex ^[a-zA-Z0-9_]{1,32}$ with a maximum length of 2000.
```

>[!NOTE]
>
>POST リクエストの場合、パラメーターのデフォルト値は&#x200B;**1048576**&#x200B;です。 GET リクエストの場合、パラメーターのデフォルト値は&#x200B;**2000**&#x200B;です。 POST リクエストのパラメーター値を変更するには、サーバーの起動時に`com.adobe.idp.dsc.provider.rest.httpParamMaxSize`引数を渡します。

## 原因 {#cause}

XSS検証正規表現は、カスタムコンポーネントによって送信されるパラメーター値のフォーマットよりも厳しいため、AEM Formsはリクエストを拒否します。

## 解決策 {#resolution}

>[!CAUTION]
>
>セキュリティチェックを削除すると、システムがクロスサイトスクリプティング（XSS）攻撃に対して脆弱になります。 セキュリティチェックは一時的な解決策としてのみ削除してください。

セキュリティチェックを一時的に削除し、すべてのHTTP リクエストを許可するには：

1. AEM Forms サーバーを停止します。

1. `[AEM-Forms-Installation-Directory]/configurationManager/export/adobe-livecycle-<application_server_name>.ear` ファイルのバックアップを作成します。

1. `adobe-livecycle-<server_name>.ear` ファイルから`esapi-helper-2.x.x.jar` ファイルを抽出します。 `esapi-helper-2.x.x.jar` ファイルの場所は、アプリケーション サーバーごとに異なります。

   | アプリケーションサーバー | esapi-helper-2.x.x.jar ファイルの場所 |
   | --- | --- |
   | JBoss | `adobe-livecycle-jboss.ear/lib` |
   | Oracle WebLogic | `adobe-livecycle-weblogic.ear/APP-INF/lib` |
   | IBM WebSphere | `adobe-livecycle-websphere.ear/` |

1. `[extracted esapi-helper-2.x.x.jar]/esapi/validation.properties`および`[extracted esapi-helper-2.x.x.jar]/esapi/ESAPI.properties` ファイルを開いて編集します。

1. 次のプロパティの値を`^[\\s\\S]*$`に設定します。 例えば、`Validator.HTTPParameterName=^[\\s\\S]*$` のようになります。 ファイルを保存して閉じます。

   * `Validator.HTTPQueryString`
   * `Validator.PMCallParameterName`
   * `Validator.PMCallParameterValue`
   * `Validator.HTTPParameterName`
   * `Validator.HTTPParameterValue`
   * `Validator.xssSafeString`

1. 更新した`esapi-helper-2.x.x.jar`を`adobe-livecycle-<application_server_name>.ear`にパッケージ化します。 更新した`adobe-livecycle-<application_server_name>.ear`をアプリケーションサーバーにデプロイします。

1. AEM Forms サーバーを起動します。

## 参照 {#references}

* [JEE 6.5 LTS SP2上のAEM Formsのサーバーサイド要求フォージェリー（SSRF）の脆弱性を軽減する](/help/forms/troubleshooting/mitigating-server-side-request-forgery-vulnerabilities-for-aem-forms-on-jee-65-lts-sp2.md)
