---
title: 实现类型可视化工具和自定义查看器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: abef18c0-8272-4451-b82a-b4624edaba7d
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b780f2115400fd43e8915a5109c960cab99bf131
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63430223"
---
# <a name="implementing-type-visualizers-and-custom-viewers"></a>实现类型可视化工具和自定义查看器
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。  
  
 类型可视化工具和自定义查看器允许用户查看特定类型的数据是比简单的十六进制转储的数字更有意义的方式。 表达式计算器 (EE) 可以将自定义查看器与特定类型的数据或变量相关联。 EE 通过实现这些自定义查看器。 EE 还可以支持外部类型可视化工具，可能来自另一个第三方供应商或最终用户也是如此。  
  
## <a name="discussion"></a>讨论  
  
### <a name="type-visualizers"></a>类型可视化工具  
 Visual Studio 会询问有关类型可视化工具并为每个对象的自定义查看器监视窗口中显示的列表。 (EE) 的表达式计算器提供此类列表中的每种类型，它想要支持类型可视化工具和自定义查看器。 调用[GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)并[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)启动整个进程的访问类型可视化工具和自定义查看器 (请参阅[可视化和查看数据](../../extensibility/debugger/visualizing-and-viewing-data.md)有关调用的序列的详细信息)。  
  
### <a name="custom-viewers"></a>自定义查看器  
 自定义查看器在特定的数据类型为 EE 中实现并由[IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)接口。 自定义查看器不是灵活性不如类型可视化工具，因为它是可用的仅当执行 EE 实现该特定的自定义查看器时。 实现自定义查看器是实现类型可视化工具的支持比简单得多。 但是，支持类型可视化工具可以提供最大的灵活性向最终用户用于可视化他或她的数据。 在本文的其余部分涉及仅类型可视化工具。  
  
## <a name="interfaces"></a>接口  
 EE 实现以下接口才能支持类型可视化工具，可供 Visual Studio:  
  
- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)  
  
- [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md)  
  
- [IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)  
  
- [IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md)  
  
- [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)  
  
- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)  
  
  EE 使用了以下接口来支持类型可视化工具：  
  
- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)  
  
- [IEEVisualizerServiceProvider](../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)  
  
- [IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)  
  
## <a name="see-also"></a>请参阅  
 [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)   
 [可视化和查看数据](../../extensibility/debugger/visualizing-and-viewing-data.md)   
 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
