---
title: Azure Monitor ログ クエリ言語の違い | Microsoft Docs
description: Azure Monitor で使用される Kusto クエリ言語のリファレンス情報。 Azure Monitor に固有の追加要素と、Azure Monitor ログ クエリでサポートされていない要素が含まれています。
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 10/31/2018
ms.author: bwren
ms.openlocfilehash: 1185f3f96fd39f168d138d7dbf66e7780884b1fa
ms.sourcegitcommit: 41ca82b5f95d2e07b0c7f9025b912daf0ab21909
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "60589271"
---
# <a name="azure-monitor-log-query-language-differences"></a>Azure Monitor ログ クエリ言語の違い

[Azure Monitor のログ](log-query-overview.md)は、[Azure Data Explorer](/azure/data-explorer) に基づいて構築されていて、同じ [Kusto クエリ言語](/azure/kusto/query)が使用されますが、言語のバージョンによっていくつかの違いがあります。 この記事では、Data Explorer で使用されるバージョンの言語と、Azure Monitor ログ クエリで使用されるバージョンの間で異なっている要素を明らかにします。

[!INCLUDE [azure-monitor-log-analytics-rebrand](../../../includes/azure-monitor-log-analytics-rebrand.md)]

## <a name="kql-elements-not-supported-in-azure-monitor"></a>Azure Monitor でサポートされていない KQL 要素
以降のセクションでは、Azure Monitor でサポートされていない Kusto クエリ言語の要素について説明します。

### <a name="statements-not-supported-in-azure-monitor"></a>Azure Monitor でサポートされていないステートメント

* [エイリアス](/azure/kusto/query/aliasstatement)
* [クエリ パラメーター](/azure/kusto/query/queryparametersstatement)

### <a name="functions-not-supported-in-azure-monitor"></a>Azure Monitor でサポートされていない関数

* [cluster()](/azure/kusto/query/clusterfunction)
* [cursor_after()](/azure/kusto/query/cursorafterfunction)
* [cursor_before_or_at()](/azure/kusto/query/cursorbeforeoratfunction)
* [cursor_current(), current_cursor()](/azure/kusto/query/cursorcurrent)
* [database()](/azure/kusto/query/databasefunction)
* [current_principal()](/azure/kusto/query/current-principalfunction)
* [extent_id()](/azure/kusto/query/extentidfunction)
* [extent_tags()](/azure/kusto/query/extenttagsfunction)

### <a name="operators-not-supported-in-azure-monitor"></a>Azure Monitor でサポートされていない演算子

* [クラスター間の結合](/azure/kusto/query/joincrosscluster)
* [externaldata 演算子](/azure/kusto/query/externaldata-operator)

### <a name="plugins-not-supported-in-azure-monitor"></a>Azure Monitor でサポートされていないプラグイン

* [sql_request プラグイン](/azure/kusto/query/sqlrequestplugin)


## <a name="additional-operators-in-azure-monitor"></a>Azure Monitor で追加されている演算子
以下の演算子は、Azure Monitor の特定の機能をサポートしており、Azure Monitor の外部では使用できません。

* [app()](app-expression.md)
* [workspace()](workspace-expression.md)

## <a name="next-steps"></a>次の手順

- [Azure Monitor ログ クエリを記述するための、さまざまなリソース](query-language.md)への参照を取得します。
- 完全な [Kusto クエリ言語のリファレンス ドキュメント](/azure/kusto/query/)にアクセスします。
