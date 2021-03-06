---
author: erhopf
ms.service: cognitive-services
ms.topic: include
ms.date: 2/20/2019
ms.author: erhopf
ms.openlocfilehash: faa93b75bde3a14e48baa7d27a3eb6439a137e44
ms.sourcegitcommit: cababb51721f6ab6b61dda6d18345514f074fb2e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66482394"
---
1. Visual Studio 2019 を起動します。

1. **ユニバーサル Windows プラットフォーム開発**ワークロードが使用できることを確認してください。 Visual Studio のメニュー バーから **[ツール]**  >  **[Get Tools and Features]\(ツールと機能の入手\)** を選択し、Visual Studio インストーラーを開きます。 このワークロードが既に有効になっている場合は、ダイアログ ボックスを閉じます。

    ![[ワークロード] タブを強調表示した Visual Studio インストーラーのスクリーンショット](../articles/cognitive-services/Speech-Service/media/sdk/vs-enable-uwp-workload.png)

    それ以外の場合、 **[.NET cross-platform development] (.NET クロス プラットフォーム開発)** の横にあるボックスを選択し、ダイアログ ボックスの右下隅にある **[変更]** を選択します。 新しい機能のインストールにはしばらく時間がかかります。

1. 空の Visual C# ユニバーサル Windows アプリを作成します。 最初に、メニューから **[ファイル]**  >  **[新規]**  >  **[プロジェクト]** を選択します。 **[新しいプロジェクト]** ダイアログ ボックスで、左側のウィンドウから **[インストール済み]**  >  **[Visual C#]**  >  **[Windows ユニバーサル]** を展開します。 次に、 **[空白のアプリ (ユニバーサル Windows)]** を選択します。 プロジェクト名として「*helloworld*」と入力します。

    ![[新しいプロジェクト] ダイアログ ボックスのスクリーンショット](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-01-new-blank-app.png)

1. Speech SDK では、Windows 10 Fall Creators Update 以降向けにアプリケーションをビルドすることが必要です。 ポップアップ表示される **[新しいユニバーサル Windows プラットフォーム プロジェクト]** ウィンドウで、 **[最小バージョン]** に **[Windows 10 Fall Creators Update (10.0; Build 16299)]** を選択します。 **[ターゲット バージョン]** ボックスで、このバージョンまたはこれ以降のバージョンを選択して、 **[OK]** をクリックします。

    ![[新しいユニバーサル Windows プラットフォーム プロジェクト] ウィンドウのスクリーンショット](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-02-new-uwp-project.png)

1. 64 ビットの Windows を実行している場合は、Visual Studio ツールバーのドロップダウン メニューを使用して、ビルド プラットフォームを `x64` に切り替えることができます。 (64 ビットの Windows は 32 ビットのアプリケーションを実行できるため、`x86` に設定しておいてもかまいません。)

   ![x64 が強調表示されている Visual Studio のツールバーのスクリーン ショット](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-03-switch-to-x64.png)

   > [!NOTE]
   > Speech SDK では、Intel 互換プロセッサのみがサポートされています。 ARM は現在サポートされていません。

1. [Speech SDK NuGet パッケージ](https://aka.ms/csspeech/nuget)をインストールして参照します。 ソリューション エクスプローラーで、ソリューションを右クリックし、 **[ソリューションの NuGet パッケージの管理]** を選択します。

    ![[ソリューションの NuGet パッケージの管理] オプションが強調表示されたソリューション エクスプローラーのスクリーン ショット](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-04-manage-nuget-packages.png)

1. 右上隅の **[パッケージ ソース]** フィールドで、 **[nuget.org]** を選択します。`Microsoft.CognitiveServices.Speech` パッケージを検索して、**helloworld** プロジェクトにインストールします。

    ![[ソリューションの NuGet パッケージの管理] ダイアログ ボックスのスクリーンショット](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-05-nuget-install-1.0.0.png "NuGet パッケージのインストール")

1. 表示されるライセンスに同意し、NuGet パッケージのインストールを開始します。

    ![[ライセンスの同意] ダイアログ ボックスのスクリーンショット](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-06-nuget-license.png "ライセンスへの同意")

1. パッケージ マネージャー コンソールに次の出力行が表示されます。

   ```text
   Successfully installed 'Microsoft.CognitiveServices.Speech 1.5.0' to helloworld
   ```

1. アプリケーションでは音声入力にマイクを使用するため、 **[マイク]** 機能をプロジェクトに追加します。 ソリューション エクスプローラーで **Package.appxmanifest** をダブルクリックして、アプリケーション マニフェストを編集します。 次に、 **[機能]** タブに切り替え、 **[マイク]** 機能の ボックスをオンにして、変更を保存します。

   ![機能とマイクを強調表示した Visual Studio のアプリケーション マニフェストのスクリーン ショット](../articles/cognitive-services/Speech-Service/media/sdk/qs-csharp-uwp-07-capabilities.png)
