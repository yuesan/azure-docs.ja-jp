---
title: Azure Key Vault セキュリティ ワールド | Microsoft Docs
ms.service: key-vault
ms.topic: conceptual
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 07/03/2017
ms.openlocfilehash: d75ce953f73912428ee88fe2e19a138799f979fa
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "64704707"
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a>Azure Key Vault セキュリティ ワールドと地理的境界

Azure Key Vault はマルチ テナント サービスであり、Azure の場所それぞれでハードウェア セキュリティ モジュール (HSM) のプールが使用されています。 

地理的に同じリージョンに属する Azure の場所にある HSM はすべて、同じ暗号化境界 (Thales セキュリティ ワールド) を共有しています。 たとえば、米国 geo ロケーションに属する米国東部と米国西部は、同じセキュリティ ワールドを使用します。 また、日本でもすべての Azure の場所が同じセキュリティ ワールドを共有しています。オーストラリア、インドなどの Azure の場所も同様です。 

## <a name="backup-and-restore-behavior"></a>バックアップと復元動作

1 つの Azure の場所のキー コンテナーから取得したキーのバックアップは、次の両方の条件を満たしていれば、別の Azure の場所のキー コンテナーに復元できます。

- Azure の場所の両方が同じ地理的な場所に属している
- キー コンテナーの両方が同じ Azure サブスクリプションに属している

たとえば、インド西部にあるキー コンテナーで、指定したキーのサブスクリプションによって取得されたバックアップは、同じサブスクリプションおよび geo ロケーション、つまりインド西部、インド中部、またはインド南部にある別のキー コンテナーにのみ復元できます。

## <a name="regions-and-products"></a>リージョンと製品

- [Azure リージョン](https://azure.microsoft.com/regions/)
- [リージョン別の Microsoft 製品](https://azure.microsoft.com/regions/services/)

リージョンは、表の大見出しとして表示されている、セキュリティ ワールドにマップされます。

リージョン別の製品の記事では、たとえば **[米国]** タブには米国東部、米国中部、米国西部が含まれ、すべて米国リージョンにマップしています。 

>[!NOTE]
>例外として、米国防総省東部と米国防総省中部には、独自のセキュリティ ワールドがあります。 

同様に、 **[ヨーロッパ]** タブでは、北ヨーロッパと西ヨーロッパの両方がヨーロッパ リージョンにマップしています。 **[アジア太平洋]** タブも同様です。



