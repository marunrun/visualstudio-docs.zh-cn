---
title: 可视化和查看数据 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], viewing data
- debugging [Debugging SDK], visualizing data
ms.assetid: 699dd0f5-7569-40b3-ade6-d0fe53e832bc
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 719a2b3d073d90ff3977496c7f98ebecb1ab48a7
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65696315"
---
# <a name="visualizing-and-viewing-data"></a>可视化和查看数据
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

类型可视化工具和自定义查看器中快速对开发人员有意义的方式呈现数据。 表达式计算器 (EE) 可以支持第三方类型可视化工具，以及提供其自己的自定义查看器。  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 确定多少类型可视化工具和自定义查看器与相关联的对象类型通过调用[GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)方法。 如果没有至少一种类型的可视化工具或自定义查看器可用，则 Visual Studio 会调用[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)方法来检索这些可视化工具和查看器的列表 (实际上，列表`CLSID`s 实现可视化工具和查看器） 并将它们提供给用户。  
  
## <a name="supporting-type-visualizers"></a>支持的类型可视化工具  
 有多个 EE 必须实现以支持类型可视化工具的接口。 这些接口可以分为两大类： 这些列表类型可视化工具和访问属性数据。  
  
### <a name="listing-type-visualizers"></a>列表类型可视化工具  
 EE 支持列出在其实现类型可视化工具`IDebugProperty3::GetCustomViewerCount`和`IDebugProperty3::GetCustomViewerList`。 这些方法将传递到相应的方法调用[GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)并[GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)。  
  
 [IEEVisualizerService](../../extensibility/debugger/reference/ieevisualizerservice.md)获取通过调用[CreateVisualizerService](../../extensibility/debugger/reference/ieevisualizerserviceprovider-createvisualizerservice.md)。 此方法需要[IDebugBinder3](../../extensibility/debugger/reference/idebugbinder3.md)接口，即[IDebugBinder](../../extensibility/debugger/reference/idebugbinder.md)接口传递给[EvaluateSync](../../extensibility/debugger/reference/idebugparsedexpression-evaluatesync.md)。 `IEEVisualizerServiceProvider::CreateVisualizerService` 此外需要[IDebugSymbolProvider](../../extensibility/debugger/reference/idebugsymbolprovider.md)并[IDebugAddress](../../extensibility/debugger/reference/idebugaddress.md)接口已传递到`IDebugParsedExpression::EvaluateSync`。 若要创建所需的最终接口`IEEVisualizerService`接口是[IEEVisualizerDataProvider](../../extensibility/debugger/reference/ieevisualizerdataprovider.md) EE 实现的接口。 此接口允许要进行可视化处理的属性进行更改。 属性的所有数据都封装在[IDebugObject](../../extensibility/debugger/reference/idebugobject.md) EE 也会实现的接口。  
  
### <a name="accessing-property-data"></a>访问属性数据  
 访问属性数据是通过[IPropertyProxyEESide](../../extensibility/debugger/reference/ipropertyproxyeeside.md)接口。 若要获取此接口，Visual Studio 会调用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)上要获取的属性对象[IPropertyProxyProvider](../../extensibility/debugger/reference/ipropertyproxyprovider.md)接口 (实现的相同对象上实现[IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)接口)，然后调用[GetPropertyProxy](../../extensibility/debugger/reference/ipropertyproxyprovider-getpropertyproxy.md)方法来获取`IPropertyProxyEESide`接口。  
  
 所有数据都传递输入和输出`IPropertyProxyEESide`接口封装在[IEEDataStorage](../../extensibility/debugger/reference/ieedatastorage.md)接口。 此接口表示一个字节数组，由 Visual Studio 和 EE 实现。 当属性的数据更改时，Visual Studio 将创建`IEEDataStorage`保存新的数据和调用对象[CreateReplacementObject](../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)与该数据对象以获取新`IEEDataStorage`对象，它又是传递给[InPlaceUpdateObject](../../extensibility/debugger/reference/ipropertyproxyeeside-inplaceupdateobject.md)来更新该属性的数据。 `IPropertyProxyEESide::CreateReplacementObject` 允许 EE 来实例化其自己的类实现`IEEDataStorage`接口。  
  
## <a name="supporting-custom-viewers"></a>支持自定义查看器  
 该标志`DBG_ATTRIB_VALUE_CUSTOM_VIEWER`中设置`dwAttrib`字段[DEBUG_PROPERTY_INFO](../../extensibility/debugger/reference/debug-property-info.md)结构 (通过调用返回[GetPropertyInfo](../../extensibility/debugger/reference/idebugproperty2-getpropertyinfo.md)) 以指示该对象具有关联的自定义查看器使用它。 当设置此标志时，Visual Studio 将获取[IDebugProperty3](../../extensibility/debugger/reference/idebugproperty3.md)从接口[IDebugProperty2](../../extensibility/debugger/reference/idebugproperty2.md)接口使用[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)。  
  
 如果用户选择自定义查看器，Visual Studio 实例化使用查看器的自定义查看器`CLSID`提供的`IDebugProperty3::GetCustomViewerList`方法。 Visual Studio 然后调用[DisplayValue](../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)以向用户显示的值。  
  
 通常情况下，`IDebugCustomViewer::DisplayValue`呈现数据的只读视图。 若要允许对数据的更改，EE 必须实现自定义界面属性对象上支持不断变化的数据。 `IDebugCustomViewer::DisplayValue`方法使用此自定义接口来支持的数据更改。 该方法将查找自定义的接口`IDebugProperty2`接口作为传递`pDebugProperty`参数。  
  
## <a name="supporting-both-type-visualizers-and-custom-viewers"></a>同时支持类型的可视化工具和自定义查看器  
 类型可视化工具和自定义查看器中的，可以支持 EE [GetCustomViewerCount](../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)并[GetCustomViewerList](../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)方法。 首先，EE 将它提供的自定义查看器数添加到返回的值[GetCustomViewerCount](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewercount.md)方法。 第二，EE 追加`CLSID`返回的列表到其自己自定义查看器 s [GetCustomViewerList](../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [调试任务](../../extensibility/debugger/debugging-tasks.md)   
 [类型可视化工具和自定义查看器](../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
