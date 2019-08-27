---
title: IDiaStackWalkHelper | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2 interface
ms.assetid: d66e5c84-565d-494e-8486-f91db9a34548
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 315af434271d57a8547963f2538ff1b799ef4fd3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68150027"
---
# <a name="idiastackwalkhelper"></a>IDiaStackWalkHelper
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

便于遍历堆栈使用程序调试数据库 (.pdb) 文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
IDiaStackWalkHelper: IUnknown  
  
```  
  
## <a name="methods-in-vtable-order"></a>VTable Order 中的方法  
 下表显示的方法`IDiaStackWalkHelper`:  
  
|方法|描述|  
|------------|-----------------|  
|[IDiaStackWalkHelper::get_registerValue](../../debugger/debug-interface-access/idiastackwalkhelper-get-registervalue.md)|检索寄存器的值。|  
|[IDiaStackWalkHelper::put_registerValue](../../debugger/debug-interface-access/idiastackwalkhelper-put-registervalue.md)|设置寄存器的值。|  
|[IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)|从可执行文件的映像在内存中读取数据的块。|  
|[IDiaStackWalkHelper::searchForReturnAddress](../../debugger/debug-interface-access/idiastackwalkhelper-searchforreturnaddress.md)|搜索指定的堆栈帧的最接近的函数返回地址。|  
|[IDiaStackWalkHelper::searchForReturnAddressStart](../../debugger/debug-interface-access/idiastackwalkhelper-searchforreturnaddressstart.md)|搜索指定的堆栈帧的寄信人地址处或附近指定的堆栈地址。|  
|[IDiaStackWalkHelper::frameForVA](../../debugger/debug-interface-access/idiastackwalkhelper-frameforva.md)|检索包含指定的虚拟地址的堆栈帧。|  
|[IDiaStackWalkHelper::symbolForVA](../../debugger/debug-interface-access/idiastackwalkhelper-symbolforva.md)|检索包含指定的虚拟地址的符号。 **注意：** 符号必须具有类型`SymTagFunctionType`(取值[SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)枚举)。|  
|[IDiaStackWalkHelper::pdataForVA](../../debugger/debug-interface-access/idiastackwalkhelper-pdataforva.md)|返回与指定的虚拟地址关联的 PDATA 数据块。|  
|[IDiaStackWalkHelper::imageForVA](../../debugger/debug-interface-access/idiastackwalkhelper-imageforva.md)|检索给定的虚拟地址某处的可执行文件的内存空间中的可执行文件，起始虚拟地址。|  
  
## <a name="remarks"></a>备注  
 此接口称为 DIA 代码以获取有关在程序执行过程中构造的堆栈帧的列表的可执行文件的信息。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 客户端应用程序实现此接口以支持在程序执行期间遍历堆栈。 此接口的实例传递给[IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)或[IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)方法。  
  
## <a name="requirements"></a>要求  
 标头：dia2.h  
  
 库： diaguids.lib  
  
 DLL: msdia80.dll  
  
## <a name="see-also"></a>请参阅  
 [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)   
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)   
 [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)   
 [IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)   
 [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)
