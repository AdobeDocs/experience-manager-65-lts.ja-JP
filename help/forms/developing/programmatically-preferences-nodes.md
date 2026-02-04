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
hidefromtoc: true
exl-id: 95a83858-c0b7-4c68-b4a9-d525bfc663c0
source-git-commit: 51342861dd01e659999c19fbe0274e8d3cbcf8c4
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 49%

---

# 環境設定ノードをプログラムで管理する {#programmatically-managing-the-preferencesnodes}

**このドキュメントのサンプルと例は、JEE 環境のAEM Formsのみを対象としています**。

このトピックでは、Preferences Manager Service API （Java）を使用して、環境設定ノードをプログラムで管理する方法について説明します。

構成設定は、管理者 UI から手動で変更できます。 オプションを変更するには、`Home>Settings>User Management> Configuration>Manual Configuration` に移動してください。変更を加えた後に `config.xml` をインポートすると、`/Adobe/Adobe Experience Manager Forms/Config/UM persist` ノードで行われた変更以外のすべての変更内容が失われます。User Management のインポートとエクスポートのプレビューでは、他のコンポーネントの構成設定の変更はサポートされていません。 現在では、これらの変更は `PreferencesManagerServiceClient` APIを使用して行うことができます。

**手順の概要**
環境設定ノードをプログラムで管理するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. `PreferencesManagerService` クライアントを作成します。
1. 適切な役割または権限の操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**`PreferencesManagerService` クライアントの作成**

User Management `PreferencesManagerService` 操作をプログラムで実行する前に、`PreferencesManagerService` クライアントを作成する必要があります。 Java API を使用して、`PreferencesManagerServiceClient` オブジェクトを作成します。

**適切な役割または権限の操作を呼び出す**

サービスクライアントを作成したら、Preferences Manager 操作を呼び出すことができます。サービスクライアントを使用すると、権限の読み取りと設定が可能です。
