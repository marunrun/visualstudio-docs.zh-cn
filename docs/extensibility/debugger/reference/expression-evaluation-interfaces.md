---
title: 表达式评估接口 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- expression evaluation, interfaces
ms.assetid: 2d259f60-2cd7-460e-b02d-24a8fb202850
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: da230a2da87b2dd3e3a85ce3ec6c914e829ccc61
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736940"
---
# <a name="expression-evaluation-interfaces"></a>表达式计算接口
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 以下是调试 SDK 的[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]表达式评估接口。

## <a name="discussion"></a>讨论区
 这些接口用于在中断模式下计算调用堆栈中的表达式。 它们仅为通用语言运行时表达式赋值器 （EE） 实现。

 表中的每个接口都显示可以从以下列表中实现它的组件：

- 调试引擎 （DE）

- 表达式赋值器 （EE）

- 视觉工作室 （VS）

|接口|实施者|描述|
|---------------|--------------------|-----------------|
|[IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)|EE|表示变量的数字别名。|
|[IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)|EE|表示变量的数字别名，并使表达式赋值器 （EE） 能够获取别名的应用程序域。|
|[IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)|EE|表示一个数组对象。|
|[IDebugArrayObject2](../../../extensibility/debugger/reference/idebugarrayobject2.md)|EE|表示托管数组对象，并允许表达式赋值器 （EE） 确定数组的基本索引（下限）。|
|[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)|DE|表示将调试符号绑定到内存中的实际地址的活页夹。|
|[IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)|DE|与[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)接口相同，但提供对类型、别名和自定义可视化工具的访问。|
|[IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)|EE|表示表达式计算器。|
|[IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)|EE|表示表达式赋值器 （EE） 的增强版本。|
|[IDebugExpressionEvaluator3](../../../extensibility/debugger/reference/idebugexpressionevaluator3.md)|EE|表示具有增强解析器树的表达式赋值器 （EE）。|
|[IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)|EE|表示函数。|
|[IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)|EE|表示函数并增强[IDebug函数对象](../../../extensibility/debugger/reference/idebugfunctionobject.md)接口。|
|[IDebugIDECallback](../../../extensibility/debugger/reference/idebugidecallback.md)|DE|使表达式赋值器 （EE） 能够在调试器的输出窗口中显示消息。|
|[IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)|EE|表示托管代码对象。|
|[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)|EE|表示绑定到内存地址的任何符号的基接口。|
|[IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)|EE|与[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)接口相同，但提供对附加信息的访问。|
|[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)|EE|表示可供计算的已解析表达式。|
|[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)|EE|表示指针。|
|[IDebugPointerObject3](../../../extensibility/debugger/reference/idebugpointerobject3.md)|EE|表示解析树中的指针，并扩展**IDebugPointerObject**接口。|
|[IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)|EE|提供通过类型可视化工具修改类型值的能力。|
|[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)|VS|提供对自定义查看器和类型可视化工具的访问。|
|[IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)|VS|提供创建[IEE 可视化服务](../../../extensibility/debugger/reference/ieevisualizerservice.md)对象的能力。|
|[IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md)|EE|表示[IDebugObject 对象](../../../extensibility/debugger/reference/idebugobject.md)的集合。|

## <a name="see-also"></a>请参阅
- [API 参考](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
- [编写 CLR 表达式计算器](../../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
