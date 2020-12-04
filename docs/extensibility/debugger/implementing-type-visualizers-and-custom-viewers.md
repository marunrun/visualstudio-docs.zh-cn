---
title: 实现类型可视化工具和自定义查看器 |Microsoft Docs
description: 了解如何实现类型可视化工具和自定义查看器，使用户能够以更有意义的方式来查看数据。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], custom viewer
- debugging [Debugging SDK], type visualizer
ms.assetid: abef18c0-8272-4451-b82a-b4624edaba7d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fc3b1f2510742e2d0656727826e5b4aeae935b6f
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96559896"
---
# <a name="implement-type-visualizers-and-custom-viewers"></a>实现类型可视化工具和自定义查看器
> [!IMPORTANT]
> 在 Visual Studio 2015 中，不推荐使用这种实现表达式计算器的方式。 有关实现 CLR 表达式计算器的信息，请参阅 [clr 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) 和 [托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 类型可视化工具和自定义查看器允许用户以比简单的数字十六进制转储更有意义的方式查看特定类型的数据。 表达式计算器 (EE) 可以将自定义查看器与特定类型的数据或变量相关联。 这些自定义查看器是由 EE 实现的。 EE 还可以支持外部类型的可视化工具，可能来自其他第三方供应商，甚至最终用户。

## <a name="discussion"></a>讨论 (Discussion)

### <a name="type-visualizers"></a>类型可视化工具
 Visual Studio 要求提供可视化工具的类型可视化工具和自定义查看器，以便在 "监视" 窗口中显示每个对象。 表达式计算器 (EE) 为要支持类型可视化工具和自定义查看器的每个类型提供此类列表。 调用 [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) 和 [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) 会启动访问类型可视化工具和自定义查看器的整个过程 (查看 [可视化和查看数据](../../extensibility/debugger/visualizing-and-viewing-data.md) ，以获取有关调用序列) 的详细信息。

### <a name="custom-viewers"></a>自定义查看器
 自定义查看器在特定数据类型的 EE 中实现并由 [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md) 接口表示。 自定义查看器并不像类型可视化工具一样灵活，因为它仅在实现了特定自定义查看器的 EE 执行时可用。 实现自定义查看器比实现对类型可视化工具的支持更简单。 但是，支持类型可视化工具可为最终用户提供最大的灵活性，以便对其数据进行可视化。 本讨论的其余部分仅涉及类型可视化工具。

## <a name="interfaces"></a>接口
 EE 实现以下接口以支持 Visual Studio 使用的类型可视化工具：

- [IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)

- [IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md)

- [IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)

- [IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md)

- [IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)

- [IDebugObject](../../extensibility/debugger/reference/idebugobject.md)

  EE 使用以下接口来支持类型可视化工具：

- [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)

- [IEEVisualizerServiceProvider](../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)

- [IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)

## <a name="see-also"></a>另请参阅
- [编写 CLR 表达式计算器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [可视化和查看数据](../../extensibility/debugger/visualizing-and-viewing-data.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
