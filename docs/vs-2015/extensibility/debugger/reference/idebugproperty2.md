---
title: IDebugProperty2 | Microsoft Docs
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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63403271"
---
# <a name="idebugproperty2"></a>IDebugProperty2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口表示堆栈帧属性、 程序文档属性或某些其他属性。 该属性通常是表达式计算的结果。  
  
> [!NOTE]
> "属性"的这种用法不应混淆，这意味着类的成员变量与尽管`IDebugProperty2`可以表示这样的实体。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProperty2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 DE 实现此接口来表示特定类型的值。 例如，值可能是由于表达式计算、 内存或寄存器和它们的值的列表显示所用的内存上下文的数字值。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)若要获取此接口，它表示的评估结果。 `IDebugExpression2::EvaluateAsync` 返回此接口通过发送[IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md) SDM，后者又调用接口[GetResult](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2-getresult.md)要检索其属性。  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md)返回关联的脚本文档提供此接口。  
  
 [GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md)返回此接口来表示一个函数的返回值。  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugprogram2-getdebugproperty.md)返回此接口来表示该程序，例如名称或内存上下文的各种属性。  
  
 [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)返回此接口来表示堆栈帧 （如本地变量） 的各种属性。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 下表显示的方法`IDebugProperty2`。  
  
|方法|描述|  
|------------|-----------------|  
|[GetPropertyInfo](../../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)|填写[DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)描述的属性的结构。|  
|[SetValueAsString](../../../extensibility/debugger/reference/idebugproperty2-setvalueasstring.md)|从字符串中设置属性的值。|  
|[SetValueAsReference](../../../extensibility/debugger/reference/idebugproperty2-setvalueasreference.md)|从给定引用的值设置属性的值。|  
|[EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)|枚举属性的子级。|  
|[GetParent](../../../extensibility/debugger/reference/idebugproperty2-getparent.md)|返回属性的父级。|  
|[GetDerivedMostProperty](../../../extensibility/debugger/reference/idebugproperty2-getderivedmostproperty.md)|返回描述属性的派生程度最高属性的属性。|  
|[GetMemoryBytes](../../../extensibility/debugger/reference/idebugproperty2-getmemorybytes.md)|返回构成的一个属性的值的内存字节数。|  
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugproperty2-getmemorycontext.md)|返回属性值的内存上下文。|  
|[GetSize](../../../extensibility/debugger/reference/idebugproperty2-getsize.md)|返回的大小，以字节为单位的属性值。|  
|[GetReference](../../../extensibility/debugger/reference/idebugproperty2-getreference.md)|返回对此属性的值的引用。|  
|[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)|返回一个属性的扩展的信息。|  
  
## <a name="remarks"></a>备注  
 属性，由表示`IDebugProperty2`接口，可视为具有名称、 类型和地址的值。 在更为通用的术语，`IDebugProperty2`可以表示任何内容的层次结构，与父项和子节点。  
  
 属性是通常是暂时的例如只相当于当前堆栈帧，持续时间。 另一方面，参考，由表示[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)接口，持续的时间，只要值保留在内存中。  
  
 可以使用 IDE`IDebugProperty2`接口以使用户可以浏览和修改在运行时属性。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
