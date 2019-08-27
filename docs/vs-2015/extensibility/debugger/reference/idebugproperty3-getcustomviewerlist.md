---
title: IDebugProperty3::GetCustomViewerList |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetCustomViewerList
helpviewer_keywords:
- IDebugProperty3::GetCustomViewerList
ms.assetid: 74490fd8-6f44-4618-beea-dab64961bb8a
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d709c9897aa80bdf18f06ae52147198323fcfef7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193400"
---
# <a name="idebugproperty3getcustomviewerlist"></a>IDebugProperty3::GetCustomViewerList
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取与此属性关联的自定义查看器的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetCustomViewerList(  
   ULONG                celtSkip,  
   ULONG                celtRequested,  
   DEBUG_CUSTOM_VIEWER* rgViewers,  
   ULONG*               pceltFetched  
);  
```  
  
```csharp  
int GetCustomViewerList(  
   uint                  celtSkip,  
   uint                  celtRequested,  
   DEBUG_CUSTOM_VIEWER[] rgViewers,  
   out uint              pceltFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celtSkip`  
 [in]若要跳过的查看者数。  
  
 `celtRequested`  
 [in]若要检索的查看者数 (还指定的大小`rgViewers`数组)。  
  
 `rgViewers`  
 [in、 out]数组[DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)要填充的结构。  
  
 `pceltFetched`  
 [out]返回的查看器的实际数目。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 若要支持类型可视化工具，此方法将调用转发到[GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)方法。 如果表达式计算器还支持用于此属性的类型的自定义查看器，此方法可以将相应自定义查看器附加到列表。  
  
 请参阅[类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)有关类型可视化工具和自定义查看器之间的差异的详细信息。  
  
## <a name="example"></a>示例  
 下面的示例演示如何实现此方法对于**CProperty**对象，它公开[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口。  
  
```cpp#  
STDMETHODIMP CProperty::GetCustomViewerList(ULONG celtSkip, ULONG celtRequested, DEBUG_CUSTOM_VIEWER* prgViewers, ULONG* pceltFetched)  
{  
    if (NULL == prgViewers)  
    {  
        return E_POINTER;  
    }  
  
    if (GetVisualizerService())  
    {  
        return m_pIEEVisualizerService->GetCustomViewerList(celtSkip, celtRequested, prgViewers, pceltFetched);  
    }  
    else  
    {  
        return E_NOTIMPL;  
    }  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)   
 [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)   
 [GetCustomViewerList](../../../extensibility/debugger/reference/ieevisualizerservice-getcustomviewerlist.md)   
 [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
