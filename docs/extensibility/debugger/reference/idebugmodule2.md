---
title: IDebugModule2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2
helpviewer_keywords:
- IDebugModule2 interface
ms.assetid: 24c2a126-f4ab-4891-8509-8ef99b994c08
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dbbea1b52133de41dd26f437aeba31a0eff5a50a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726906"
---
# <a name="idebugmodule2"></a>IDebugModule2
此接口表示一个模块，即程序的可执行单元，如 DLL。

## <a name="syntax"></a>语法

```
IDebugModule2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示模块并提供对该模块信息的访问。

## <a name="notes-for-callers"></a>呼叫者备注
 对[GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)的调用将返回此接口。 DE 使用[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)方法将[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)接口发送到会话调试管理器 （SDM）。

 此接口也可以在[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构中返回（通过调用[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)返回）。

- [接下来](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md)还会返回此接口 （[枚举模块](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md)返回[IEnumDebugModule2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)接口）。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugModule2`。

|方法|描述|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)|获取描述此模块[MODULE_INFO。](../../../extensibility/debugger/reference/module-info.md)|
|[ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md)|已过时。 请勿使用。 重新加载此模块的符号。|

## <a name="remarks"></a>备注
 模块信息可以显示在 IDE 的 **"模块"** 窗口中。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [获取模块](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
