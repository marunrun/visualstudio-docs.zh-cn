---
title: IDebug记忆字节2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2
helpviewer_keywords:
- IDebugMemoryBytes2 interface
ms.assetid: d7647575-0e06-4190-88f5-ca40b82209a4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 56cb234e2295c5c9c08c2a2e9271e1c173524875
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727502"
---
# <a name="idebugmemorybytes2"></a>IDebugMemoryBytes2
此接口表示内存的字节数。

## <a name="syntax"></a>语法

```
IDebugMemoryBytes2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎 （DE） 实现此接口以表示内存中的字节。

## <a name="notes-for-callers"></a>呼叫者备注
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)返回此接口以提供对系统内存的访问。 [获取内存字节](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)和[获取内存字节](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)返回此接口以提供对对象的字节的访问。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugMemoryBytes2`。

|方法|描述|
|------------|-----------------|
|[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)|从给定位置开始读取字节序列。|
|[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)|写入`dwCount`字节，从`pStartContext`开始。|
|[GetSize](../../../extensibility/debugger/reference/idebugmemorybytes2-getsize.md)|获取此接口表示的内存的大小（以字节为单位）。|

## <a name="remarks"></a>备注
 对于属性，表示数组的[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)接口提供了`IDebugMemoryBytes2`一个接口来访问该数组中的值。

 Visual Studio 的**内存视图**调用[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md) `IDebugMemoryBytes2`来检索用于访问系统内存的接口。 要访问的地址是通过分析以地址输入到内存视图中的表达式，然后使用[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)计算解析的表达式来获取`IDebugProperty2`接口。 对[GetMemoryContext 的](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)调用返回描述内存地址的[IDebugMemoryContext2。](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 然后，此内存上下文将传递到[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)和[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
