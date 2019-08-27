---
title: IEEVisualizerService | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService
helpviewer_keywords:
- IEEVisualizerService interface
ms.assetid: 3bdb124b-c582-47ba-b465-13c6a1cdb702
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d3c9cff6b4de172e9331057bb56a39a87e8b6ab0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310117"
---
# <a name="ieevisualizerservice"></a>IEEVisualizerService
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种方式实现表达式计算器已弃用。 有关实现 CLR 表达式计算器的信息，请参阅[CLR 表达式计算器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)并[托管表达式计算器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口实现提供的功能的关键方法[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)并[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)接口。

## <a name="syntax"></a>语法

```
IEEVisualizerService : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
 Visual Studio 实现此接口以允许的表达式计算器 (EE) 来支持类型可视化工具。

## <a name="notes-for-callers"></a>调用方的说明
 EE 调用[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)此接口作为其支持的一部分获取的类型可视化工具。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法

|方法|描述|
|------------|-----------------|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)|检索此服务知道哪些自定义查看器数。|
|[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)|检索自定义查看器的列表。|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)|返回一个代理对象的属性。|
|[GetValueDisplayStringCount](../../../extensibility/debugger/reference/ieevisualizerservice-getvaluedisplaystringcount.md)|检索要显示为指定的属性或字段的值字符串数。|

## <a name="remarks"></a>备注
 IDE 使用[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口，以确定是否有任何自定义查看器，或键入属性的可视化工具。 通过创建可视化工具服务 (与[CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md))，EE 可以提供的功能提供给`IDebugProperty3`并[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md) (支持查看和更改属性的值） 接口，从而支持类型可视化工具。

 如果 EE 具有自定义查看器本身实现，可以将附加 EE`CLSID`到返回的列表的末尾这些自定义查看器 s [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)。 这允许 EE 支持类型可视化工具和其自己的自定义查看器。 只需务必[GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)反映添加的任何自定义查看器。

 请参阅[类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)有关可视化工具和查看器之间的差异的讨论。

## <a name="requirements"></a>要求
 标头： ee.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)