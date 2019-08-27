---
title: IDebugProgramEx2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2
helpviewer_keywords:
- IDebugProgramEx2 interface
ms.assetid: 663359ed-635a-4539-addb-0cc52f19d1bd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 13a9e44ee2a7782cb804c4e0b6f4279918e7d78e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325104"
---
# <a name="idebugprogramex2"></a>IDebugProgramEx2
此接口允许的会话调试管理器 (SDM) 附加到的程序和获取与程序关联的程序节点。

## <a name="syntax"></a>语法

```
IDebugProgramEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 自定义端口提供程序在与相同的对象上实现此接口[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)接口，以便让 SDM 附加到的程序，同时允许端口供应商联系，以跟踪所有会话附加到时程序。 如果还选择能自定义端口供应商可以实现此接口。

## <a name="notes-for-callers"></a>调用方的说明
 SDM 调用[QueryInterface](/cpp/atl/queryinterface)上`IDebugProgram2`接口，以获得此接口可跟踪已附加到程序的会话。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugProgramEx2`。

|方法|描述|
|------------|-----------------|
|[附加](../../../extensibility/debugger/reference/idebugprogramex2-attach.md)|将程序附加到会话。|
|[GetProgramNode](../../../extensibility/debugger/reference/idebugprogramex2-getprogramnode.md)|获取与程序关联的程序节点。|

## <a name="remarks"></a>备注
 此接口是专用 SDM 和程序之间。

## <a name="requirements"></a>要求
 标头：Portpriv.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)