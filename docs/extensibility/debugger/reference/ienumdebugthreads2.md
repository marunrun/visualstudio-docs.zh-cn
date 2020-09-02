---
title: IEnumDebugThreads2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80715092"
---
# <a name="ienumdebugthreads2"></a>IEnumDebugThreads2
此接口枚举当前调试会话中正在运行的线程。

## <a name="syntax"></a>语法

```
IEnumDebugThreads2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎 (DE) 实现此接口以表示程序中的线程列表。

## <a name="notes-for-callers"></a>调用方说明
 调用 [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md) 可获取此接口，该接口表示在进程中运行的所有程序中的所有线程的列表。 调用 [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md) 可获取表示程序中正在运行的线程列表的此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法 `IEnumDebugThreads2` 。

|方法|说明|
|------------|-----------------|
|[下一页](../../../extensibility/debugger/reference/ienumdebugthreads2-next.md)|检索枚举序列中指定数量的线程。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugthreads2-skip.md)|跳过枚举序列中指定数量的线程。|
|[重置](../../../extensibility/debugger/reference/ienumdebugthreads2-reset.md)|将枚举序列重置到开始处。|
|[克隆](../../../extensibility/debugger/reference/ienumdebugthreads2-clone.md)|创建与当前枚举数包含相同枚举状态的枚举数。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugthreads2-getcount.md)|获取枚举器中的线程数。|

## <a name="remarks"></a>备注
 Visual Studio 通常获取此接口以更新 " **线程** " 窗口以及获取列表的第一个线程，以便调用 [Execute](../../../extensibility/debugger/reference/idebugprocess3-execute.md)、 [Continue](../../../extensibility/debugger/reference/idebugprocess3-continue.md)和 [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprocess2-enumthreads.md)
- [EnumThreads](../../../extensibility/debugger/reference/idebugprogram2-enumthreads.md)
- [步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)
- [继续](../../../extensibility/debugger/reference/idebugprocess3-continue.md)
- [执行](../../../extensibility/debugger/reference/idebugprocess3-execute.md)
