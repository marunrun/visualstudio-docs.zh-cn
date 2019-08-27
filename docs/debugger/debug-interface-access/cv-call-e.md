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
ms.openlocfilehash: ec5fea99994b891250dad85cfc43320848df98f9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62555099"
---
# <a name="cvcalle"></a>CV_call_e
指定的函数的调用约定。

> [!NOTE]
> 此处介绍了仅是最常见的枚举值。 完整的枚举是 cvconst.h 标头文件中。

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
CV_CALL_NEAR_C 指定使用近右到左推送的函数调用约定。 调用函数清除堆栈。

CV_CALL_NEAR_FAST 指定函数调用约定使用几乎从左到右请求与注册。 被调用的函数使用参数的字节数之和来清除堆栈。

CV_CALL_NEAR_STD 指定使用近乎标准调用 （从右到左推送） 的函数调用约定。

CV_CALL_NEAR_SYS 指定调用使用接近系统函数调用约定。

函数调用约定使用指定 CV_CALL_THISCALL`this`调用 (`this`在寄存器中传递的指针)。

CV_CALL_CLRCALL 指定使用由公共语言运行时 (CLR) （也称为托管代码调用约定） 的函数调用约定。

## <a name="remarks"></a>备注
此枚举中的值返回通过调用[idiasymbol:: Get_callingconvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)方法。

## <a name="requirements"></a>要求
标头： cvconst.h

## <a name="see-also"></a>请参阅
- [枚举和结构](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)
