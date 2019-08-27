---
title: IDebugMemoryContext2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2
helpviewer_keywords:
- IDebugMemoryContext2 interface
ms.assetid: 3a544c8b-11dc-46bb-8549-261e4ac5bbc4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bb1abe29a915d8ca2aaba1135d2e57946250bc3f
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346974"
---
# <a name="idebugmemorycontext2"></a>IDebugMemoryContext2
此接口表示运行正在调试的程序的计算机的地址空间中的位置。

## <a name="syntax"></a>语法

```
IDebugMemoryContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 调试引擎 (DE) 实现此接口来表示内存中的地址。

## <a name="notes-for-callers"></a>调用方的说明
 调用[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)或[GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)返回此接口。 此外，调用[外](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)并[Subtract](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)应用适当的算术运算后返回的此接口的新副本。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示的方法`IDebugMemoryContext2`。

|方法|描述|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugmemorycontext2-getname.md)|获取此上下文中的用户可显示名称。|
|[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)|获取描述此上下文的信息。|
|[添加](../../../extensibility/debugger/reference/idebugmemorycontext2-add.md)|将指定的值添加到当前上下文的地址以创建新的上下文。|
|[相减](../../../extensibility/debugger/reference/idebugmemorycontext2-subtract.md)|减去指定的值从当前上下文的地址以创建新的上下文。|
|[Compare](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)|比较两个上下文的方式指示比较标志。|

## <a name="remarks"></a>备注
 Visual Studio**内存**窗口中调用[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)若要获取`IDebugMemoryContext2`包含计算的表达式使用的内存地址的接口。 然后将此上下文传递给[ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)并[WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)来指定要读取或写入的地址。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)
- [GetMemoryContext](../../../extensibility/debugger/reference/idebugreference2-getmemorycontext.md)
- [ReadAt](../../../extensibility/debugger/reference/idebugmemorybytes2-readat.md)
- [WriteAt](../../../extensibility/debugger/reference/idebugmemorybytes2-writeat.md)