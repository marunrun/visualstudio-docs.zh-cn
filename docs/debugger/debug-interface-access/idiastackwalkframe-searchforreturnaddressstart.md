---
title: 'Idiastackwalkframe:: Searchforreturnaddressstart |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::searchForReturnAddressStart method
ms.assetid: 47660b9b-6e4f-4dfa-88ab-63dce28f7412
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bf7de77016f5ccc15f2cea8bf3172321dd824096
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838049"
---
# <a name="idiastackwalkframesearchforreturnaddressstart"></a>IDiaStackWalkFrame::searchForReturnAddressStart
搜索指定的堆栈帧的寄信人地址处或附近指定的地址。

## <a name="syntax"></a>语法

```C++
HRESULT searchForReturnAddressStart ( 
   IDiaFrameData* frame,
   ULONGLONG      startAddress,
   ULONGLONG*     returnAddress
);
```

#### <a name="parameters"></a>参数
 `frame`

[in][IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象，表示当前堆栈帧。

 `startAddress`

[in]从此处开始搜索的虚拟内存地址。

 `returnAddress`

[out]返回最接近的函数返回地址`startAddress`。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)