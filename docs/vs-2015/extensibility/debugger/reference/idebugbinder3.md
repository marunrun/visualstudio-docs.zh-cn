---
title: IDebugBinder3 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBinder3
helpviewer_keywords:
- IDebugBinder3 interface
ms.assetid: 92353a74-dc74-4f93-8762-61d6b220478c
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3f23c2ad4aeaf911e45b28686584d741e5c4d22f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65704140"
---
# <a name="idebugbinder3"></a>IDebugBinder3
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 此接口提供对类型、别名和自定义可视化工具服务的访问。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugBinder3 : IDebugBinder  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 调试引擎实现此接口以支持别名、自定义可视化工具服务和对对象类型信息的访问。  
  
## <a name="notes-for-callers"></a>调用方说明  
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)接口通过使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法  
 除了 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 接口提供的方法之外，此接口还实现以下内容：  
  
|方法|说明|  
|------------|-----------------|  
|[GetMemoryObject](../../../extensibility/debugger/reference/idebugbinder3-getmemoryobject.md)|检索表示此对象绑定到的内存的内存对象。|  
|[GetExceptionObjectAndType](../../../extensibility/debugger/reference/idebugbinder3-getexceptionobjectandtype.md)|如果任何) ，则检索与此对象关联的异常 (|  
|[FindAlias](../../../extensibility/debugger/reference/idebugbinder3-findalias.md)|检索别名，并为其指定名称。|  
|[GetAllAliases](../../../extensibility/debugger/reference/idebugbinder3-getallaliases.md)|检索此对象的所有别名的数组，|  
|[GetTypeArgumentCount](../../../extensibility/debugger/reference/idebugbinder3-gettypeargumentcount.md)|获取与此对象关联的参数类型的数目，|  
|[GetTypeArguments](../../../extensibility/debugger/reference/idebugbinder3-gettypearguments.md)|检索与此对象关联的参数类型的列表，|  
|[GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)|获取可视化工具服务的接口，|  
|[GetMemoryContext64](../../../extensibility/debugger/reference/idebugbinder3-getmemorycontext64.md)|将对象位置或64位内存地址转换为内存上下文。|  
  
## <a name="requirements"></a>要求  
 标头： ee。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
