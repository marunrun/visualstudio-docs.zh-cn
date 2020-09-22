---
title: IEEVisualizerServiceProvider |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEEVisualizerServiceProvider
helpviewer_keywords:
- IEEVisualizerServiceProvider interface
ms.assetid: 859d1a51-1c65-4c8b-ae74-3b74b181ebcd
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c9ba7c7216c590f773f1054a1f06cd3412ff6b20
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840464"
---
# <a name="ieevisualizerserviceprovider"></a>IEEVisualizerServiceProvider
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 此接口允许访问可创建可视化工具服务的方法，该服务用于处理 IDE 的类型可视化工具任务。  
  
## <a name="syntax"></a>语法  
  
```  
IEEVisualizerServiceProvider : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 Visual Studio 实现此接口来创建可视化工具服务对象，该对象进而用于向 `CLSID` Visual STUDIO IDE 提供类型可视化工具 () 类 id。  
  
## <a name="notes-for-callers"></a>调用方说明  
 表达式计算器 (EE) 调用 [GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md) 来获取此接口。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法  
  
|方法|说明|  
|------------|-----------------|  
|[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)|创建可视化工具服务|  
  
## <a name="remarks"></a>备注  
 `IEEVisualizerServiceProvider`接口是在实现[EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)的过程中获取的。 此接口创建的可视化工具服务用于向 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md) 接口提供功能，而该接口由 EE 负责实现。 EE 还负责实现允许类型可视化工具查看和修改属性值的 [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md) 接口。  
  
 有关这些接口如何交互的详细信息，请参阅 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md) 。  
  
## <a name="requirements"></a>要求  
 标头： ee。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [EvaluateSync](../../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)   
 [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)   
 [GetEEService](../../../extensibility/debugger/reference/idebugbinder3-geteeservice.md)   
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)   
 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
