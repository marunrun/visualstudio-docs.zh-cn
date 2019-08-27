---
title: IDiaSectionContrib::get_informational | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSectionContrib::get_informational method
ms.assetid: 5351e89f-7db1-4f8e-9e57-2dd1c74002e0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b00d07b788fe07fbe2e879f01a98929927743a0b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839584"
---
# <a name="idiasectioncontribgetinformational"></a>IDiaSectionContrib::get_informational
检索一个标志，指示一个部分包含注释或类似的信息。

## <a name="syntax"></a>语法

```C++
HRESULT get_informational(
   BOOL* pRetVal
};
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`的部分包含注释或其他信息; 否则返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果此属性不受支持。 否则，返回错误代码。

## <a name="remarks"></a>备注
 通常.directive 部分包含的信息。

## <a name="see-also"></a>请参阅
- [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)