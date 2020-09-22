---
title: IDebugProperty2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProperty2
helpviewer_keywords:
- IDebugProperty2 interface
ms.assetid: a7d5c70f-a1a5-4120-9f70-184e01c25bff
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1f72a66e6dbfe2749910019760c16f6363498785
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840530"
---
# <a name="idebugproperty2"></a>IDebugProperty2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示堆栈帧属性、程序文档属性或其他属性。 属性通常是表达式计算的结果。  
  
> [!NOTE]
> 不应将 "属性" 的用法与这意味着类的成员变量相混淆，尽管 `IDebugProperty2` 可以表示此类实体。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProperty2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 DE 实现此接口来表示特定类型的值。 例如，值可以是表达式计算结果的数值、用于显示内存的内存上下文或寄存器及其值的列表。  
  
## <a name="notes-for-callers"></a>调用方说明  
 调用 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 或 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 以获取此接口，该接口表示求值的结果。 `IDebugExpression2::EvaluateAsync` 返回此接口，方法是将 [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) 接口发送到 SDM，后者又调用 [GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md) 来检索属性。  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md) 返回此接口以提供关联的脚本文档。  
  
 [GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md) 返回此接口以表示函数的返回值。  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md) 返回此接口以表示程序的各种属性，如名称或内存上下文。  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) 返回此接口以表示堆栈帧的各种属性，如局部变量。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法 `IDebugProperty2` 。  
  
|方法|说明|  
|------------|-----------------|  
|[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)|填充描述属性的 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) 结构。|  
|[SetValueAsString](../../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)|设置字符串的属性的值。|  
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugproperty2-setvalueasreference.md)|设置给定引用的值的属性值。|  
|[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)|枚举属性的子元素。|  
|[GetParent](../../../extensibility/debugger/reference/idebugproperty2-getparent.md)|返回属性的父。|  
|[GetDerivedMostProperty](../../../extensibility/debugger/reference/idebugproperty2-getderivedmostproperty.md)|返回描述属性的最常派生属性的属性。|  
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)|返回构成属性值的内存字节。|  
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)|返回属性值的内存上下文。|  
|[GetSize](../../../extensibility/debugger/reference/idebugproperty2-getsize.md)|返回属性值的大小（以字节为单位）。|  
|[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)|返回对此属性的值的引用。|  
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)|返回属性的扩展信息。|  
  
## <a name="remarks"></a>备注  
 由接口表示的属性 `IDebugProperty2` 可被视为一个具有名称、类型和地址的值。 在更常见的术语中， `IDebugProperty2` 可以使用父节点和子节点来表示具有层次结构的任何内容。  
  
 通常，属性是暂时的，只是当前堆栈帧（例如）的持续时间。 另一方面， [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 接口所表示的引用会持续到值保留在内存中。  
  
 IDE 可以使用 `IDebugProperty2` 接口允许用户在运行时浏览和修改属性。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
