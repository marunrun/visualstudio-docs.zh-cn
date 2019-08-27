---
title: IEEVisualizerService::GetCustomViewerList |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEEVisualizerService::GetCustomViewerList
helpviewer_keywords:
- IEEVisualizerService::GetCustomViewerList method
ms.assetid: 249d26ca-914f-43af-a400-8162477223f4
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c2ee2682b04b03b2b0bb04e0ba9ef5d9a2df8a35
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68192066"
---
# <a name="ieevisualizerservicegetcustomviewerlist"></a>IEEVisualizerService::GetCustomViewerList
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法返回此服务知道的类型可视化工具的列表。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetCustomViewerList(  
   ULONG                celtSkip,  
   ULONG                celtRequested,  
   DEBUG_CUSTOM_VIEWER* rgViewers,  
   ULONG*               pceltFetched  
);  
```  
  
```csharp  
int GetCustomViewerList(  
   uint                  celtSkip,  
   uint                  celtRequested,  
   DEBUG_CUSTOM_VIEWER[] rgViewers,  
   out uint              pceltFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celtSkip`  
 [in]可视化工具，以便跳过的数。  
  
 `celRequested`  
 [in]可视化工具，以便检索数 (还指定了大小的`rgViewers`数组)。  
  
 `rgViewers`  
 [in、 out]数组[DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)要填充的结构。  
  
 `pceltFetched`  
 [out]实际检索的可视化工具数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)将请求传递给此方法作为其支持的一部分的类型可视化工具。 如果表达式计算器还提供了相同类型的自定义查看器，它可以追加相应地填充扩展[DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)列表对这些自定义查看器的结构。 请确保[GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)反映了这些附加的浏览器。  
  
 请参阅[类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)有关可视化工具和查看器之间的差异的详细信息。  
  
## <a name="see-also"></a>请参阅  
 [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)   
 [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)   
 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)   
 [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)   
 [类型可视化工具和自定义查看器](../../../extensibility/debugger/type-visualizer-and-custom-viewer.md)
