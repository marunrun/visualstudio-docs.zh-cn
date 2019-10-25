---
title: IDiaStackWalkFrame | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame interface
ms.assetid: 42d82845-d6f6-4846-9ecd-9dd169216077
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5b2657127726e387e81a5b28c639abbaa5399019
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741442"
---
# <a name="idiastackwalkframe"></a>IDiaStackWalkFrame
在调用[IDiaFrameData：： execute](../../debugger/debug-interface-access/idiaframedata-execute.md)方法之间维护堆栈上下文。

## <a name="syntax"></a>语法

```
IDiaStackWalkFrame : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示 `IDiaStackWalkFrame` 的方法。

|方法|描述|
|------------|-----------------|
|[IDiaStackWalkFrame::get_registerValue](../../debugger/debug-interface-access/idiastackwalkframe-get-registervalue.md)|检索寄存器的值。|
|[IDiaStackWalkFrame::put_registerValue](../../debugger/debug-interface-access/idiastackwalkframe-put-registervalue.md)|设置寄存器的值。|
|[IDiaStackWalkFrame::readMemory](../../debugger/debug-interface-access/idiastackwalkframe-readmemory.md)|从映像读取内存。|
|[IDiaStackWalkFrame::searchForReturnAddress](../../debugger/debug-interface-access/idiastackwalkframe-searchforreturnaddress.md)|在指定的堆栈帧中搜索最近的函数返回地址。|
|[IDiaStackWalkFrame::searchForReturnAddressStart](../../debugger/debug-interface-access/idiastackwalkframe-searchforreturnaddressstart.md)|在指定的堆栈帧中搜索指定地址处或附近的返回地址。|

## <a name="remarks"></a>备注
 在程序执行过程中，将使用此接口来读取和写入寄存器，以及访问内存和查找返回地址。

## <a name="notes-for-callers"></a>调用方说明
 客户端应用程序实现此接口，并将接口的实例传递给[IDiaFrameData：： execute](../../debugger/debug-interface-access/idiaframedata-execute.md)方法。 再次使用此接口的同一个实例，以便在每次调用 `execute` 方法的过程中保持寄存器的状态。 @No__t_0 方法还使用此接口来确定寄信人地址。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md)