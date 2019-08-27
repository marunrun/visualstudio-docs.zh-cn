---
title: IDebugBreakpointResolution2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointResolution2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 451d5bce-b9c1-48ff-beaa-2b4c3e1ceea0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4884da23d3be45067884c295f80305683cb16abb
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352849"
---
# <a name="idebugbreakpointresolution2"></a>IDebugBreakpointResolution2
此接口表示用于描述绑定的断点的信息。

## <a name="syntax"></a>语法

```
IDebugBreakpointResolution2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口作为断点的支持的一部分。 此接口提供了会话调试管理器时用户查看断点的属性使用的绑定断点的说明。

## <a name="notes-for-callers"></a>调用方的说明
 调用[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugBreakpointResolution2`。

|方法|描述|
|------------|-----------------|
|[GetBreakpointType](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getbreakpointtype.md)|获取此解析由表示该断点的类型。|
|[GetResolutionInfo](../../../extensibility/debugger/reference/idebugbreakpointresolution2-getresolutioninfo.md)|获取描述此断点的断点解决方法信息。|

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [GetBreakpointResolution](../../../extensibility/debugger/reference/idebugboundbreakpoint2-getbreakpointresolution.md)