---
title: IDiaStackWalkHelper：： searchForReturnAddressStart |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper::searchForReturnAddressStart method
ms.assetid: 0a33142e-5d31-44ea-874a-a2e94d95cbd2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b0753cfe2d9ef8b08606185a5f57a3951f54e7de
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741337"
---
# <a name="idiastackwalkhelpersearchforreturnaddressstart"></a>IDiaStackWalkHelper::searchForReturnAddressStart
在指定的堆栈帧中搜索指定堆栈地址或指定堆栈地址附近的返回地址。

## <a name="syntax"></a>语法

```C++
HRESULT searchForReturnAddressStart( 
   IDiaFrameData*  frame,
   ULONGLONG       startAddress,
   ULONGLONG*      returnAddress
);
```

#### <a name="parameters"></a>参数
 `frame`

中表示当前堆栈帧的[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象。

 `startAddress`

中要从其开始搜索的虚拟内存地址。

 `ReturnAddress`

弄将最近的函数返回地址返回到 `startAddress`。

## <a name="return-value"></a>返回值
 如果成功，将返回 `S_OK`;否则，将返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)