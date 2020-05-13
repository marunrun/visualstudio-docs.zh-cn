---
title: IDebug程序节点附加2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2
helpviewer_keywords:
- IDebugProgramNodeAttach2 interface
ms.assetid: 46b37ac9-a026-4ad3-997b-f19e2f8deb73
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d527dfcfcd09e4d70adca86436aa56e1852bee70
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721831"
---
# <a name="idebugprogramnodeattach2"></a>IDebugProgramNodeAttach2
允许通知程序节点尝试附加到关联的程序。

## <a name="syntax"></a>语法

```
IDebugProgramNodeAttach2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 此接口在实现[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)接口的同一类上实现，以便接收附加操作的通知并提供取消附加操作的机会。

## <a name="notes-for-callers"></a>呼叫者备注
 通过在`QueryInterface`[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象中调用方法来获取此接口。 在[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法之前必须调用[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法，以便给程序节点停止附加进程的机会。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)|附加到关联的程序或延迟附加过程到[附加](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法。|

## <a name="remarks"></a>备注
 此接口是弃用[Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)方法的首选替代方法。 所有调试引擎始终加载函数`CoCreateInstance`，即它们在正在调试的程序的地址空间之外实例化。

 如果`IDebugProgramNode2::Attach_V7`该方法的先前实现只是设置正在调试的程序`GUID`，则只需要实现[OnAttach](../../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)方法。

 如果`IDebugProgramNode2::Attach_V7`该方法的先前实现使用了提供的回调接口，则需要将该功能移动到[Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)方法的实现，`IDebugProgramNodeAttach2`并且不必实现该接口。

## <a name="requirements"></a>要求
 标题： Msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
- [Attach_V7](../../../extensibility/debugger/reference/idebugprogramnode2-attach-v7.md)
