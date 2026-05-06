---
title: 技術的なよくある質問（FAQ）
description: AEM 6.5 LTS に関する技術的なよくある質問です。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: 89016492c069d61c18f9bf83bfb896cd78fb20fd
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 75%

---

# AEM 6.5 LTS に関する技術的なよくある質問（FAQ） {#technical-faq}

このページは、AEM 6.5 LTS に関する技術的なよくある質問への回答を目的としています。

## 技術的な FAQ

### AEM 6.5 LTS では `/systemalive` エンドポイントが使用できなくなりました。

`/systemalive` エンドポイントを提供するように設定された Felix System Ready バンドルは非推奨（廃止予定）になり、Apache Felix ヘルスチェックに置き換えられました。 このバンドルは、AEM 6.5 LTS には含まれなくなりました。

新しいヘルスチェックエンドポイントは、`/system/health` で使用でき、Apache Felix ヘルスチェックを使用して実装されます。

Felix ヘルスチェックフレームワークに関するドキュメントについて詳しくは、[felix ドキュメント](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md)を参照してください。

### AEM Groovy Consoleのサポート

AEM 6.5で使用されていたAEM Groovy コンソールバージョンは、guavaの依存関係が欠落しているため、AEM 6.5 LTSで機能しない可能性があります。 新しくサポートされるAEM Groovy Consoleのバージョンは[19.0.8](https://github.com/orbinson/aem-groovy-console/releases/download/19.0.8/aem-groovy-console-all-19.0.8.zip)です。

#### AEM Groovy Consoleに必要な追加の設定

AEM Groovy Consoleを使用している場合は、`com.adobe.granite.apicontroller.FilterResolverHookFactory`に対して次のOSGi設定を明示的に追加する必要があります。 `aem-groovy-console-bundle`を`org.apache.sling.distribution.api` キーの許可されたバンドルリストに追加し、プラットフォームのデフォルトを拡張します。

```
"org.apache.sling.distribution.api": "com.adobe.*,com.day.*,org.apache.sling.*,aem-groovy-console-bundle"
```

### AEM 6.5 LTS はユーザー同期をサポートしていますか？

はい、AEM 6.5 LTS はユーザー同期をサポートしています。 AEM 6.5 と 6.5 LTS の間でユーザー同期の機能に変更はありません。

### Maven Central の Uber JAR が破損しているようです。問題は何ですか？

`apis` 分類子で Uber JAR を使用していることを確認します。 AEM 6.5 LTS では、Uber JAR のパッケージ構造が変更されていることに注意してください。 詳しくは、[AEM Uber Jar バージョンの更新](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version)を参照してください。

## 追加のヘルプの入手

ここで説明されていない問題が発生した場合：
* 既知の問題について詳しくは、[リリースノート](/help/release-notes/release-notes.md)を参照してください。
* サポートが必要な場合は、アドビサポートにお問い合わせください。
