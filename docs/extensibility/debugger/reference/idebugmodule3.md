---
title: IDebugModule3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3
helpviewer_keywords:
- IDebugModule3 interface
ms.assetid: 44f8e96e-9c59-4ffc-9a08-9c908a0e4de7
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 582c6fa887062986ccd1b66c7f3466b89407bcca
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323758"
---
# <a name="idebugmodule3"></a>IDebugModule3
此接口表示支持备用位置的符号和 JustMyCode 状态的模块。

## <a name="syntax"></a>语法

```
IDebugModule3 : IDebugModule2
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口以支持备用位置的符号，并可以使用 JustMyCode 状态 (请参阅[Visual Studio 调试器词汇表](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)"JustMyCode"的定义)。

## <a name="notes-for-callers"></a>调用方的说明
 调用[GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)返回此接口。 DE 发送[IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)会话调试管理器 (SDM) 使用接口[事件](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)方法。 此外，调用[QueryInterface](/cpp/atl/queryinterface)上[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)接口返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了上的方法[IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)接口，此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)|返回符号和搜索每个路径的结果的搜索路径的列表。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)|加载并初始化当前模块的符号。|
|[IsUserCode](../../../extensibility/debugger/reference/idebugmodule3-isusercode.md)|返回标志，指定该模块是否表示用户代码。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugmodule3-setjustmycodestate.md)|指定是否将模块应被视为用户代码还是不。|

## <a name="remarks"></a>备注
 Visual Studio 是典型的使用者使用此接口。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)
- [GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)