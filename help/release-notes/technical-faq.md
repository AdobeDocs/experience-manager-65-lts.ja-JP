---
title: 技術的なよくある質問（FAQ）
description: AEM 6.5 LTS に関する技術的な FAQ
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
exl-id: 051244f1-cc67-4222-bd45-0c135c28bb15
source-git-commit: ec722773ce3acff1d0de861523db8ff7df552c4b
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 2%

---

# AEM 6.5 LTS テクニカル FAQ {#technical-faq}

ここでは、AEM 6.5 LTS に関するよくある技術的な質問に回答する目的で、このページを用意しました。

## 技術的 FAQ

### `/systemalive` エンドポイントは、AEM 6.5 LTS では使用できなくなりました。

`/systemalive` エンドポイントを提供するように設定された Felix System Ready バンドルは非推奨（廃止予定）になり、Apache Felix ヘルスチェックに置き換わりました。 このバンドルは、AEM 6.5 LTS には含まれなくなりました。

新しいヘルスチェックエンドポイントは `/system/health` で使用でき、Apache Felix ヘルスチェックを使用して実装されます。

Felix ヘルスチェックフレームワークに関する詳細なドキュメントについては、[felix documentation](https://github.com/apache/felix-dev/blob/master/healthcheck/README.md) を参照してください。

### AEM Groovy コンソールのサポート

AEM 6.5 で使用されていたAEM Groovy コンソールバージョンは、guava の依存関係がないので、AEM 6.5 LTS では機能しない可能性があります。 AEM Groovy コンソールの新しくサポートされているバージョンは [19.0.8](https://mvnrepository.com/artifact/be.orbinson.aem/aem-groovy-console/19.0.8) です。

### AEM 6.5 LTS はユーザー同期をサポートしていますか？

はい、AEM 6.5 LTS はユーザー同期をサポートしています。 AEM 6.5 と 6.5 LTS の間では、ユーザー同期の機能は変わりません。

### Maven Central の Uber JAR が破損しているように見えます。何が問題ですか？

`apis` 分類子を持つ Uber JAR を使用していることを確認します。 Uber JAR のパッケージ構造は、AEM 6.5 LTS で変更されました。 詳しくは、[AEM Uber Jar のバージョンの更新 ](/help/sites-deploying/upgrading-code-and-customizations.md#update-the-aem-uber-jar-version) を参照してください。

## 追加のヘルプを取得しています

ここで取り上げられていない問題が発生した場合は、以下の手順を実行します。
* 既知の問題については、[ リリースノート ](/help/release-notes/release-notes.md) を確認してください。
* サポートが必要な場合は、アドビサポートにお問い合わせください。
