---
title: IDebugCodeContext2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2
helpviewer_keywords:
- IDebugCodeContext2 interface
ms.assetid: 3670439e-2171-405d-9d77-dedb0f1cba93
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 778602cc29049d855c418fd8fa416feb1ad8e9fe
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734208"
---
# <a name="idebugcodecontext2"></a>IDebugCodeContext2
此接口表示代码指令的起始位置。 对于当今的大多数运行时体系结构，可以将代码上下文视为程序执行流中的地址。

## <a name="syntax"></a>语法

```
IDebugCodeContext2 : IDebugMemoryContext2
```

## <a name="notes-for-implementers"></a>实施者说明
 调试引擎实现此接口，将代码指令的位置与文档位置相关联。

## <a name="notes-for-callers"></a>呼叫者备注
 许多接口上的方法返回此接口，最常见的是[GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)。 它还广泛用于[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)接口以及断点分辨率信息。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)接口上的方法外，此接口还实现了以下方法：

|方法|描述|
|------------|-----------------|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)|获取与活动代码上下文对应的文档上下文。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugcodecontext2-getlanguageinfo.md)|获取此代码上下文的语言信息。|

## <a name="remarks"></a>备注
 接口和[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)接口之间的主要区别是，始终`IDebugCodeContext2`与指令对齐。 `IDebugCodeContext2` 这意味着 始终`IDebugCodeContext2`指向指令的开头，而 可以`IDebugMemoryContext2`指向运行时体系结构中的任何字节内存。 `IDebugCodeContext2`由指令而不是基本存储大小（通常字节）递增。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)
- [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)
- [下一步](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
