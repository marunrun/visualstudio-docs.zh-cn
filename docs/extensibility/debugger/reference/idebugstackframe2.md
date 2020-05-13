---
title: IDebugStackFrame2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2
helpviewer_keywords:
- IDebugStackFrame2 interface
ms.assetid: bd212a6a-dcc6-4756-a77a-e8dfda38b104
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 37acb9f2984c36130de494108ef4b76a59cc74e7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719512"
---
# <a name="idebugstackframe2"></a>IDebugStackFrame2
此接口表示特定线程中的调用堆栈中的单个堆栈帧。

## <a name="syntax"></a>语法

```
IDebugStackFrame2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示堆栈帧。

## <a name="notes-for-callers"></a>呼叫者备注
 调用[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)以检索[IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)接口。 调用[下一个](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)以检索包含接口的`IDebugStackFrame2` [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)结构。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugStackFrame2`。

|方法|描述|
|------------|-----------------|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|获取此堆栈帧的代码上下文。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|获取此堆栈框架的文档上下文。|
|[GetName](../../../extensibility/debugger/reference/idebugstackframe2-getname.md)|获取堆栈帧的名称。|
|[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)|获取堆栈帧的说明。|
|[GetPhysicalStackRange](../../../extensibility/debugger/reference/idebugstackframe2-getphysicalstackrange.md)|获取与堆栈帧关联的物理地址范围的与计算机相关的表示形式。|
|[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)|获取用于在堆栈框架和线程的当前上下文中执行表达式计算的评估上下文。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugstackframe2-getlanguageinfo.md)|获取与堆栈帧关联的语言。|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)|获取与堆栈帧关联的属性的说明。|
|[EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)|为堆栈帧属性创建枚举器。|
|[GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)|获取与堆栈帧关联的线程。|

## <a name="remarks"></a>备注
 仅当正在调试的程序在断点（由用户设置的断点或异常引起）停止时，才获得此接口。 在此接口中，可以获取表达式上下文以评估表达式，可以返回寄存器列表，也可以获取和检查调用堆栈。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
