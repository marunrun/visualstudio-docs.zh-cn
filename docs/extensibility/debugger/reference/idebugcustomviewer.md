---
title: IDebugCustomViewer |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomViewer
helpviewer_keywords:
- IDebugCustomViewer interface
ms.assetid: 7aca27d3-c7b8-470f-b42c-d1e9d9115edd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c44d2289180ece35725b9258e9d20abeb3a4cac3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80732415"
---
# <a name="idebugcustomviewer"></a>IDebugCustomViewer
此接口使表达式计算器 (EE) 以任何需要的格式显示属性值。

## <a name="syntax"></a>语法

```
IDebugCustomViewer : IUknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
EE 实现此接口以自定义格式显示属性值。

## <a name="notes-for-callers"></a>调用方说明
对 COM 函数的调用将 `CoCreateInstance` 实例化此接口。 `CLSID`传递给的 `CoCreateInstance` 是从注册表获取的。 对 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md) 的调用会获取注册表中的位置。 有关详细信息和示例，请参阅备注。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法
此接口实现以下方法：

|方法|说明|
|------------|-----------------|
|[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)|执行显示给定值所需的任何内容。|

## <a name="remarks"></a>备注
如果属性的值不能按正常方式显示（例如，使用数据表或其他复杂属性类型），则使用此接口。 由接口表示的自定义查看器与 `IDebugCustomViewer` 类型可视化工具不同，后者是一个外部程序，用于显示特定类型的数据，而不考虑 EE。 EE 实现特定于该 EE 的自定义查看器。 用户选择要使用的可视化工具类型，是类型可视化工具或自定义查看器。 有关此过程的详细信息，请参阅 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md) 。

自定义查看器的注册方式与 EE 相同，因此需要语言 GUID 和供应商 GUID。 确切的指标 (或注册表项名称) 只对 EE 知道。 此指标在 [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md) 结构中返回，后者又由对 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)的调用返回。 度量值中存储的值是 `CLSID` 传递给 COM 函数的， `CoCreateInstance` (参见示例) 。

用于 [调试函数的 SDK 帮助](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) `SetEEMetric` 器可用于注册自定义查看器。 `Debugging SDK Helpers`有关自定义查看器需要的特定注册表项，请参阅的 "表达式计算器" 注册表部分。 请注意，自定义查看器仅需一个指标 (由 EE 的实施者) 定义，而表达式计算器需要多个预定义的指标。

通常，自定义查看器提供数据的只读视图，因为提供给[DisplayValue](../../../extensibility/debugger/reference/idebugcustomviewer-displayvalue.md)的[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口没有用于更改该属性的值（作为字符串）的方法。 为了支持更改任意数据块，EE 在实现接口的同一对象上实现了一个自定义接口 `IDebugProperty3` 。 然后，此自定义接口将提供更改任意数据块所需的方法。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="example"></a>示例
此示例演示如何从属性获取第一个自定义查看器（如果该属性具有任何自定义查看器）。

```cpp
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

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
