---
title: Azure Logic Apps から Salesforce に接続する | Microsoft Docs
description: Azure Logic Apps を使用して Salesforce のレコードおよびジョブを監視、作成、および管理するタスクとワークフローを自動化する
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.topic: article
tags: connectors
ms.date: 08/24/2018
ms.openlocfilehash: 292d517f2c99974f4674a4c94472a0a320320ce4
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "62106017"
---
# <a name="monitor-create-and-manage-salesforce-resources-by-using-azure-logic-apps"></a>Azure Logic Apps を使用して Salesforce リソースを監視、作成、および管理する

Azure Logic Apps と Salesforce コネクタを使用すると、次のような、Salesforce リソース (レコード、ジョブ、オブジェクトなど) に対する自動化されたタスクやワークフローを作成することができます。

* レコードが作成または変更されるのを監視します。 
* 挿入、更新、および削除のアクションを含め、ジョブとレコードを作成、取得、および管理します。

Salesforce トリガーを使用すると、Salesforce からの応答を取得し、他のアクションで使用可能な出力を作成することができます。 ロジック アプリでアクションを使用して、Salesforce のリソースでタスクを実行することができます。 ロジック アプリを初めて使用する場合は、「[Azure Logic Apps とは](../logic-apps/logic-apps-overview.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

* Azure サブスクリプション。 Azure サブスクリプションがない場合は、<a href="https://azure.microsoft.com/free/" target="_blank">無料の Azure アカウントにサインアップ</a>してください。 

* [Salesforce アカウント](https://salesforce.com/)

* [ロジック アプリの作成方法](../logic-apps/quickstart-create-first-logic-app-workflow.md)に関する基本的な知識

* Salesforce アカウントにアクセスするためのロジック アプリ。 Salesforce トリガーで開始するには、[空のロジック アプリを作成](../logic-apps/quickstart-create-first-logic-app-workflow.md)します。 Salesforce アクションを使用するには、**Recurrence** トリガーなど、別のトリガーでロジック アプリを開始します。

## <a name="connect-to-salesforce"></a>Salesforce に接続する

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. [Azure portal](https://portal.azure.com) にサインインし、ロジック アプリ デザイナーでロジック アプリを開きます (まだ開いていない場合)。

1. 以下からパスを選択します。 

   * 空のロジック アプリの場合、検索ボックスに、フィルターとして「salesforce」と入力します。 
   トリガーの一覧で、目的のトリガーを選択します。 

     または

   * 既存のロジック アプリの場合、アクションを追加する手順で、 **[新しいステップ]** を選択します。 検索ボックスに、フィルターとして「salesforce」と入力します。 アクションの一覧で、目的のアクションを選択します。

1. Salesforce へのサインインを求めるメッセージが表示される場合は、ここでサインインしてアクセスを許可します。

   Salesforce への接続を作成してデータにアクセスしてよいという承認が、この資格情報によってロジック アプリに与えられます。

1. 選択したトリガーまたはアクションのために必要な詳細を指定し、ロジック アプリのワークフローの構築を続けます。

## <a name="connector-reference"></a>コネクタのレファレンス

コネクタの OpenAPI (以前の Swagger) の説明に記載されているトリガー、アクション、および制限に関する技術的な詳細については、コネクタの[リファレンス ページ](/connectors/salesforce/)を参照してください。

## <a name="get-support"></a>サポートを受ける

* 質問がある場合は、[Azure Logic Apps フォーラム](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps)にアクセスしてください。
* 機能のアイデアについて投稿や投票を行うには、[Logic Apps のユーザー フィードバック サイト](https://aka.ms/logicapps-wish)にアクセスしてください。

## <a name="next-steps"></a>次の手順

* 他の[Logic Apps コネクタ](../connectors/apis-list.md)を確認します。