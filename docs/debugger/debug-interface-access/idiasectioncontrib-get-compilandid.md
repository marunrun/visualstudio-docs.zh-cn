---
title: IDiaSectionContrib::get_compilandId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_compilandId method
ms.assetid: 71ef2e63-d095-42b6-88d8-626e3129f0d9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b66740fc4c767dca3539d4a2889d82b485902603
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742701"
---
# <a name="idiasectioncontribget_compilandid"></a>IDiaSectionContrib::get_compilandId
检索部分的编译单位标识符。

## <a name="syntax"></a>语法

```C++
HRESULT get_compilandId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回部分的编译单位标识符。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果此属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)