---
title: IDebugCoreServer2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer2
helpviewer_keywords:
- IDebugCoreServer2 interface
ms.assetid: 9c47d0a6-9eb1-464e-bd44-fa2b552d4d36
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7a5990c84fbaeb5ebb3b1e188d3317234afda06b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733037"
---
# <a name="idebugcoreserver2"></a>IDebugCoreServer2
此接口用于表示和获取网络上的计算机上的服务器的信息。

## <a name="syntax"></a>语法

```
IDebugCoreServer2 : IUknown
```

## <a name="notes-for-implementers"></a>实施者说明
 Visual Studio 实现此接口以表示服务器。 Visual Studio 的每个实例都创建此接口的实例。

## <a name="notes-for-callers"></a>呼叫者备注
 自定义端口供应商在调用[事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)中接收此接口。

 调试引擎可以通过调用[GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)间接获取此接口（它返回[IDebugCoreServer3，](../../../extensibility/debugger/reference/idebugcoreserver3.md)一个派生自`IDebugCoreServer2`的接口）。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugCoreServer2`。

|方法|描述|
|------------|-----------------|
|[GetMachineInfo](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineinfo.md)|获取计算机的名称和属性。|
|[GetMachineName](../../../extensibility/debugger/reference/idebugcoreserver2-getmachinename.md)|获取计算机的名称。|
|[GetPortSupplier](../../../extensibility/debugger/reference/idebugcoreserver2-getportsupplier.md)|获取计算机上存在的端口供应商。|
|[GetPort](../../../extensibility/debugger/reference/idebugcoreserver2-getport.md)|获取计算机上已存在的端口。|
|[EnumPorts](../../../extensibility/debugger/reference/idebugcoreserver2-enumports.md)|为计算机上的所有端口创建枚举器。|
|[EnumPortSuppliers](../../../extensibility/debugger/reference/idebugcoreserver2-enumportsuppliers.md)|为计算机上的所有端口供应商创建枚举器。|
|[GetMachineUtilities_V7](../../../extensibility/debugger/reference/idebugcoreserver2-getmachineutilities-v7.md)|获取机器的机器实用程序。|

## <a name="remarks"></a>备注
 Visual Studio 还使用此接口来浏览在网络上计算机上运行的进程。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)
- [GetServer](../../../extensibility/debugger/reference/idebugdefaultport2-getserver.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
