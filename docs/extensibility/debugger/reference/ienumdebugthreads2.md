---
title: IEnum调试线程2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2
helpviewer_keywords:
- IEnumDebugThreads2
ms.assetid: 1854f078-3b49-42c2-b65b-33e3b506fd63
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bbbe047c08f8e91264163d028c1b40d94cde97fc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715092"
---
# <a name="ienumdebugthreads2"></a>IEnumDebugThreads2
此接口枚举在当前调试会话中运行的线程。

## <a name="syntax"></a>语法

```
IEnumDebugThreads2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示程序中的线程列表。

## <a name="notes-for-callers"></a>呼叫者备注
 调用[EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)以获取此接口，以表示进程中运行的所有程序中所有线程的列表。 调用[EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)以获取此接口，表示程序中正在运行的线程列表。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IEnumDebugThreads2`。

|方法|描述|
|------------|-----------------|
|[下一步](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md)|检索枚举序列中指定数量的线程。|
|[跳](../../../extensibility/debugger/reference/ienumdebugthreads2-skip.md)|在枚举序列中跳过指定数量的线程。|
|[重置](../../../extensibility/debugger/reference/ienumdebugthreads2-reset.md)|将枚举序列重置为开头。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugthreads2-clone.md)|创建与当前枚举状态相同的枚举器。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugthreads2-getcount.md)|获取枚举器中的线程数。|

## <a name="remarks"></a>备注
 Visual Studio 通常获取此接口以更新**线程**窗口以及获取列表的第一个线程，以便调用[执行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)、[继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)和[步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
- [步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)
- [继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
- [执行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)
