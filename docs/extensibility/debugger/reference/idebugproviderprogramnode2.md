---
title: IDebugProviderProgramNode2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2
helpviewer_keywords:
- IDebugProviderProgramNode2
ms.assetid: f0bca1cc-afbe-44cf-b5aa-d078aa685d24
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 33c4a4914e15a8ecbea0d4f28c2325a952a042de
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353808"
---
# <a name="idebugproviderprogramnode2"></a>IDebugProviderProgramNode2
此接口将跨进程边界封送与程序相关的接口。

## <a name="syntax"></a>语法

```
IDebugProviderProgramNode2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口上实现的相同对象[IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)以支持跨进程边界封送处理的接口。

## <a name="notes-for-callers"></a>调用方的说明
 调用[QueryInterface](/cpp/atl/queryinterface)上`IDebugProgramNode2`接口，以获得此接口。 如果无法获取此接口，DE 不支持的接口封送处理。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[UnmarshalDebuggeeInterface](../../../extensibility/debugger/reference/idebugproviderprogramnode2-unmarshaldebuggeeinterface.md)|获取跨进程边界的指定的接口。|

## <a name="remarks"></a>备注
 DE 在单独的进程空间中运行从正在调试的程序时实现此接口： 例如，DE 运行时在 Visual Studio 进程空间而不是正在调试的程序的进程空间中。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)