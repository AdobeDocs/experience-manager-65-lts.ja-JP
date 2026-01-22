---
title: JBoss EAP 8 を使用したAEM Forms 6.5 LTS でスクリプトが実行できない（Linux）
description: linux 環境で JBoss EAP 8.0 （AEM Forms 6.5.1 LTS）を設定すると、シェルスクリプトまたはスタートアップファイルの実行中に特定のエラーが発生する場合があります
solution: Experience Manager
feature: Deploying
role: User,Admin,Developer
hide: true
index: false
hidefromtoc: true
source-git-commit: 5d020671efaa4527a5f6dbb4b779c7a3351888a4
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 1%

---


# JBoss EAP 8 を使用したAEM Forms 6.5 LTS でスクリプトが実行できない（Linux）

## 問題

**Linux** 環境で **JBoss EAP 8.0 （AEM Forms 6.5.1 LTS）を設定する場合** シェルスクリプトまたは起動ファイルの実行中に次のいずれかのエラーが発生することがあります。

```text
/bin/sh^M: bad interpreter
$'\r': command not found
```

これらのエラーは、シェルスクリプトまたは設定ファイルが **Windows** システム上で作成または編集され、**CRLF （キャリッジリターン + ラインフィード）** 行末が含まれている場合に発生します。
Linux システムは **LF （ラインフィード）** 行末のみをサポートしており、Windows スタイルの行末はスクリプトの実行エラーの原因となります。

## 適用先

* **JBoss EAP 8.0**
* **Linux/UNIX ベースのオペレーティングシステム**

## トラブルシューティング手順

1. **影響を受けるファイルを特定**

   * エラー出力を確認して、エラーの原因となっている `.sh` スクリプトまたは構成ファイルを特定します。

2. **ファイルを UNIX 形式に変換**

   * `dos2unix` ユーティリティを使用して、Windows スタイルの行末を Unix 形式に変換します。

     ```bash
     dos2unix <file_name>
     ```

   * `<file_name>` を、エラーをスローする実際のスクリプトまたは設定ファイルに置き換えます。

3. **必要に応じて繰り返す**

   * 複数のスクリプトが影響を受ける場合は、関連するすべての `.sh` ファイル（インストーラー、LCM、JBoss スタートアップスクリプトなど）に対して変換を繰り返します。

4. **スクリプトを再実行します**。

   * 変換後、スクリプトを再実行して、問題が解決されたことを確認します。

ファイルを Unix （LF）行末に変換した後、`/bin/sh^M` および `$'\r': command not found` エラーが解決され、JBoss スクリプトが Linux で正常に実行されます。
