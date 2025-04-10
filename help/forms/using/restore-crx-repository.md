---
title: JEE クラスターサーバーに適用可能な破損した CRX リポジトリを復元できません
description: 破損している CRX リポジトリを復元する方法について説明します。
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
hide: true
hidefromtoc: true
exl-id: 716d8eb2-2010-4d55-b8fe-bd4f6f256a4d
source-git-commit: bc91f56d447d1f2c26c160f5c414fd0e6054f84c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 100%

---

# 破損した CRX リポジトリを復元できません {#unable-to-restore-corrupt-crx-repository}

## 問題 {#issue}

リレーショナルデータベースを使用する JEE 上の AEM Forms の場合、AEM Forms とリレーショナルデータベースをホストするマシンでの時間は常に絶対同期にする必要があります。 これらのマシンの時間が同期しなくなった場合、JEE 上の AEM Forms サーバーの CRX リポジトリにアクセスできなくなる可能性があります。 破損しているように見え、URL 経由でアクセスできなくなる場合があります。この `AuthenticationsupportService missing` エラーが記録されます。

## 前提条件 {#prerequisites}

以下の手順を実行する前に、CRX リポジトリのバックアップを取ります。

## 解決策 {#solution}

1. `https://[AEM Forms Server]:[port]/system/console/bundles` にアクセスします。

1. `oak-core` バンドルを見つけて、実行中かどうかを確認します。

1. 実行されていない場合は、`oak-core` バンドルを再起動します。![「一時停止」ボタン](/help/forms/using/assets/stop.png)アイコンが `oak-core` バンドルの前にある場合、バンドルが実行状態であることを示しています。

1. それでも問題が解決されない場合は、バックアップの CRX リポジトリから復元するか、バックアップが使用できない場合は CRX リポジトリを再構築します。


## 適用先 {#applies-to}

このソリューションは、JEE 上の AEM Forms クラスターに適用されます。
