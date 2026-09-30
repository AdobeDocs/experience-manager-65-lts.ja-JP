---
title: PreferencesNodes をプログラムで管理する
description: 環境設定マネージャーサービス API （Java）を使用して、環境設定ノードをプログラムで管理します。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
hide: true
removedfrom6.5.2025: 'yes'
exl-id: 95a83858-c0b7-4c68-b4a9-d525bfc663c0
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 2e690827bfa8f3d8227860de4efb802758ae0095
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 49%
---
# 環境設定ノードのプログラムによる管理 {#programmatically-managing-the-preferencesnodes}

**このドキュメントのサンプルと例は、JEE上のAEM Formsでのみ使用できます。**

このトピックでは、Preferences Manager Service API （Java）を使用して環境設定ノードをプログラムで管理する方法について説明します。

管理者UIから設定設定を手動で変更できます。 オプションを変更するには、`Home>Settings>User Management> Configuration>Manual Configuration` に移動してください。 変更を加えた後に `config.xml` をインポートすると、`/Adobe/Adobe Experience Manager Forms/Config/UM persist` ノードで行われた変更以外のすべての変更内容が失われます。 ユーザー管理の読み込みと書き出しのプレビューでは、他のコンポーネントの構成設定の変更はサポートされていません。 現在では、これらの変更は `PreferencesManagerServiceClient` APIを使用して行うことができます。

**手順の概要**
環境設定ノードをプログラムで管理するには、次の操作を行います。

1. プロジェクトファイルを含めます。
1. `PreferencesManagerService` クライアントを作成します。
1. 適切な役割または権限の操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。 Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**`PreferencesManagerService` クライアントを作成**

ユーザー管理`PreferencesManagerService`操作をプログラムで実行する前に、`PreferencesManagerService` クライアントを作成する必要があります。 Java APIを使用して、`PreferencesManagerServiceClient` オブジェクトを作成します。

**適切な役割または権限の操作を呼び出す**

サービスクライアントを作成したら、Preferences Manager 操作を呼び出すことができます。 サービスクライアントを使用すると、権限の読み取りと設定が可能です。
