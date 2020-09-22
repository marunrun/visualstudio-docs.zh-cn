---
title: IEEVisualizerDataProvider |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider
helpviewer_keywords:
- IEEVisualizerDataProvider interface
ms.assetid: 5fdfe6e3-b94e-4edb-acc5-41d8773d8ca5
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 86ad3f3ecec94c4c0773325ed2a571171b1f9b33
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840785"
---
# <a name="ieevisualizerdataprovider"></a>IEEVisualizerDataProvider
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 此接口提供通过类型可视化工具更改对象的值的功能。  
  
## <a name="syntax"></a>语法  
  
```  
IEEVisualizerDataProvider : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 表达式计算器实现此接口，以支持通过类型可视化工具修改属性对象上的数据。  
  
## <a name="notes-for-callers"></a>调用方说明  
 此接口在通过调用[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)创建[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)对象时使用。 有关更多详细信息，请参阅 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md) 。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法  
  
|方法|说明|  
|------------|-----------------|  
|[CanSetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-cansetobjectforvisualizer.md)|确定是否可以更新 (的对象，以及此可视化工具所表示) 其值。|  
|[GetNewObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getnewobjectforvisualizer.md)|强制重新计算此可视化工具的对象。|  
|[GetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-getobjectforvisualizer.md)|获取此可视化工具的现有对象， (未) 进行任何计算。|  
|[SetObjectForVisualizer](../../../extensibility/debugger/reference/ieevisualizerdataprovider-setobjectforvisualizer.md)|更新此可视化工具的对象，从而更改可视化工具显示的值。|  
  
## <a name="remarks"></a>备注  
 可视化工具服务 (由 [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) 接口表示，并由) [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md) 返回，以保留对实现接口的对象的引用 `IEEVisualizerDataProvider` 。 因此， `IEEVisualizerDataProvider` 如果该对象维护对该对象的引用，则不应在实现 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 的同一对象上实现接口 `IEEVisualizerService` ：循环引用结果和销毁对象时出现死锁。 推荐的方法是 `IEEVisualizerDataProvider` 在对象委托的单独对象上实现， `IDebugProperty2` 而无需对该对象进行调用 `IUnknown::AddRef` 。  
  
## <a name="requirements"></a>要求  
 标头： ee。h  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)   
 [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)   
 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
