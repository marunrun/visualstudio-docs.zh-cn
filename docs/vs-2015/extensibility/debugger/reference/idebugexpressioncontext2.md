---
title: IDebugExpressionContext2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2
helpviewer_keywords:
- IDebugExpressionContext2 interface
ms.assetid: 577fdaae-4b2d-4112-9839-ab899535fa6f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a18f546cf43ddff7f445ac0aa04a337487de0538
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192136"
---
# <a name="idebugexpressioncontext2"></a>IDebugExpressionContext2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示为表达式计算上下文  
  
## <a name="syntax"></a>语法  
  
```  
IDebugExpressionContext2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 调试引擎 (DE) 实现此接口来表示可在其中计算表达式的上下文。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)返回此接口。 仅当已暂停正在调试的程序和堆栈帧是可用时，此接口是可访问。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugExpressionContext2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetName](../../../extensibility/debugger/reference/idebugexpressioncontext2-getname.md)|检索评估上下文的名称。|  
|[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)|分析评估使用基于文本的表达式。|  
  
## <a name="remarks"></a>备注  
 评估上下文可以看作执行表达式计算的作用域。  
  
 会话调试管理器 (SDM) 时已停止程序，从通过调用 DE 获取堆栈帧[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)。 然后调用 SDM [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)若要获取`IDebugExpressionContext2`接口。 随后调用[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)来创建[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)接口，它表示分析可供计算的表达式。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)   
 [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
