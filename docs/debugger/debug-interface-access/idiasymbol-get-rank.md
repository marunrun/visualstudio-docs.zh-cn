---
title: IDiaSymbol：： get_rank |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_rank method
ms.assetid: 14cc9c4b-a5ec-414a-b01f-4a142c17b7cc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c5cff86464a4034ad869cdfe231a88ad128dbf52
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72739488"
---
# <a name="idiasymbolget_rank"></a>IDiaSymbol::get_rank
检索 FORTRAN 多维数组的秩（维数）。

## <a name="syntax"></a>语法

```C++
HRESULT get_rank ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回 FORTRAN 多维数组中的维度数。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回 `S_FALSE` 或错误代码。

> [!NOTE]
> @No__t_0 的返回值意味着该属性对符号不可用。

## <a name="remarks"></a>备注
 Rank 是指数组中数组的维数，其中数组被声明为 `myarray[1,2,3]`。 此示例的排名为3和3。 Rank 不适用于C++使用每个维度的数组（即 `myarray[1][2][3]`）的概念。

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)