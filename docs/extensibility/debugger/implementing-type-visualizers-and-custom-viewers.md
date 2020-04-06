---
title: 实现类型可视化器和自定义查看器 |微软文档
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
ms.openlocfilehash: c2ebbb5c8e27df4ae4baf2d9a9f1c3314188e2b3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738506"
---
# <a name="implement-type-visualizers-and-custom-viewers"></a>实现类型可视化器和自定义查看器
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 类型可视化器和自定义查看器允许用户以比简单的十六进制数字转储更有意义的方式查看特定类型的数据。 表达式赋值器 （EE） 可以将自定义查看器与特定类型的数据或变量相关联。 这些自定义查看器由 EE 实现。 EE 还可以支持外部类型可视化工具，这些可视化工具可能来自其他第三方供应商甚至最终用户。

## <a name="discussion"></a>讨论区

### <a name="type-visualizers"></a>类型可视化器
 Visual Studio 要求列出要在监视窗口中显示的每个对象的类型可视化器和自定义查看器。 表达式赋值器 （EE） 为它希望支持类型可视化器和自定义查看器的每种类型提供此类列表。 对[GetCustomViewerCount 和](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md) [GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)的调用开始访问类型可视化器和自定义查看器的整个过程（有关调用序列的详细信息，请参阅[可视化和查看数据](../../extensibility/debugger/visualizing-and-viewing-data.md)）。

### <a name="custom-viewers"></a>自定义查看器
 自定义查看器在 EE 中为特定数据类型实现，并由[IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)接口表示。 自定义查看器不像类型可视化器那样灵活，因为它仅在执行该特定自定义查看器的 EE 时才可用。 实现自定义查看器比实现对类型可视化工具的支持更简单。 但是，支持类型可视化器为最终用户可视化其数据提供了最大的灵活性。 本讨论的其余部分仅涉及类型可视化工具。

## <a name="interfaces"></a>接口
 EE 实现以下接口以支持 Visual Studio 使用的型可视化工具：

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

## <a name="see-also"></a>请参阅
- [编写 CLR 表达式赋值器](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)
- [可视化和查看数据](../../extensibility/debugger/visualizing-and-viewing-data.md)
- [IDebugCustomViewer](../../extensibility/debugger/reference/idebugcustomviewer.md)
