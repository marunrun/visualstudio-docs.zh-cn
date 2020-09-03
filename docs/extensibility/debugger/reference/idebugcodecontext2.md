---
title: IDebugCodeContext2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80734208"
---
# <a name="idebugcodecontext2"></a>IDebugCodeContext2
此接口表示代码指令的起始位置。 对于今天的大多数运行时体系结构，可以将代码上下文视为程序的执行流中的地址。

## <a name="syntax"></a>语法

```
IDebugCodeContext2 : IDebugMemoryContext2
```

## <a name="notes-for-implementers"></a>实施者注意事项
 调试引擎实现此接口，以便将代码指令的位置与文档位置相关。

## <a name="notes-for-callers"></a>调用方说明
 许多接口上的方法返回此接口，最常见的方法是 [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)。 它还广泛用于 [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) 接口以及断点解析信息。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
 除了 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 接口上的方法，此接口还实现以下方法：

|方法|说明|
|------------|-----------------|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)|获取对应于活动代码上下文的文档上下文。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugcodecontext2-getlanguageinfo.md)|获取此代码上下文的语言信息。|

## <a name="remarks"></a>备注
 `IDebugCodeContext2`接口和[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)接口之间的主要区别在于 `IDebugCodeContext2` 始终为指令对齐。 这意味着， `IDebugCodeContext2` 始终指向指令的开头，而 `IDebugMemoryContext2` 可能指向运行时体系结构中的任何内存字节。 `IDebugCodeContext2` 按指令递增，而不是按基本存储大小递增 (通常为 byte) 。

## <a name="requirements"></a>要求
 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)
- [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)
- [下一页](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
