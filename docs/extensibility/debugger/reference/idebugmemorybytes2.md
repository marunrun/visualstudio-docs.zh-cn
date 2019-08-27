---
title: IDebugMemoryBytes2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2
helpviewer_keywords:
- IDebugMemoryBytes2 interface
ms.assetid: d7647575-0e06-4190-88f5-ca40b82209a4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b7496c7fb083558cec08bfc851f96075ea02bae9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66347117"
---
# <a name="idebugmemorybytes2"></a>IDebugMemoryBytes2
此接口表示内存字节数。

## <a name="syntax"></a>语法

```
IDebugMemoryBytes2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口来表示在内存中的字节数。

## <a name="notes-for-callers"></a>调用方的说明
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)返回此接口可提供对系统内存的访问。 [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)并[GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)返回此接口可提供对对象的字节数的访问。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugMemoryBytes2`。

|方法|描述|
|------------|-----------------|
|[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)|读取给定位置处开始的字节序列。|
|[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)|将写入`dwCount`开始的字节`pStartContext`。|
|[GetSize](../../../extensibility/debugger/reference/idebugmemorybytes2-getsize.md)|获取大小，以字节为单位，表示通过此接口的内存。|

## <a name="remarks"></a>备注
 对于属性， [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)接口表示一个数组提供`IDebugMemoryBytes2`界面来访问该数组中的值。

 Visual Studio**内存视图**调用[GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)检索`IDebugMemoryBytes2`用于访问系统内存接口。 获取要访问的地址通过分析为地址输入到内存视图表达式，以及然后计算分析得出的表达式使用[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)若要获取`IDebugProperty2`接口。 调用[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)返回[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)描述的内存地址。 然后将此内存上下文传递给[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)并[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugprogram2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)
- [GetMemoryBytes](../../../extensibility/debugger/reference/idebugreference2-getmemorybytes.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)