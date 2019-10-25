---
title: IDiaEnumStackFrames::Next | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumStackFrames::Next method
ms.assetid: 09378a21-d5e3-4213-b7e2-10f04d85295f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ffde40e221823d9656c4b6414b14067ac9d0537a
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72744044"
---
# <a name="idiaenumstackframesnext"></a>IDiaEnumStackFrames::Next
检索枚举序列中指定数目的堆栈帧元素。

## <a name="syntax"></a>语法

```C++
HRESULT Next( 
   ULONG             celt,
   IDiaStackFrame**  rgelt,
   ULONG*            pceltFetched
);
```

#### <a name="parameters"></a>参数
 celt

中要检索的枚举器中的堆栈帧元素的数目。

 rgelt

弄要使用请求的[IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)对象填充的数组。

 pceltFetched

弄返回提取的枚举器中的堆栈帧元素数。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果没有更多堆栈帧，则返回 `S_FALSE`。 否则，返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)