---
title: IDiaStackFrame::get_lengthSavedRegisters | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_lengthSavedRegisters method
ms.assetid: b75fad6e-1ef4-44e6-89e3-c31c6fba10b3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3a06e96091a32f1425495a941f418a292f4155d2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741675"
---
# <a name="idiastackframeget_lengthsavedregisters"></a>IDiaStackFrame::get_lengthSavedRegisters
检索推送到堆栈上的已保存寄存器的字节数。

## <a name="syntax"></a>语法

```C++
HRESULT get_lengthSavedRegisters ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>参数
 `pRetVal`

弄返回已保存寄存器的字节数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果属性不受支持，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)