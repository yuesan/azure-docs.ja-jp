---
title: インクルード ファイル
description: インクルード ファイル
ms.topic: include
ms.custom: include file
services: time-series-insights
ms.service: time-series-insights
author: kingdomofends
ms.author: adgera
ms.date: 07/02/2019
ms.openlocfilehash: a463e3cf475909c34054717460dc10dbba4ad8f0
ms.sourcegitcommit: 5bdd50e769a4d50ccb89e135cfd38b788ade594d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2019
ms.locfileid: "67543934"
---
> [!IMPORTANT]
> * 従来の **[Azure Active Director]**  >  **[アプリの登録 (レガシー)]** ブレードは、2019 年 5 月に新しい **[Azure Active Directory]**  >  **[アプリの登録]** ブレードに差し替えられています。
> * レガシー ブレードで作成された、またはそのブレードに表示されていたアプリの登録は、自動的に新しいブレードに表示されます。
> * 新しい Azure アプリの登録エクスペリエンスの総合的な情報については、[Azure アプリ登録トレーニング ガイド](https://docs.microsoft.com/azure/active-directory/develop/app-registrations-training-guide)と [Azure Active Directory クイックスタート](https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app)をご覧ください。

1. [Azure portal](https://ms.portal.azure.com/) で、 **[Azure Active Directory]**  >  **[アプリの登録]**  >  **[新規登録]** を選択します。

   [![Azure Active Directory での新しいアプリケーションの登録](media/time-series-insights-aad-registration/active-directory-new-application-registration.png)](media/time-series-insights-aad-registration/active-directory-new-application-registration.png#lightbox)

   > [!TIP]
   > 新しい Azure Active Directory アプリ登録パネルでは、 **[所有しているアプリケーション]** を選択することで、表示されるアプリをフィルター処理できます。

    アプリを登録すると、ここにそのアプリが表示されます。

1. アプリケーションの名前を指定し、 **[この組織のディレクトリ内のアカウントのみ]** を選択して、この API にアクセスできる **[サポートされているアカウントの種類]** を指定します。 認証されたユーザーのリダイレクト先となる有効な URI を選択し、 **[登録]** を選択します。

   [![Azure Active Directory にアプリケーションを作成する](media/time-series-insights-aad-registration/active-directory-registration.png)](media/time-series-insights-aad-registration/active-directory-registration.png#lightbox)

1. 表示されているアプリの **[概要]** ブレードに、Azure Active Directory アプリの重要な情報が表示されます。 **[所有しているアプリ]** からアプリを選択し、 **[概要]** を選択します。

   [![アプリケーション ID をコピーする](media/time-series-insights-aad-registration/active-directory-copy-application-id.png)](media/time-series-insights-aad-registration/active-directory-copy-application-id.png#lightbox)

   使用する **[アプリケーション (クライアント) ID]** を、クライアント アプリケーション内にコピーします。

1. **[認証]** ブレードで、重要な認証構成設定を指定します。 

    1. **[リダイレクト URI]** は、認証要求で指定されたアドレスと一致する必要があります。

        * ローカル開発環境でホストされているアプリでは、 **[パブリック クライアント (モバイルとデスクトップ)]** を選択します。 **[既定のクライアントの種類]** が [はい] に設定されていることを確認します。
        * Azure App Service でホストされているシングル ページ アプリでは、 **[Web]** を選択します。

    1. **[ID トークン]** をオンにすることで、暗黙的な許可フローを有効にします。

   [![新しいクライアント シークレットを生成する](media/time-series-insights-aad-registration/active-directory-auth-blade.png)](media/time-series-insights-aad-registration/active-directory-auth-blade.png#lightbox)

   **[Save]** をクリックします。

1. お使いの Azure Active Directory アプリを Azure Time Series Insights に関連付けます。 **[API のアクセス許可]**  >  **[アクセス許可の追加]**  >  **[所属する組織で使用している API]** を選択します。 

    [![API をお使いの Azure Active Directory アプリに関連付ける](media/time-series-insights-aad-registration/active-directory-app-api-permission.png)](media/time-series-insights-aad-registration/active-directory-app-api-permission.png#lightbox)

   検索バーに「`Azure Time Series Insights`」と入力した後、`Azure Time Series Insights` を選択します。

1. 次に、お使いのアプリで必要な API のアクセス許可の種類を指定します。 既定では、 **[委任されたアクセス許可]** が強調表示されます。 アクセス許可の種類を選択した後、 **[アクセス許可の追加]** を選択します。

    [![お使いのアプリで必要な API のアクセス許可の種類を指定する](media/time-series-insights-aad-registration/active-directory-app-permission-grant.png)](media/time-series-insights-aad-registration/active-directory-app-permission-grant.png#lightbox)