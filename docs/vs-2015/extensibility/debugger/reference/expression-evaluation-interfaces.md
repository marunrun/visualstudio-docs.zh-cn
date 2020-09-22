---
title: 表达式计算接口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- expression evaluation, interfaces
ms.assetid: 2d259f60-2cd7-460e-b02d-24a8fb202850
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8a710019390120768b665cf3b27174831a67f0cc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840432"
---
# <a name="expression-evaluation-interfaces"></a>表达式计算接口
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [Clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 下面是用于调试 SDK 的表达式计算接口 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 。  
  
## <a name="discussion"></a>讨论 (Discussion)  
 这些接口用于在中断模式期间计算调用堆栈中的表达式。 它们仅实现了公共语言运行时表达式计算器 (EE) 。  
  
 表中的每个接口都显示可从以下列表中实现该接口的组件：  
  
-  (DE) 调试引擎  
  
- 表达式计算器 (EE)   
  
- Visual Studio (与)   
  
|接口|实现者|说明|  
|---------------|--------------------|-----------------|  
|[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)|EE|表示变量的数字别名。|  
|[IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)|EE|表示变量的数字别名，并使表达式计算器 (EE) 获取别名的应用程序域。|  
|[IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)|EE|表示一个数组对象。|  
|[IDebugArrayObject2](../../../extensibility/debugger/reference/idebugarrayobject2.md)|EE|表示托管数组对象，并允许表达式计算器 (EE) 确定数组 (下限) 的基本索引。|  
|[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)|DE|表示将调试符号绑定到内存中的实际地址的联编程序。|  
|[IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)|DE|与 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 接口相同，但提供对类型、别名和自定义可视化工具的访问。|  
|[IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)|EE|表示表达式计算器。|  
|[IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)|EE|表示表达式计算器 (EE) 的增强版本。|  
|[IDebugExpressionEvaluator3](../../../extensibility/debugger/reference/idebugexpressionevaluator3.md)|EE|表示包含增强的分析器树 (EE) 的表达式计算器。|  
|[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)|EE|表示函数。|  
|[IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)|EE|表示函数并增强 [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) 接口。|  
|[IDebugIDECallback](../../../extensibility/debugger/reference/idebugidecallback.md)|DE|启用表达式计算器 (EE) 在调试器的 "输出" 窗口中显示一条消息。|  
|[IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)|EE|表示托管代码对象。|  
|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)|EE|表示绑定到内存地址的任何符号的基接口。|  
|[IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)|EE|与 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 接口相同，但提供对其他信息的访问。|  
|[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)|EE|表示可以进行计算的已分析表达式。|  
|[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)|EE|表示指针。|  
|[IDebugPointerObject3](../../../extensibility/debugger/reference/idebugpointerobject3.md)|EE|表示分析树中的指针，并扩展 **IDebugPointerObject** 接口。|  
|[IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)|EE|提供通过类型可视化工具修改类型的值的功能。|  
|[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)|VS|提供对自定义查看器和类型可视化工具的访问。|  
|[IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)|VS|提供创建 [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) 对象的功能。|  
|[IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)|EE|表示 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象的集合。|  
  
## <a name="see-also"></a>另请参阅  
 [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)   
 [编写 CLR 表达式计算器](../../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)   
 [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
