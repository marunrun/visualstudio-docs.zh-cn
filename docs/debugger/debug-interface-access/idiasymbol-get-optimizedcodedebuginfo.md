---
title: IDiaSymbol::get_optimizedCodeDebugInfo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_optimizedCodeDebugInfo method
ms.assetid: 57ef4170-37a9-46b0-8217-c1a674725113
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 27e2edec7964e2105cd411321a6e7644e7835097
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/12/2019
ms.locfileid: "64796442"
---
# <a name="idiasymbolgetoptimizedcodedebuginfo"></a>IDiaSymbol::get_optimizedCodeDebugInfo
检索一个标志，指示函数是否包含特定于优化的代码的调试信息。

## <a name="syntax"></a>语法

```C++
HRESULT get_optimizedCodeDebugInfo(
   BOOL *pFlag
);
```

#### <a name="parameters"></a>参数
 `pFlag`

[out]返回`TRUE`已优化的函数或标签包含调试信息; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`或错误代码。

> [!NOTE]
> 返回值为`S_FALSE`表示该属性不是可用于符号。

## <a name="requirements"></a>要求

|需求|描述|
|-----------------|-----------------|
|标头：|dia2.h|

## <a name="see-also"></a>请参阅
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)