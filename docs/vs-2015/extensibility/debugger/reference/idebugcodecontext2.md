---
title: IDebugCodeContext2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCodeContext2
helpviewer_keywords:
- IDebugCodeContext2 interface
ms.assetid: 3670439e-2171-405d-9d77-dedb0f1cba93
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2e06fd709b2d076b6fa8de7f104e907eb1b35a42
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68190954"
---
# <a name="idebugcodecontext2"></a>IDebugCodeContext2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示的代码指令的起始位置。 为大多数运行时体系结构现在，代码上下文可以认为的程序的执行流中的地址。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugCodeContext2 : IDebugMemoryContext2  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎实现此接口可关联到的文档位置的代码指令的位置。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 多个接口上的方法最通常情况下，返回此接口， [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)。 它还用于广泛[IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)接口也与断点解决方法信息。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 除了上的方法[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)接口，此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)|获取与活动的代码上下文相对应的文档上下文。|  
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugcodecontext2-getlanguageinfo.md)|获取此代码的上下文的语言信息。|  
  
## <a name="remarks"></a>备注  
 主要区别`IDebugCodeContext2`接口和一个[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)接口是`IDebugCodeContext2`始终指令对齐。 这意味着`IDebugCodeContext2`始终指向到的指令，开头而`IDebugMemoryContext2`都可能会导致运行时体系结构中的内存的任何字节。 `IDebugCodeContext2` 就会增加通过说明而不是基本的存储大小 （通常为字节）。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)   
 [CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)   
 [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)   
 [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)   
 [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)   
 [下一步](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)   
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
