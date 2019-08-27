---
title: IDebugCustomViewer |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCustomViewer
helpviewer_keywords:
- IDebugCustomViewer interface
ms.assetid: 7aca27d3-c7b8-470f-b42c-d1e9d9115edd
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5f94fe0301777a615fa6dc567311c493ff55a90a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196297"
---
# <a name="idebugcustomviewer"></a>IDebugCustomViewer
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口允许的表达式计算器 (EE) 以显示在任何格式是必需的属性的值。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugCustomViewer : IUknown  
```  
  
## <a name="notes-for-implementers"></a>实施者的说明  
 EE 实现此接口可自定义格式显示属性的值。  
  
## <a name="notes-for-callers"></a>调用方的说明  
 调用 COM 的`CoCreateInstance`函数实例化此接口。 `CLSID`传递给`CoCreateInstance`从注册表获取。 调用[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)获取在注册表中的位置。 有关详细信息，以及该示例，请参阅备注。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
 此接口实现以下方法：  
  
|方法|描述|  
|------------|-----------------|  
|[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)|会执行任何所需显示给定的值。|  
  
## <a name="remarks"></a>备注  
 无法通过常规方法显示属性的值时使用此接口 — 例如，对于数据表或另一种复杂属性类型。 自定义查看器所表示的`IDebugCustomViewer`接口，不同于类型可视化工具，它是用于显示数据而不考虑 EE 特定类型的一个外部程序。 EE 实现特定于该 EE 的自定义查看器。 用户选择哪种类型的可视化工具使用，比如类型可视化工具或自定义查看器。 请参阅[可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)有关此过程的详细信息。  
  
 自定义查看器已注册 EE 的方式相同，因此，需要一种语言 GUID 和供应商的 GUID。 确切的指标 （或注册表项的名称） 才知道 EE。 此度量值中返回[DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)结构，它又通过调用返回[GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)。 存储指标中的值是`CLSID`传递给 COM 的`CoCreateInstance`函数 （请参见示例）。  
  
 [以便进行调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)函数， `SetEEMetric`，可以用于注册自定义查看器。 请参阅的"表达式计算器"注册表部分`Debugging SDK Helpers`对于特定的注册表键需要自定义查看器。 请注意，自定义查看器将需要只有一个度量值 （这由 EE 的实施者定义），而表达式计算器要求使用多个预定义的指标。  
  
 通常情况下，自定义查看器提供了只读的视图的数据，因为[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口提供给[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)没有更改除字符串形式的属性的值的方法。 为了支持更改任意数据块，EE 实现自定义接口上实现的相同对象`IDebugProperty3`接口。 此自定义接口然后将提供所需更改数据的任意块的方法。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>示例  
 此示例演示如何从属性获取第一个自定义查看器，该属性是否具有任何自定义查看器。  
  
```cpp#  
IDebugCustomViewer *GetFirstCustomViewer(IDebugProperty2 *pProperty)  
{  
    // This string is typically defined globally.  For this example, it  
    // is defined here.  
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";  
    IDebugCustomViewer *pViewer = NULL;  
    if (pProperty != NULL) {  
        CComQIPtr<IDebugProperty3> pProperty3(pProperty);  
        if (pProperty3 != NULL) {  
            HRESULT hr;  
            ULONG viewerCount = 0;  
            hr = pProperty3->GetCustomViewerCount(&viewerCount);  
            if (viewerCount > 0) {  
                ULONG viewersFetched = 0;  
                DEBUG_CUSTOM_VIEWER viewerInfo = { 0 };  
                hr = pProperty3->GetCustomViewerList(0,  
                                                     1,  
                                                     &viewerInfo,  
                                                     &viewersFetched);  
                if (viewersFetched == 1) {  
                    CLSID clsidViewer = { 0 };  
                    CComPtr<IDebugCustomViewer> spCustomViewer;  
                    // Get the viewer's CLSID from the registry.  
                    ::GetEEMetric(viewerInfo.guidLang,  
                                  viewerInfo.guidVendor,  
                                  viewerInfo.bstrMetric,  
                                  &clsidViewer,  
                                  strRegistrationRoot);  
                    if (!IsEqualGUID(clsidViewer,GUID_NULL)) {  
                        // Instantiate the custom viewer.  
                        spCustomViewer.CoCreateInstance(clsidViewer);  
                        if (spCustomViewer != NULL) {  
                            pViewer = spCustomViewer.Detach();  
                        }  
                    }  
                }  
            }  
        }  
    }  
    return(pViewer);  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)   
 [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)   
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
