---
title: IDebugModule3 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3
helpviewer_keywords:
- IDebugModule3 interface
ms.assetid: 44f8e96e-9c59-4ffc-9a08-9c908a0e4de7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 84db1b672a9460ef3809162a2a1433f269796046
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726744"
---
# <a name="idebugmodule3"></a>IDebugModule3
此接口表示支持符号和 JustMyCode 状态的备用位置的模块。

## <a name="syntax"></a>语法

```
IDebugModule3 : IDebugModule2
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以支持符号的替代位置，并与 JustMyCode 状态配合使用（有关"JustMyCode"的定义，请参阅[可视化工作室调试器术语表](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)）。

## <a name="notes-for-callers"></a>呼叫者备注
 对[GetSymbolSearchSearchInfo 的](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)调用将返回此接口。 DE 使用[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)方法将[IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)接口发送到会话调试管理器 （SDM）。 此外，对[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md) [接口上的查询接口](/cpp/atl/queryinterface)的调用将返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)|返回搜索符号的路径列表和搜索每个路径的结果。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)|加载和初始化当前模块的符号。|
|[IsUserCode](../../../extensibility/debugger/reference/idebugmodule3-isusercode.md)|返回指示模块是否表示用户代码的标志。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugmodule3-setjustmycodestate.md)|指定是否应将模块视为用户代码。|

## <a name="remarks"></a>备注
 Visual Studio 是此接口的典型使用者。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)
- [GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)
