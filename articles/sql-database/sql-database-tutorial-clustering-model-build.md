---
title: チュートリアル:R でクラスタリング モデルを作成する
titleSuffix: Azure SQL Database Machine Learning Services (preview)
description: この 3 部構成のチュートリアル シリーズのパート 2 では、Azure SQL Database Machine Learning Services (プレビュー) を使用して、R でクラスタリングを実行する K-Means モデルを作成します。
services: sql-database
ms.service: sql-database
ms.subservice: machine-learning
ms.custom: ''
ms.devlang: r
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
manager: cgronlun
ms.date: 05/17/2019
ms.openlocfilehash: 12738b63be92420c5f3afea6c133522cbd97f849
ms.sourcegitcommit: c05618a257787af6f9a2751c549c9a3634832c90
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2019
ms.locfileid: "66420230"
---
# <a name="tutorial-build-a-clustering-model-in-r-with-azure-sql-database-machine-learning-services-preview"></a>チュートリアル:Azure SQL Database Machine Learning Services (プレビュー) を使用して R でクラスタリング モデルを作成する

この 3 部構成のチュートリアル シリーズのパート 2 では、Azure SQL Database Machine Learning Services (プレビュー) を使用して、R でクラスタリングを実行する K-Means モデルを作成します。

この記事では、以下の方法について説明します。

> [!div class="checklist"]
> * K-Means アルゴリズムのクラスター数を定義する
> * クラスタリングを実行する
> * 結果を分析する

[パート 1](sql-database-tutorial-clustering-model-prepare-data.md) では、Azure SQL データベースからデータを準備して、R でクラスタリングを実行する方法を学習しました。

[パート 3](sql-database-tutorial-clustering-model-deploy.md) では、新しいデータに基づいてクラスタリングを実行するストアド プロシージャを Azure SQL データベースで作成する方法について説明します。

[!INCLUDE[ml-preview-note](../../includes/sql-database-ml-preview-note.md)]

## <a name="prerequisites"></a>前提条件

* このチュートリアルのパート 2 では、[**パート 1**](sql-database-tutorial-clustering-model-prepare-data.md) とその前提条件を完了していることを前提としています。

## <a name="define-the-number-of-clusters"></a>クラスターの数を定義する

顧客データをクラスタリングするには、**K-Means** クラスタリング アルゴリズムを使用します。これは、もっとも簡単でよく知られたデータのグループ化の方法です。
K-Means の詳細については、「[A complete guide to K-means clustering algorithm](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html)」を参照してください。

このアルゴリズムは、データそのものと、事前に定義された数値 "*k*" の 2 つの入力を受け入れます。この数値は、生成するクラスターの数を表します。
出力は、入力データがクラスター間でパーティション分割された *k* 個のクラスターです。

アルゴリズムで使用するクラスターの数を決定するには、抽出されるクラスターの数による、グループ内の平方和のプロットを使用します。 使用するクラスターの適切な数は、プロットの "エルボ" (肘のように屈曲している部分) です。

```r
# Determine number of clusters by using a plot of the within groups sum of squares,
# by number of clusters extracted. 
wss <- (nrow(customer_data) - 1) * sum(apply(customer_data, 2, var))
for (i in 2:20)
    wss[i] <- sum(kmeans(customer_data, centers = i)$withinss)
plot(1:20, wss, type = "b", xlab = "Number of Clusters", ylab = "Within groups sum of squares")
```

![エルボ グラフ](./media/sql-database-tutorial-clustering-model-build/elbow-graph.png)

グラフに基づくと、*k = 4* という値を試すのが適切であると思われます。 *k* 値により、顧客は 4 つのクラスターにグループ化されます。

## <a name="perform-clustering"></a>クラスタリングを実行する

次の R スクリプトでは、RevoScaleR パッケージの K-Means 関数である **rxKmeans** 関数を使用します。

```r
# Output table to hold the customer group mappings.
# This is a table where the cluster mappings will be saved in the database.
return_cluster = RxSqlServerData(table = "return_cluster", connectionString = connStr);
# Set the seed for the random number generator for predictability
set.seed(10);
# Generate clusters using rxKmeans and output key / cluster to a table in SQL database
# called return_cluster
clust <- rxKmeans( ~ orderRatio + itemsRatio + monetaryRatio + frequency,
                   customer_returns,
                   numClusters=4,
                   outFile=return_cluster,
                   outColName="cluster",
                   extraVarsToWrite=c("customer"),
                   overwrite=TRUE);

# Read the customer returns cluster table from the database
customer_cluster <- rxDataStep(return_cluster);
```

## <a name="analyze-the-results"></a>結果を分析する

K-Means を使用してクラスタリングを実行したので、次の手順は、結果を分析してアクションにつながる情報を得られるか確認することです。

**clust** オブジェクトには、K-Means クラスタリングの結果が含まれます。

```r
#Look at the clustering details to analyze results
clust
```

```results
Call:
rxKmeans(formula = ~orderRatio + itemsRatio + monetaryRatio + 
    frequency, data = customer_returns, outFile = return_cluster, 
    outColName = "cluster", extraVarsToWrite = c("customer"), 
    overwrite = TRUE, numClusters = 4)
Data: customer_returns
Number of valid observations: 37336
Number of missing observations: 0 
Clustering algorithm:  

K-means clustering with 4 clusters of sizes 31675, 671, 2851, 2139
Cluster means:
   orderRatio   itemsRatio monetaryRatio frequency
1 0.000000000 0.0000000000    0.00000000  0.000000
2 0.007451565 0.0000000000    0.04449653  4.271237
3 1.008067345 0.2707821817    0.49515232  1.031568
4 0.000000000 0.0004675082    0.10858272  1.186068
Within cluster sum of squares by cluster:
         1          2          3          4
    0.0000  1329.0160 18561.3157   363.2188
```

[パート 1](sql-database-tutorial-clustering-model-prepare-data.md#separate-customers) で定義した変数を使用して、4 つのクラスター方法が提供されます。

* *orderRatio* = 返品注文の割合 (注文の合計数に対する一部または全部が返品された注文の合計数)
* *itemsRatio* = 返品品目の割合 (購入された品目の数に対する返品された品目の合計数)
* *monetaryRatio* = 返品金額の割合 (購入金額に対する返品品目の合計金額)
* *frequency* = 返品の頻度

多くの場合、K-Means を使用したデータ マイニングでは、各クラスターを解釈するために結果をさらに分析し、さらなる手順を実行する必要がありますが、これにより、良いてがかりが得られる場合があります。
これらの結果を解釈する方法を次にいくつか示します。

* クラスター 1 (もっとも大きいクラスター) はアクティブでない顧客グループであると考えられます (すべての値が 0)。
* クラスター 3 は、返品に関して突出するグループであると考えられます。

## <a name="clean-up-resources"></a>リソースのクリーンアップ

***このチュートリアルを続行しない場合は***、Azure SQL Database サーバーから tpcxbb_1gb データベースを削除します。

Azure portal から次の手順を実行します。

1. Azure portal の左側のメニューから、 **[すべてのリソース]** または **[SQL データベース]** を選択します。
1. **[名前でフィルター]** フィールドに、「**tpcxbb_1gb**」と入力し、自分のサブスクリプションを選択します。
1. **tpcxbb_1gb** データベースを選択します。
1. **[概要]** ページで **[削除]** を選択します。

## <a name="next-steps"></a>次の手順

このチュートリアル シリーズのパート 2 では、これらの手順を完了しました。

* K-Means アルゴリズムのクラスター数を定義する
* クラスタリングを実行する
* 結果を分析する

作成した機械学習モデルをデプロイするには、このチュートリアル シリーズのパート 3 に従ってください。

> [!div class="nextstepaction"]
> [チュートリアル:Azure SQL Database Machine Learning Services (プレビュー) を使用して R でクラスタリング モデルをデプロイする](sql-database-tutorial-clustering-model-deploy.md)