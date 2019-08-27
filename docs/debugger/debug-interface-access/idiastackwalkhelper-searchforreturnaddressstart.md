---
title: 'Idiastackwalkhelper:: Searchforreturnaddressstart |Microsoft Docs'
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
ms.openlocfilehash: a311b10f2fc5b53daff58e93feec3a9cd6077d14
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62831977"
---
# <a name="idiastackwalkhelpersearchforreturnaddressstart"></a>IDiaStackWalkHelper::searchForReturnAddressStart
搜索指定的堆栈帧的寄信人地址处或附近指定的堆栈地址。

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

[in][IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象，表示当前堆栈帧。

 `startAddress`

[in]从此处开始搜索的虚拟内存地址。

 `ReturnAddress`

[out]返回最接近的函数返回地址`startAddress`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)