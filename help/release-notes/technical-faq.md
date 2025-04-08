---
title: 技術的なよくある質問（FAQ）
description: AEM 6.5 LTS に関する技術的な FAQ
solution: Experience Manager
feature: Release Information
role: User,Admin,Architect,Developer
source-git-commit: 2352420843c613884ad3cae487ed048bd775e294
workflow-type: tm+mt
source-wordcount: '171'
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

## 追加のヘルプを取得しています

ここで取り上げられていない問題が発生した場合は、以下の手順を実行します。
* 既知の問題については、[ リリースノート ](/help/release-notes/release-notes.md) を確認してください。
* サポートが必要な場合は、アドビサポートにお問い合わせください。
