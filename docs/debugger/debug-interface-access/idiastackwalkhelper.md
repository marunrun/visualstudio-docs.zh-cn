---
title: IDiaStackWalkHelper | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2 interface
ms.assetid: d66e5c84-565d-494e-8486-f91db9a34548
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 40c2b58778b2a1073b31acc7007388d8e8fe222c
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72741309"
---
# <a name="idiastackwalkhelper"></a>IDiaStackWalkHelper
使用程序调试数据库（.pdb）文件，有助于遍历堆栈。

## <a name="syntax"></a>语法

```

IDiaStackWalkHelper: IUnknown

```

## <a name="methods-in-vtable-order"></a>VTable Order 中的方法
 下表显示 `IDiaStackWalkHelper` 的方法：

|方法|描述|
|------------|-----------------|
|[IDiaStackWalkHelper::get_registerValue](../../debugger/debug-interface-access/idiastackwalkhelper-get-registervalue.md)|检索寄存器的值。|
|[IDiaStackWalkHelper::put_registerValue](../../debugger/debug-interface-access/idiastackwalkhelper-put-registervalue.md)|设置寄存器的值。|
|[IDiaStackWalkHelper::readMemory](../../debugger/debug-interface-access/idiastackwalkhelper-readmemory.md)|从可执行文件的图像的内存中读取数据块。|
|[IDiaStackWalkHelper::searchForReturnAddress](../../debugger/debug-interface-access/idiastackwalkhelper-searchforreturnaddress.md)|在指定的堆栈帧中搜索最近的函数返回地址。|
|[IDiaStackWalkHelper::searchForReturnAddressStart](../../debugger/debug-interface-access/idiastackwalkhelper-searchforreturnaddressstart.md)|在指定的堆栈帧中搜索指定堆栈地址或指定堆栈地址附近的返回地址。|
|[IDiaStackWalkHelper::frameForVA](../../debugger/debug-interface-access/idiastackwalkhelper-frameforva.md)|检索包含指定虚拟地址的堆栈帧。|
|[IDiaStackWalkHelper::symbolForVA](../../debugger/debug-interface-access/idiastackwalkhelper-symbolforva.md)|检索包含指定虚拟地址的符号。 **注意：** 符号必须具有类型 `SymTagFunctionType` （ [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)枚举中的值）。|
|[IDiaStackWalkHelper::pdataForVA](../../debugger/debug-interface-access/idiastackwalkhelper-pdataforva.md)|返回与指定的虚拟地址相关联的 PDATA 数据块。|
|[IDiaStackWalkHelper::imageForVA](../../debugger/debug-interface-access/idiastackwalkhelper-imageforva.md)|在可执行文件的内存空间中的某个位置，检索可执行文件的起始虚拟地址。|

## <a name="remarks"></a>备注
 此接口由 DIA 代码调用，以获取有关可执行文件的信息，以便在程序执行过程中构造堆栈帧的列表。

## <a name="notes-for-callers"></a>调用方说明
 客户端应用程序实现此接口以支持在程序执行期间遍历堆栈。 此接口的实例将传递给[IDiaStackWalker：： getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)或[IDiaStackWalker：： getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)方法。

## <a name="requirements"></a>要求
 标头： Dia2

 库： diaguids

 DLL： msdia80

## <a name="see-also"></a>请参阅
- [接口（调试接口访问 SDK）](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
- [SymTagEnum 枚举](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)
- [IDiaStackWalker::getEnumFrames2](../../debugger/debug-interface-access/idiastackwalker-getenumframes2.md)