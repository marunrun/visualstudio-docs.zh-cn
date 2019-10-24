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
ms.openlocfilehash: d270b9b177367c9a15c2b64f6f8bc5607c5a459d
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741623"
---
# <a name="idiastackframeget_registervalue"></a>IDiaStackFrame::get_registerValue
检索存储在堆栈帧中的指定寄存器的值。

## <a name="syntax"></a>语法

```C++
HRESULT get_registerValue(
   ULONG      registerIndex,
   ULONGLONG *pRetVal
);
```

#### <a name="parameters"></a>参数
 `registerIndex`

中[CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)值之一。

 `pRetVal`

弄存储在寄存器中的值。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [CV_HREG_e 枚举](../../debugger/debug-interface-access/cv-hreg-e.md)