---
title: IDebugPortEvents2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEvents2
helpviewer_keywords:
- IDebugPortEvents2 interface
ms.assetid: 2c017094-3ba2-4067-83f9-147df1d96bce
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9c611eb531bdabb633b11ac2e8ca2d0d11f52005
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725184"
---
# <a name="idebugportevents2"></a>IDebugPortEvents2
此接口通知侦听器（通常是会话调试管理器 [SDM] 或调试引擎）特定端口上的进程和程序创建和销毁。 此信息可用于显示在端口上运行的进程和程序的实时视图。

## <a name="syntax"></a>语法

```
IDebugPortEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 Visual Studio 通常实现此接口来接收有关程序创建和销毁的通知。 调试引擎还可以实现此接口来侦听此类端口事件。

## <a name="notes-for-callers"></a>呼叫者备注
 可以查询所有[IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)接口。 <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> 然后在接口中<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>调用`IDebugPortEvents2`方法以获取接口<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.FindConnectionPoint%2A> 最后，<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A>调用接口中<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>的方法通过[Event](../../../extensibility/debugger/reference/idebugportevents2-event.md)方法发送事件。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugPortEvents2`。

|方法|描述|
|------------|-----------------|
|[事件](../../../extensibility/debugger/reference/idebugportevents2-event.md)|发送描述端口上进程和程序的创建和销毁的事件。|

## <a name="remarks"></a>备注
 `IDebugPortEvents2`SDM 还用于调试在已调试的进程中运行的程序。

 端口事件通过此接口传递到 SDM。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
