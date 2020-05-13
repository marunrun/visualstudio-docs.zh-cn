---
title: IDebugProgramNode2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2
helpviewer_keywords:
- IDebugProgramNode2 interface
ms.assetid: 80e511d8-9b40-4a85-aa5d-952fa5ee6ae7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2e6eac7c97b9d375f32e36a372d6f31175c79098
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721911"
---
# <a name="idebugprogramnode2"></a>IDebugProgramNode2
此接口表示可以调试的程序。

## <a name="syntax"></a>语法

```
IDebugProgramNode2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 或自定义端口供应商实现此接口以表示可以调试的程序。 此接口通常实现于实现[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口的同一对象上。 此接口通过调用[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)][PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)注册。

## <a name="notes-for-callers"></a>呼叫者备注
 调用[获取提供程序程序节点](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)以返回此接口。 自定义端口供应商通过调用[AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)接收此接口。 DE 通过调用[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)接收此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugProgramNode2`。

|方法|描述|
|------------|-----------------|
|[GetProgramName](../../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)|获取程序的名称。|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)|获取承载程序的进程的名称。|
|[GetHostPid](../../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)|获取承载程序的进程的系统进程标识符。|
|[GetHostMachineName_V7](../../../extensibility/debugger/reference/idebugprogramnode2-gethostmachinename-v7.md)|废弃。 请勿使用。|
|[Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)|废弃。 请勿使用。 有关替代方法，请参阅[IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)接口。|
|[GetEngineInfo](../../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)|获取运行此程序的 DE 的名称和标识符。|
|[DetachDebugger_V7](../../../extensibility/debugger/reference/idebugprogramnode2-detachdebugger-v7.md)|废弃。 请勿使用。|

## <a name="remarks"></a>备注
 会话调试管理器 （SDM） 通常调用[GetProviderProgramnode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)以获取此接口。

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [AddProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
- [RemoveProgramNode](../../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)
- [PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)
