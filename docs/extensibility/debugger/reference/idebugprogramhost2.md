---
title: IDebugProgramHost2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2
helpviewer_keywords:
- IDebugProgramHost2 interface
ms.assetid: 2c37b3aa-97a9-4665-8709-edd917f18cb1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 64db456e0c438f8665f122c3cd1b079c2ad1cea1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722220"
---
# <a name="idebugprogramhost2"></a>IDebugProgramHost2
此接口提供有关程序的主机（进程）信息。

## <a name="syntax"></a>语法

```
IDebugProgramHost2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎在[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口的同一对象上实现此接口，以提供有关托管过程的信息。 这是一个可选的接口。

## <a name="notes-for-callers"></a>呼叫者备注
 在`IDebugProgram2`接口上调用[查询接口](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugProgramHost2`。

|方法|描述|
|------------|-----------------|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostname.md)|获取此程序的托管过程的标题、友好名称或文件名。|
|[GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)|获取此程序的托管进程的进程标识符。|
|[GetHostMachineName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostmachinename.md)|获取运行此程序的托管进程的计算机的名称。|

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
