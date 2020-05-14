---
title: IDebugdisassembly2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2
helpviewer_keywords:
- IDebugDisassemblyStream2 interface
ms.assetid: b03cab0c-3f0b-4cc6-88dc-acb3b48c567a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 98ba08e4ec32aceaf6c265714848939cc6ad9c66
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732046"
---
# <a name="idebugdisassemblystream2"></a>IDebugDisassemblyStream2
此接口表示指令流。

## <a name="syntax"></a>语法

```
IDebugDisassemblyStream2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎实现此接口以支持程序代码的拆解。

## <a name="notes-for-callers"></a>呼叫者备注
 对[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)方法的调用将返回此接口。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 下表显示了 的方法`IDebugDisassemblyStream2`。

|方法|描述|
|------------|-----------------|
|[读取](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)|读取从拆解流中的当前位置开始的指令。|
|[Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)|相对于指定位置，在拆解流中移动读取指针的给定指令数。|
|[GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)|返回特定代码上下文的代码位置标识符。|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)|返回与指定代码位置标识符对应的代码上下文对象。|
|[GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)|返回表示当前代码位置的代码位置标识符。|
|[GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)|获取与此拆解流关联的源文档。|
|[GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)|获取此拆解流的范围。|
|[GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)|获取此拆解流的大小。|

## <a name="remarks"></a>备注
 可以创建拆解流以表示整个地址空间，或者仅表示空间内的函数或模块。 每个指令都由对[Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)方法的调用返回的[拆解数据](../../../extensibility/debugger/reference/disassemblydata.md)结构表示。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
