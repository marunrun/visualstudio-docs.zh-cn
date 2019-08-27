---
title: IDiaStackFrame::get_cplusplusExceptionHandling | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_cplusplusExceptionHandling method
ms.assetid: f2631820-c986-40ca-b61e-230d7a9c426c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3f0c2e07b5c9141b8cf31511405939fc65be6446
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62839057"
---
# <a name="idiastackframegetcplusplusexceptionhandling"></a>IDiaStackFrame::get_cplusplusExceptionHandling
检索一个标志，指示如果C++实际上是异常处理。

## <a name="syntax"></a>语法

```C++
HRESULT get_cplusplusExceptionHandling ( 
   BOOL* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

[out]返回`TRUE`如果C++异常处理适用于此帧; 否则，返回`FALSE`。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果不支持的属性。 否则，返回错误代码。

## <a name="remarks"></a>备注
 C++异常处理不是结构化相同或系统异常处理。

 若要确定如果结构化异常处理的有效方法是，调用[IDiaStackFrame::get_systemExceptionHandling](../../debugger/debug-interface-access/idiastackframe-get-systemexceptionhandling.md)方法。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [IDiaStackFrame::get_systemExceptionHandling](../../debugger/debug-interface-access/idiastackframe-get-systemexceptionhandling.md)