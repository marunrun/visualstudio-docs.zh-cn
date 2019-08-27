---
title: IDebugModule2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2
helpviewer_keywords:
- IDebugModule2 interface
ms.assetid: 24c2a126-f4ab-4891-8509-8ef99b994c08
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b621ae3b1408bc4af371243a1c34909117d40576
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323932"
---
# <a name="idebugmodule2"></a>IDebugModule2
此接口表示模块 — 即，程序可执行单元，如的 DLL。

## <a name="syntax"></a>语法

```
IDebugModule2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口来表示一个模块，并为访问有关该模块的信息。

## <a name="notes-for-callers"></a>调用方的说明
 调用[GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)返回此接口。 DE 发送[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)会话调试管理器 (SDM) 使用接口[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)方法。

 在中，此接口也会返回[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构 (通过调用返回[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md))。

- [下一步](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md)也会返回此接口 ([EnumModules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)返回[IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)接口)。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugModule2`。

|方法|描述|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)|获取[MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)用于描述此模块。|
|[ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md)|已过时。 不要使用。 重新加载此模块的符号。|

## <a name="remarks"></a>备注
 模块信息可以显示在**模块**在 IDE 的窗口。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)