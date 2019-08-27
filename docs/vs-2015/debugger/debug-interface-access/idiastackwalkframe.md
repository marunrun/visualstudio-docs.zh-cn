---
title: IDiaStackWalkFrame | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame interface
ms.assetid: 42d82845-d6f6-4846-9ecd-9dd169216077
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 27aab0ca87e589661798028ff38fb019dae815ed
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150134"
---
# <a name="idiastackwalkframe"></a>IDiaStackWalkFrame
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

维护之间的调用堆栈上下文[idiaframedata:: Execute](../../debugger/debug-interface-access/idiaframedata-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
IDiaStackWalkFrame : IUnknown  
```  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDiaStackWalkFrame`。  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaStackWalkFrame::get_registerValue](../../debugger/debug-interface-access/idiastackwalkframe-get-registervalue.md)|检索寄存器的值。|  
|[IDiaStackWalkFrame::put_registerValue](../../debugger/debug-interface-access/idiastackwalkframe-put-registervalue.md)|设置寄存器的值。|  
|[IDiaStackWalkFrame::readMemory](../../debugger/debug-interface-access/idiastackwalkframe-readmemory.md)|从图像中读取内存。|  
|[IDiaStackWalkFrame::searchForReturnAddress](../../debugger/debug-interface-access/idiastackwalkframe-searchforreturnaddress.md)|搜索指定的堆栈帧的最接近的函数返回地址。|  
|[IDiaStackWalkFrame::searchForReturnAddressStart](../../debugger/debug-interface-access/idiastackwalkframe-searchforreturnaddressstart.md)|搜索指定的堆栈帧的寄信人地址处或附近指定的地址。|  
  
## <a name="remarks"></a>备注  
 此接口用于在程序执行期间读取和写入寄存器，以及访问的内存和查找返回地址。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 客户端应用程序实现此接口，并将传递到接口的实例[idiaframedata:: Execute](../../debugger/debug-interface-access/idiaframedata-execute.md)方法。 重复使用此接口的同一实例的每个调用期间保存的寄存器状态`execute`方法。 `execute`方法还使用此接口来确定返回的地址。  
  
## <a name="requirements"></a>要求  
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaFrameData::execute](../../debugger/debug-interface-access/idiaframedata-execute.md)
