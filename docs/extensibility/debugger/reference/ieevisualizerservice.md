---
title: IEE可视化服务 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService
helpviewer_keywords:
- IEEVisualizerService interface
ms.assetid: 3bdb124b-c582-47ba-b465-13c6a1cdb702
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 40d21dcc9b1da0e1e2250adcfad59b3ef46a2113
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80717940"
---
# <a name="ieevisualizerservice"></a>IEEVisualizerService
> [!IMPORTANT]
> 在 Visual Studio 2015 中，这种实现表达式赋值器的方式被弃用。 有关实现 CLR 表达式赋值器的信息，请参阅[CLR 表达式赋值器](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)和[托管表达式赋值器示例](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)。

 此接口实现关键方法，为[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)和[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)接口提供功能。

## <a name="syntax"></a>语法

```
IEEVisualizerService : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
 Visual Studio 实现此接口，以允许表达式赋值器 （EE） 支持类型可视化器。

## <a name="notes-for-callers"></a>呼叫者备注
 EE 调用[CreateVisualizer 服务](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)以获取此接口，作为其对类型可视化器的支持的一部分。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法

|方法|描述|
|------------|-----------------|
|[GetCustomViewerCount](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)|检索此服务知道的自定义查看器数。|
|[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)|检索自定义查看器的列表。|
|[GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)|返回属性的代理对象。|
|[GetValueDisplayStringCount](../../../extensibility/debugger/reference/ieevisualizerservice-getvaluedisplaystringcount.md)|检索要为指定属性或字段显示的值字符串数。|

## <a name="remarks"></a>备注
 IDE 使用[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口来确定是否有任何自定义查看器或类型可视化器的属性。 通过创建可视化工具服务（使用[CreateVisualizer 服务](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)），EE 可以为`IDebugProperty3`和[IPropertyProxyEESide（](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)支持查看和更改属性的值）接口提供功能，从而支持类型可视化器。

 如果 EE 具有自身实现的自定义查看器，则 EE 可以将这些`CLSID`自定义查看器的 s 追加到[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)返回的列表末尾。 这允许 EE 同时支持类型可视化器及其自己的自定义查看器。 只需确保[GetCustomViewerCount 反映](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)任何自定义查看器的添加。

 有关可视化工具与查看器之间的差异的讨论，请参阅["类型可视化器"和"自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)"。

## <a name="requirements"></a>要求
 标题： ee.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [表达式计算接口](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [CreateVisualizerService](../../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)
- [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
