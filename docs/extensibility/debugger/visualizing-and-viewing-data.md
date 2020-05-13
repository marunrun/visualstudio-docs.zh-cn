---
title: 可视化和查看数据 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], viewing data
- debugging [Debugging SDK], visualizing data
ms.assetid: 699dd0f5-7569-40b3-ade6-d0fe53e832bc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2b5f984e6c6a3c1c8f3835dfa93a8679ae16680a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712375"
---
# <a name="visualizing-and-viewing-data"></a>可视化和查看数据
键入可视化工具并自定义查看器以对开发人员来说快速有意义的方式呈现数据。 表达式赋值器 （EE） 可以支持第三方类型可视化器，以及提供自己的自定义查看器。

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]通过调用[GetCustomViewerCount 方法](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)确定与对象类型关联的类型可视化器和自定义查看器的数量。 如果至少有一种类型可视化工具或自定义查看器可用，Visual Studio 调用[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)方法来检索这些可视化工具和查看器的列表（实际上，是实现可视化器和查看器的 s 列表），并将其呈现给用户。

## <a name="supporting-type-visualizers"></a>支持类型可视化工具
 EE 必须实现许多接口来支持类型可视化工具。 这些接口可以分为两大类：列出类型可视化器的接口和访问属性数据的接口。

### <a name="listing-type-visualizers"></a>列表类型可视化工具
 EE 支持在其 实现`IDebugProperty3::GetCustomViewerCount`和`IDebugProperty3::GetCustomViewerList`中列出类型可视化器。 这些方法将调用传递给相应的方法[GetCustomViewerCount 和](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md) [getCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)。

 [IEE可视化服务](../../extensibility/debugger/reference/ieevisualizerservice.md)是通过调用[创建可视化服务](../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)获得的。 此方法需要[IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)接口，该接口是从传递给[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)的[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)接口获得的。 `IEEVisualizerServiceProvider::CreateVisualizerService`还需要[IDebugSymbol 提供程序](../../extensibility/debugger/reference/idebugsymbolprovider.md)和[IDebug地址](../../extensibility/debugger/reference/idebugaddress.md)接口，这些接口已`IDebugParsedExpression::EvaluateSync`传递到 。 创建`IEEVisualizerService`接口所需的最终接口是 EE 实现的[IEEVisualizer 数据提供程序](../../extensibility/debugger/reference/ieevisualizerdataprovider.md)接口。 此接口允许对要可视化的属性进行更改。 所有属性数据都封装在[IDebugObject](../../extensibility/debugger/reference/idebugobject.md)接口中，该接口也由 EE 实现。

### <a name="accessing-property-data"></a>访问属性数据
 访问属性数据是通过[IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md)接口完成的。 要获取此接口，Visual Studio 调用属性对象的[QueryInterface](/cpp/atl/queryinterface)以获取[IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)接口（实现在实现[IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)接口的同一对象上），然后调用[GetPropertyProxy](../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)方法`IPropertyProxyEESide`以获取该接口。

 传入和流出接口的`IPropertyProxyEESide`所有数据都封装在[IEEDataStorage 接口](../../extensibility/debugger/reference/ieedatastorage.md)中。 此接口表示字节数组，由 Visual Studio 和 EE 实现。 更改属性数据时，Visual `IEEDataStorage` Studio 会创建一个包含新数据的对象，并调用[CreateCreate 替代对象](../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)，以便获取一个新`IEEDataStorage`对象，该对象又传递到[InPlaceUpdateObject](../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)以更新属性的数据。 `IPropertyProxyEESide::CreateReplacementObject`允许 EE 实例化实现`IEEDataStorage`接口的自身类。

## <a name="supporting-custom-viewers"></a>支持自定义查看器
 标志`DBG_ATTRIB_VALUE_CUSTOM_VIEWER`在`dwAttrib`[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)结构的字段中设置（通过调用[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)返回）来指示对象具有与其关联的自定义查看器。 设置此标志时，Visual Studio 使用[查询接口](/cpp/atl/queryinterface)从[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口获取[IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)接口。

 如果用户选择自定义查看器，Visual Studio 将使用`CLSID``IDebugProperty3::GetCustomViewerList`该方法提供的查看器实例化自定义查看器。 然后，可视化工作室调用[DisplayValue](../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)向用户显示该值。

 通常，`IDebugCustomViewer::DisplayValue`显示数据的只读视图。 要允许对数据进行更改，EE 必须实现一个自定义接口，该接口支持更改属性对象上的数据。 该方法`IDebugCustomViewer::DisplayValue`使用此自定义接口支持更改数据。 该方法查找作为`IDebugProperty2``pDebugProperty`参数传入的接口上的自定义接口。

## <a name="supporting-both-type-visualizers-and-custom-viewers"></a>支持类型可视化器和自定义查看器
 EE 可以在[GetCustomViewerCount 和](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)[获取自定义查看器列表](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)方法中同时支持类型可视化器和自定义查看器。 首先，EE 会将其提供的自定义查看器数添加到[GetCustomViewerCount 方法](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)返回的值。 其次，EE 将自己的自定义`CLSID`查看器的 s 追加到[GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)方法返回的列表。

## <a name="see-also"></a>请参阅
- [调试任务](../../extensibility/debugger/debugging-tasks.md)
- [类型可视化器和自定义查看器](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
