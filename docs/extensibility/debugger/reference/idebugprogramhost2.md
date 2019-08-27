---
title: IDebugProgramHost2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2
helpviewer_keywords:
- IDebugProgramHost2 interface
ms.assetid: 2c37b3aa-97a9-4665-8709-edd917f18cb1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dc7a3222b2fab85657eea1eb0203f8c8da7dd5dc
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351222"
---
# <a name="idebugprogramhost2"></a>IDebugProgramHost2
此接口提供有关程序的主机 （进程） 信息。

## <a name="syntax"></a>语法

```
IDebugProgramHost2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎与相同的对象上实现此接口[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口，以提供有关托管进程的信息。 这是可选的接口。

## <a name="notes-for-callers"></a>调用方的说明
 调用[QueryInterface](/cpp/atl/queryinterface)上`IDebugProgram2`接口，以获得此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugProgramHost2`。

|方法|描述|
|------------|-----------------|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostname.md)|获取标题、 友好名称或此程序的宿主进程的文件名。|
|[GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)|获取此程序的宿主进程的进程标识符。|
|[GetHostMachineName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostmachinename.md)|获取此程序的宿主进程运行的计算机的名称。|

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)