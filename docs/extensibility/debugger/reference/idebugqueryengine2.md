---
title: IDebugQueryEngine2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2
helpviewer_keywords:
- IDebugQueryEngine2 interface
ms.assetid: 8f0e1838-a818-4459-9138-a3dceb7408de
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ad823c2aab4d2ca17b95c989925b8ffe16b1504d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66339850"
---
# <a name="idebugqueryengine2"></a>IDebugQueryEngine2
此接口允许的会话调试管理器 (SDM) 检索表示调试引擎 (DE) 的接口。

## <a name="syntax"></a>语法

```
IDebugQueryEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 DE 实现此接口上实现最常见的 DE 接口的对象 (如[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)， [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)，并[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)) 中若要允许访问的顺序[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) DE 本身的接口。

## <a name="notes-for-callers"></a>调用方的说明
 调用[QueryInterface](/cpp/atl/queryinterface)典型的 DE 接口来获取此接口上。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugQueryEngine2`。

|方法|描述|
|------------|-----------------|
|[GetEngineInterface](../../../extensibility/debugger/reference/idebugqueryengine2-getengineinterface.md)|获取自定义调试引擎 (DE) 接口。|

## <a name="remarks"></a>备注
 通常在实现的对象中实现此接口[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口以支持因果关系顺序逐句通过函数; 即，调试器跳出函数，下一步要执行的函数可能不是在堆栈上的上一个函数，但另一个线程中的函数完全。 有关"因果关系"的定义，请参阅[Visual Studio 调试器词汇表](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)