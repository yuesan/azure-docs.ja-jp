---
title: Academic Knowledge API の所属エンティティの属性
titlesuffix: Azure Cognitive Services
description: Academic Knowledge API で所属エンティティに使用できる属性について説明します。
services: cognitive-services
author: alch-msft
manager: nitinme
ms.service: cognitive-services
ms.subservice: academic-knowledge
ms.topic: conceptual
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: 82e6a5b66342e58e62da029d617cbd1d74c28149
ms.sourcegitcommit: d4dfbc34a1f03488e1b7bc5e711a11b72c717ada
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "61340521"
---
# <a name="affiliation-entity"></a>所属エンティティ

<sub> *次の属性は、所属エンティティに固有です。(Ty = '5') </sub>

Name    |説明                            |Type       | Operations
------- | ------------------------------------- | --------- | ----------------------------
Id      |エンティティ ID                              |Int64      |等しい
AfN     |所属の標準化名        |string     |等しい
DAfN    |所属の表示名       |string     |なし
CC      |所属の引用の総数           |Int32      |なし  
ECC     |所属の引用の推定総数 |Int32      |なし

## <a name="extended-metadata-attributes"></a>拡張メタデータの属性 ##

Name    | 説明               
--------|---------------------------    
PC      |所属の論文数
