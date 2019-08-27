---
title: IDiaStackFrame::get_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_registerValue method
ms.assetid: cbe3d8ac-319a-40ac-bc3e-4eb81b2d7807
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a819293863b658f6e12609b2c1cd83c37532e02d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62832100"
---
# <a name="idiastackframegetregistervalue"></a>IDiaStackFrame::get_registerValue
检索指定寄存器的值，如存储在堆栈帧。

## <a name="syntax"></a>语法

```C++
HRESULT get_registerValue(
   ULONG      registerIndex,
   ULONGLONG *pRetVal
);
```

#### <a name="parameters"></a>参数
 `registerIndex`

[in]之一[CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)枚举值。

 `pRetVal`

[out]存储在寄存器的值。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)