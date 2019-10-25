---
title: IDiaSymbol：： get_lowerBoundId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_lowerBoundId method
ms.assetid: 12ce98e9-a225-4947-88c9-5fda39dd67e4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8d3685512521d5fc919f4c9b1752a039ae1085bc
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739827"
---
# <a name="idiasymbolget_lowerboundid"></a>IDiaSymbol::get_lowerBoundId
检索 FORTRAN 数组维度下限的符号标识符。

## <a name="syntax"></a>语法

```C++
HRESULT get_lowerBoundId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回表示 FORTRAN 数组维度下限的符号的符号 ID。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 标识符是由 DIA SDK 创建的唯一值，用于将所有符号标记为唯一。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)