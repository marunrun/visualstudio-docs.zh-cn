---
title: IDiaSectionContrib::get_initializedData | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_initializedData method
ms.assetid: f5c108be-a0cc-408b-9590-b8d44361810c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ef878dcae9f8d6d29761bcda5f5aa9588f26d66c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828168"
---
# <a name="idiasectioncontribgetinitializeddata"></a>IDiaSectionContrib::get_initializedData
检索一个标志，指示的部分是否包含初始化的数据。

## <a name="syntax"></a>语法

```C++
HRESULT get_initializedData ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`的部分包含初始化的数据; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)