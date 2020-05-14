---
title: IDebugProcessEx2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2
helpviewer_keywords:
- IDebugProcessEx2 interface
ms.assetid: 44e309ba-1d6f-499b-aa7e-9b34858a6d57
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 743dd1aa72d9b8db6b848618c8a2ad6c8c8ecaaf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723339"
---
# <a name="idebugprocessex2"></a>IDebugProcessEx2
此接口允许会话调试管理器 （SDM） 通知它附加到的进程或从进程分离的进程。

## <a name="syntax"></a>语法

```
IDebugProcessEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 自定义端口供应商在[IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)接口的同一对象上实现此接口，以便：

- 支持跟踪连接到进程的会话

- 支持跨多个调试引擎自动附加

  如果选择，自定义端口供应商可以实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注

- SDM 在`IDebugProcess2`接口上调用[查询接口](/cpp/atl/queryinterface)以获取此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugProcessEx2`。

|方法|描述|
|------------|-----------------|
|[Attach](../../../extensibility/debugger/reference/idebugprocessex2-attach.md)|通知进程会话正在调试进程。|
|[Detach](../../../extensibility/debugger/reference/idebugprocessex2-detach.md)|通知进程会话不再调试进程。|
|[AddImplicitProgramNodes](../../../extensibility/debugger/reference/idebugprocessex2-addimplicitprogramnodes.md)|为调试引擎列表添加程序节点。|

## <a name="remarks"></a>备注
 此接口在 SDM 和进程之间是私有的。

## <a name="requirements"></a>要求
 标题： 波特普里夫.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
