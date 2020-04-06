---
title: IDebug提供程序程序节点2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2
helpviewer_keywords:
- IDebugProviderProgramNode2
ms.assetid: f0bca1cc-afbe-44cf-b5aa-d078aa685d24
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 815a945f6fb591960ebf0bf4b4fcd9d842ffefd3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720677"
---
# <a name="idebugproviderprogramnode2"></a>IDebugProviderProgramNode2
此接口跨进程边界封送程序相关接口。

## <a name="syntax"></a>语法

```
IDebugProviderProgramNode2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 在实现[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)以支持跨进程边界封送接口的同一对象上实现此接口。

## <a name="notes-for-callers"></a>呼叫者备注
 在`IDebugProgramNode2`接口上调用[查询接口](/cpp/atl/queryinterface)以获取此接口。 如果无法获取此接口，DE 不支持接口的封送。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[UnmarshalDebuggeeInterface](../../../extensibility/debugger/reference/idebugproviderprogramnode2-unmarshaldebuggeeinterface.md)|跨进程边界获取指定的接口。|

## <a name="remarks"></a>备注
 当 DE 在独立于正在调试的程序的进程空间中运行时，将实现此接口：例如，当 DE 在 Visual Studio 进程空间中运行时，而不是调试程序的进程空间。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
