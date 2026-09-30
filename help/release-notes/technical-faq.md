---
title: 技術的なよくある質問（FAQ）
description: AEM 6.5 LTS に関する技術的なよくある質問です。
solution: Experience Manager
feature: Release Information
role: User,Admin,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: ed762d86-a04b-452b-a08f-86359bb8ff27
    internal-label: Configuration and operations
subfeature_v2:
  - id: c21ccc2b-e0c8-4853-bf41-f12259ed93f8
    internal-label: Release information
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 59%
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

### AEM 6.5 LTSは、`jakarta.*` パッケージ名前空間（例：`jakarta.annotation`）をサポートしていますか？

いいえ。 AEM 6.5 LTSは、`jakarta.*` パッケージ名前空間に移行されたSling アーティファクトをサポートしていません。 コードと依存関係で`javax.*`の同等のものを使用します。例えば、`jakarta.annotation.PostConstruct`ではなく`javax.annotation.PostConstruct`をSling モデルで使用します。 AEM 6.5 LTSのSling モデルの実装では、`javax.*`個の注釈のみが認識されるため、`jakarta.*`個の注釈は初期化中に無視されます。

詳しくは、ナレッジベースの記事「[Sling Models with `jakarta.annotation.PostConstruct` fail on AEM 6.5 LTS](https://experienceleague.adobe.com/ja/docs/experience-cloud-kcs/kbarticles/ka-30339)」を参照してください。

## 追加のヘルプの入手

ここで説明されていない問題が発生した場合：
* 既知の問題について詳しくは、[リリースノート](/help/release-notes/release-notes.md)を参照してください。
* サポートが必要な場合は、アドビサポートにお問い合わせください。
