---
title: Visual Studio を使用して Azure で初めての関数を作成する
description: Visual Studio を使用し、HTTP によってトリガーされる Azure 関数を作成して発行します。
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: Azure Functions, 関数, イベント処理, コンピューティング, サーバーなしのアーキテクチャ
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: azure-functions
ms.devlang: multiple
ms.topic: quickstart
ms.date: 10/17/2018
ms.author: glenga
ms.custom: mvc, devcenter, vs-azure, 23113853-34f2-4f
ms.openlocfilehash: 1c07da0121b8e350c55b139901d56cfe2133386d
ms.sourcegitcommit: 4c2b9bc9cc704652cc77f33a870c4ec2d0579451
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65864494"
---
# <a name="create-your-first-function-using-visual-studio"></a>Visual Studio を使用して初めての関数を作成する

Azure Functions を使用すると、最初に VM を作成したり Web アプリケーションを発行したりしなくても、[サーバーレス](https://azure.microsoft.com/solutions/serverless/)環境でコードを実行できます。

この記事では、Visual Studio 2019 Tools for Azure Functions を使用して、"hello world" 関数をローカルで作成およびテストする方法を学習します。 その後、関数コードを Azure に発行します。 これらのツールは、Visual Studio 2019 の Azure の開発ワークロードの一部として使用できます。

![ブラウザーでの関数 localhost の応答](./media/functions-create-your-first-function-visual-studio/functions-create-your-first-function-visual-studio-browser-local-final.png)

このトピックには、同じ基本的な手順を示す[動画](#watch-the-video)が含まれています。

## <a name="prerequisites"></a>前提条件

このチュートリアルを完了するには、以下が必要です。

* [Visual Studio 2019](https://azure.microsoft.com/downloads/) をインストールし、 **[Azure の開発]** ワークロードもインストールされていることを確認します。

* [最新の Azure Functions ツール](functions-develop-vs.md#check-your-tools-version)があることを確認します。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-function-app-project"></a>関数アプリ プロジェクトを作成する

[!INCLUDE [Create a project using the Azure Functions template](../../includes/functions-vstools-create.md)]

Visual Studio によってプロジェクトが作成されます。その中には、選択した関数の種類のスケルトン コードが含まれているクラスがあります。 メソッドの **FunctionName** 属性は、関数の名前を設定します。 **HttpTrigger** 属性は、関数が HTTP 要求によってトリガーされることを指定します。 スケルトン コードは、要求本文またはクエリ文字列の値を含む HTTP 応答を送信します。 メソッドに適切な属性を適用することによって、関数に入力および出力バインディングを追加することができます。 詳細については、[Azure Functions C# 開発者向けリファレンス](functions-dotnet-class-library.md)の「[トリガーとバインド](functions-dotnet-class-library.md#triggers-and-bindings)」のセクションを参照してください。

関数プロジェクトと、HTTP によってトリガーされる関数を作成できたので、この関数をローカル コンピューターでテストすることができます。

## <a name="test-the-function-locally"></a>関数をローカルでテストする

Azure Functions Core Tools を使用すると、ローカルの開発用コンピューター上で Azure Functions プロジェクトを実行できます。 Visual Studio から初めて関数を開始すると、これらのツールをインストールするよう求めるメッセージが表示されます。

1. 関数をテストするには、F5 キーを押します。 メッセージが表示されたら、Visual Studio からの要求に同意し、Azure Functions Core (CLI) ツールをダウンロードしてインストールします。 また、ツールで HTTP 要求を処理できるようにファイアウォールの例外を有効にすることが必要になる場合もあります。

2. Azure Functions のランタイムの出力から、関数の URL をコピーします。

    ![Azure ローカル ランタイム](./media/functions-create-your-first-function-visual-studio/functions-create-your-first-function-visual-studio-debugging.png)

3. HTTP 要求の URL をブラウザーのアドレス バーに貼り付けます。 この URL にクエリ文字列 `?name=<YOUR_NAME>` を追加して、要求を実行します。 関数によって返されたローカルの GET 要求に対するブラウザーでの応答を次に示します。 

    ![ブラウザーでの関数 localhost の応答](./media/functions-create-your-first-function-visual-studio/functions-create-your-first-function-visual-studio-browser-local.png)

4. デバッグを停止するには、**Shift キーを押しながら F5 キー**を押します。

関数がローカル コンピューター上で正常に動作することを確認した後、プロジェクトを Azure に発行します。

## <a name="publish-the-project-to-azure"></a>Azure にプロジェクトを発行する

プロジェクトを発行するには、Azure サブスクリプションに関数アプリがあることが必要です。 関数アプリは、Visual Studio から直接作成できます。

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a>Azure で関数をテストする

1. [発行プロファイル] ページから関数アプリのベース URL をコピーします。 関数をローカルでテストしたときに使用した URL の `localhost:port` 部分を新しいベース URL に置き換えます。 前と同様に、この URL にクエリ文字列 `?name=<YOUR_NAME>` を追加してから、要求を実行します。

    HTTP によってトリガーされる関数を呼び出す URL は、次の形式である必要があります。

        http://<APP_NAME>.azurewebsites.net/api/<FUNCTION_NAME>?name=<YOUR_NAME> 

2. HTTP 要求のこの新しい URL をブラウザーのアドレス バーに貼り付けます。 関数によって返されたリモート GET 要求に対するブラウザーでの応答を次に示します。

    ![ブラウザーでの関数の応答](./media/functions-create-your-first-function-visual-studio/functions-create-your-first-function-visual-studio-browser-azure.png)

## <a name="watch-the-video"></a>ビデオを見る

> [!VIDEO https://www.youtube-nocookie.com/embed/DrhG-Rdm80k]

## <a name="next-steps"></a>次の手順

Visual Studio を使用して、HTTP によってトリガーされる単純な関数を含む C# 関数アプリを作成して発行しました。

* [他のサービスと統合する入力および出力バインドを追加する方法を学習します。](functions-develop-vs.md#add-bindings)
* [.NET クラス ライブラリとして関数を開発する詳細を学習します](functions-dotnet-class-library.md)。
