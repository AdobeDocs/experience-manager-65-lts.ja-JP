---
title: 実稼動準備モードでの AEM の実行
description: 実稼動準備モードで AEM を実行する方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
exl-id: 99724bd6-41b4-4491-9958-1f5d9e1f5050
source-git-commit: c3e9029236734e22f5d266ac26b923eafbe0a459
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 100%

---

# 実稼動準備モードでの AEM の実行{#running-aem-in-production-ready-mode}

AEM 6.1 では、アドビは実稼動環境においてデプロイメント用の AEM インスタンスの準備に必要な手順の自動化を目的とした、新しい `"nosamplecontent"` 実行モードを導入します。

この新しい実行モードは、セキュリティチェックリストに記載されるセキュリティのベストプラクティスに従うようにインスタンスを自動的に設定するだけでなく、サンプルの Geometrixx アプリケーションと設定をプロセスですべて削除します。

>[!NOTE]
>
>実用的な理由から、AEM の実稼動準備モードは、インスタンスの保護に必要な多くのタスクにのみ対応しているので、実稼動環境で運用を開始する前に[セキュリティチェックリスト](/help/sites-administering/security-checklist.md)を確認しておくことを強くお勧めします。
>
>また、AEM を実稼動準備モードを実行すると CRXDE Lite へのアクセスが無効になります。デバッグのためにアクセスする必要がある場合は、[AEM での CRXDE Lite の有効化](/help/sites-administering/enabling-crxde-lite.md)を参照してください。

![chlimage_1-83](assets/chlimage_1-83a.png)

実稼動準備モードで AEM を実行するには、`-r` 実行モードスイッチ経由で `nosamplecontent` を既存の起動引数に追加する必要があります。

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

例えば次に示すように、実稼動準備を使用して、MongoDB 永続性を備えたオーサーインスタンスを起動できます。

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## 実稼動準備モードの変更点 {#changes-part-of-the-production-ready-mode}

具体的には、AEM を実稼動準備モードで実行すると、次の設定が変更されます。

1. 実稼動準備モードでは、**CRXDE サポートバンドル**（`com.adobe.granite.crxde-support`）がデフォルトで無効になります。このバンドルは、アドビの Maven 公開リポジトリからいつでもインストールできます。AEM 6.1 には、バージョンは 3.0.0 が必要です。

1. **Apache Sling Simple WebDAV Access To Repositories**（`org.apache.sling.jcr.webdav`）バンドルは&#x200B;**オーサー**&#x200B;インスタンスでのみ使用できます。

1. 新しく作成されたユーザーは、初回ログイン時にパスワードを変更する必要があります。これは、管理者ユーザーには適用されません。
1. **Apache Java Script Handler** では、**デバッグ情報を生成**&#x200B;が無効になります。

1. **Apache Sling JSP Script Handler** では、「**Mapped Content**」と「**Generate Debug Info**」が無効になります。

1. **Day CQ WCM Filter** は、**オーサー**&#x200B;インスタンスでは `edit` に設定され、**パブリッシュ**&#x200B;インスタンスでは `disabled` に設定されます。

1. **Adobe Granite HTML ライブラリマネージャー**&#x200B;は次のように設定されます。

   1. **Minify：** `enabled`
   1. **デバッグ：** `disabled`
   1. **Gzip：** `enabled`
   1. **タイミング：** `disabled`

1. **Apache Sling GET Servlet** は、次に示すセキュアな設定をサポートするようにデフォルトで設定されます。

| **設定** | **作成者** | **公開** |
|---|---|---|
| TXT レンディション | 無効 | 無効 |
| HTML レンディション | 無効 | 無効 |
| JSON レンディション | enabled | enabled |
| XML レンディション | 無効 | 無効 |
| json.maximumresults | 1000 | 100 |
| 自動インデックス | 無効 | 無効 |
