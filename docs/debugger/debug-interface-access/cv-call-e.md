---
title: CV_call_e | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- CV_call_e enumeration
ms.assetid: f230560b-4243-432d-8f19-46df112043b9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5deb59d4bbee06e505ba10bf1d4f08b1b06aa62d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745355"
---
# <a name="cv_call_e"></a>CV_call_e
指定函数的调用约定。

> [!NOTE]
> 此处仅介绍最常见的枚举值。 Cvconst 头文件中提供了完整的枚举。

## <a name="syntax"></a>语法

```C++
typedef enum CV_call_e {
    CV_CALL_NEAR_C    = 0x00,
    CV_CALL_NEAR_FAST = 0x04,
    CV_CALL_NEAR_STD  = 0x07,
    CV_CALL_NEAR_SYS  = 0x09,
    CV_CALL_THISCALL  = 0x0b,
    CV_CALL_CLRCALL   = 0x16
} CV_call_e;
```

## <a name="elements"></a>元素
CV_CALL_NEAR_C 使用接近的右到左推送指定函数调用约定。 调用函数清除堆栈。

CV_CALL_NEAR_FAST 指定函数调用约定，使用接近于寄存器的近乎左到右推送。 被调用的函数使用参数字节的和来清除堆栈。

CV_CALL_NEAR_STD 使用接近标准调用（从右到左推送）指定函数调用约定。

CV_CALL_NEAR_SYS 使用近系统调用指定函数调用约定。

CV_CALL_THISCALL 使用 `this` 调用（传入 register `this` 指针）指定函数调用约定。

CV_CALL_CLRCALL 指定公共语言运行时（CLR）使用的函数调用约定（也称为托管代码调用约定）。

## <a name="remarks"></a>备注
此枚举中的值由对[IDiaSymbol：： get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)方法的调用返回。

## <a name="requirements"></a>要求
标头： cvconst

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)
