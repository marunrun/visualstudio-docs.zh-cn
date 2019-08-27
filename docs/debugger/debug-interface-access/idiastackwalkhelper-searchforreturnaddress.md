---
title: IDiaStackWalkHelper::searchForReturnAddress |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::searchForReturnAddress method
ms.assetid: 904223b1-6e26-4980-b310-d0b222cdbbbd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 87518257d9cab91976f69dd03c9026b0800a0680
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62837896"
---
# <a name="idiastackwalkhelpersearchforreturnaddress"></a>IDiaStackWalkHelper::searchForReturnAddress
搜索指定的堆栈帧的最接近的函数返回地址。

## <a name="syntax"></a>语法

```C++
HRESULT searchForReturnAddress( 
   IDiaFrameData*  frame,
   ULONGLONG*      returnAddress
);
```

#### <a name="parameters"></a>参数
 `frame`

[in][IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)对象，表示当前堆栈帧。

 `returnAddress`

[out]返回最接近的函数返回地址。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)