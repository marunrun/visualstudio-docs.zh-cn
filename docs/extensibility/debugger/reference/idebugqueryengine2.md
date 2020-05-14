---
title: IDebug查询引擎2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2
helpviewer_keywords:
- IDebugQueryEngine2 interface
ms.assetid: 8f0e1838-a818-4459-9138-a3dceb7408de
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 31b1784055c54c9243237c81edb708e13de9bc5b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720651"
---
# <a name="idebugqueryengine2"></a>IDebugQueryEngine2
此接口允许会话调试管理器 （SDM） 检索表示调试引擎 （DE） 的接口。

## <a name="syntax"></a>语法

```
IDebugQueryEngine2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 DE 在实现最常见的 DE 接口的对象（如[IDebugProgram2、IDebugThread2](../../../extensibility/debugger/reference/idebugprogram2.md)和[IDebugStackFrame2）](../../../extensibility/debugger/reference/idebugstackframe2.md)上实现此接口，以便允许访问 DE 本身的[IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)接口。 [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)

## <a name="notes-for-callers"></a>呼叫者备注
 在典型的 DE 接口上调用[查询接口](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugQueryEngine2`。

|方法|描述|
|------------|-----------------|
|[GetEngineInterface](../../../extensibility/debugger/reference/idebugqueryengine2-getengineinterface.md)|获取自定义调试引擎 （DE） 接口。|

## <a name="remarks"></a>备注
 此接口通常在实现[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口的对象中实现，以支持按因果关系顺序执行函数;也就是说，当调试器退出函数时，要执行的下一个函数可能不是堆栈上的上一个函数，而是另一个线程中的函数。 有关"因果关系"的定义，请参阅[可视化工作室调试器词汇表](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
