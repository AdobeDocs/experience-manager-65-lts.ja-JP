---
title: JBoss EAP 8 （Linux）でAEM Forms 6.5 LTSでスクリプト実行が失敗する
description: Linux環境でJBoss EAP 8.0を設定すると、シェルスクリプトまたはスタートアップファイルの実行中に特定のエラーが発生する場合があります
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
exl-id: 4dfaa625-47fa-4681-9e2f-a3bbdca95276
source-git-commit: 96fe29ceae4c38238ccc40d456f2ad8e276788c7
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 1%

---

# JBoss EAP 8 （Linux）でAEM Forms 6.5 LTSでスクリプト実行が失敗する

## 問題

**Linux**&#x200B;環境で&#x200B;**JBoss EAP 8.0 （AEM Forms 6.5.1 LTS）**&#x200B;を設定する際に、シェルスクリプトまたはスタートアップファイルの実行中に次のいずれかのエラーが発生する場合があります。

```text
/bin/sh^M: bad interpreter
$'\r': command not found
```

これらのエラーは、**Windows** システムでシェルスクリプトまたは設定ファイルが作成または編集され、**CRLF （キャリッジ リターン + ライン フィード）**行の末尾が含まれている場合に発生します。
Linux システムは**LF （Line Feed）**&#x200B;行の末尾のみをサポートし、Windows スタイルの行の末尾はスクリプト実行エラーの原因となります。

## 適用先

* **JBoss EAP 8.0**
* **Linux / UNIX ベースのオペレーティング システム**

## トラブルシューティング手順

1. **影響を受けるファイルを特定**

   * エラー出力を確認して、エラーの原因となる`.sh` スクリプトまたは構成ファイルを特定します。

2. **ファイルをUnix形式に変換**

   * `dos2unix` ユーティリティを使用して、Windows形式の行末をUnix形式に変換します。

     ```bash
     dos2unix <file_name>
     ```

   * エラーをスローしている実際のスクリプトまたは設定ファイルに`<file_name>`を置き換えます。

3. **必要に応じて繰り返す**

   * 複数のスクリプトが影響を受ける場合は、関連するすべての`.sh` ファイル（インストーラー、LCM、JBoss起動スクリプトなど）に対して変換を繰り返します。

4. **スクリプトを再実行**

   * 変換後、スクリプトを再実行して、問題が解決されたことを確認します。

ファイルをUnix （LF）行の末尾に変換すると、`/bin/sh^M`と`$'\r': command not found`のエラーが解決され、LinuxでJBoss スクリプトが正常に実行されます。
