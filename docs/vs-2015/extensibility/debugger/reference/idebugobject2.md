---
title: IDebugObject2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject2
helpviewer_keywords:
- IDebugObject2 interface
ms.assetid: ef640967-8adb-4793-994d-ae1736510891
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 979ede5601f1f31ca972bb9067b626954b1296f7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65695201"
---
# <a name="idebugobject2"></a>IDebugObject2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 此接口提供有关对象的其他信息。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugObject2 : IDebugObject  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 表达式计算器实现此接口，以提供对别名的支持以及对对象信息的访问。  
  
## <a name="notes-for-callers"></a>调用方说明  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口可以使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)获取此接口。 此外， [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md) 返回此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法  
 除了 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口上的方法之外， `IDebugObject2` 接口还实现以下各项：  
  
|方法|说明|  
|------------|-----------------|  
|[GetBackingFieldForProperty](../../../extensibility/debugger/reference/idebugobject2-getbackingfieldforproperty.md)|如果任何可能支持此对象所表示的属性的) ，则获取字段或变量 (。|  
|[GetICorDebugValue](../../../extensibility/debugger/reference/idebugobject2-geticordebugvalue.md)|获取表示此对象的值的托管代码对象。|  
|[CreateAlias](../../../extensibility/debugger/reference/idebugobject2-createalias.md)|为此对象创建唯一 ID，或返回现有别名。|  
|[GetAlias](../../../extensibility/debugger/reference/idebugobject2-getalias.md)|获取与此对象关联的别名（如果有）。|  
|[GetField](../../../extensibility/debugger/reference/idebugobject2-getfield.md)|获取此对象的类型。|  
|[IsUserData](../../../extensibility/debugger/reference/idebugobject2-isuserdata.md)|确定此对象是否表示用户数据。|  
|[IsEncOutdated](../../../extensibility/debugger/reference/idebugobject2-isencoutdated.md)|确定 "编辑并继续" 状态是否不再有效。<br /><br /> 自定义表达式计算器不实现此方法 (应始终返回 `E_NOTIMPL`) 。|  
  
## <a name="remarks"></a>备注  
 有关别名的讨论，请参阅 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) 。  
  
## <a name="requirements"></a>要求  
 标头： ee。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)   
 [GetObject](../../../extensibility/debugger/reference/idebugalias-getobject.md)
