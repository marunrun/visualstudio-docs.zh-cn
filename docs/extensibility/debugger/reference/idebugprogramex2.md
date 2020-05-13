---
title: IDebugProgramEx2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2
helpviewer_keywords:
- IDebugProgramEx2 interface
ms.assetid: 663359ed-635a-4539-addb-0cc52f19d1bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b8961ea105779674aab0b67c9ad6339ce1c282f9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722329"
---
# <a name="idebugprogramex2"></a>IDebugProgramEx2
此接口允许会话调试管理器 （SDM） 附加到程序，并获取程序节点与程序关联。

## <a name="syntax"></a>语法

```
IDebugProgramEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 自定义端口供应商在[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口的同一对象上实现此接口，以便允许 SDM 附加到程序，同时允许端口供应商跟踪附加到程序的所有会话。 如果选择，自定义端口供应商可以实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 SDM 在`IDebugProgram2`接口上调用[QueryInterface](/cpp/atl/queryinterface)以获取此接口以跟踪已附加到程序的会话。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugProgramEx2`。

|方法|描述|
|------------|-----------------|
|[Attach](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)|将程序附加到会话。|
|[GetProgramNode](../../../extensibility/debugger/reference/idebugprogramex2-getprogramnode.md)|获取与程序关联的程序节点。|

## <a name="remarks"></a>备注
 此接口在 SDM 和程序之间是私有的。

## <a name="requirements"></a>要求
 标题： 波特普里夫.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
