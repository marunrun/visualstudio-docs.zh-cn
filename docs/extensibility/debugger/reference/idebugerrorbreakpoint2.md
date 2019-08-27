---
title: IDebugErrorBreakpoint2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorBreakpoint2
helpviewer_keywords:
- IDebugErrorBreakpoint2 interface
ms.assetid: 1f2a4b94-3713-46e9-8272-3917187792bd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2f25187b2aa88153fcfd712b9dd4b0f651ba8860
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66327789"
---
# <a name="idebugerrorbreakpoint2"></a>IDebugErrorBreakpoint2
此接口表示一个错误或警告断点，如无效的位置、 无效的表达式或为何挂起断点具有未绑定 （代码不会加载尚未，依此类推） 的原因。

## <a name="syntax"></a>语法

```
IDebugErrorBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎实现此接口作为断点的支持的一部分。 此接口用于报告绑定断点的问题。

## <a name="notes-for-callers"></a>调用方的说明
 调用[GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)获取此接口。 此接口，也会返回 (由表示列表的一部分[IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)接口) 通过调用[CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)或[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugErrorBreakpoint2`。

|方法|描述|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|获取导致了错误的挂起断点。|
|[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|获取描述错误断点错误解决方法。|

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
- [GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)
- [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-next.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)