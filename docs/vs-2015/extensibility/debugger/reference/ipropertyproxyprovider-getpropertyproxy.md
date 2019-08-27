---
title: IPropertyProxyProvider::GetPropertyProxy |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IPropertyProxyProvider::GetPropertyProxy
helpviewer_keywords:
- IPropertyProxyProvider::GetPropertyProxy
ms.assetid: 3ebb7515-5bfe-48f4-9b8d-721b8f664eb6
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cc505799a0ea7571ccff41057ba9852018ddbb3e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68199461"
---
# <a name="ipropertyproxyprovidergetpropertyproxy"></a>IPropertyProxyProvider::GetPropertyProxy
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索属性代理接口的指定的代理 id。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetPropertyProxy(  
   DWORD                  dwID,  
   IPropertyProxyEESide** proxy  
);  
```  
  
```csharp  
int GetPropertyProxy(  
   uint                     dwID,  
   out IPropertyProxyEESide proxy  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwID`  
 [in]所需的属性代理的 ID。  
  
 `proxy`  
 [out]返回[IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 若要支持外部类型可视化工具，此方法通常将调用转发到[GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)方法。 请参阅[可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)有关如何获取 IEEVisualizerService 的详细信息。  
  
## <a name="see-also"></a>请参阅  
 [IPropertyProxyProvider](../../../extensibility/debugger/reference/ipropertyproxyprovider.md)   
 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)   
 [GetPropertyProxy](../../../extensibility/debugger/reference/ieevisualizerservice-getpropertyproxy.md)   
 [可视化和查看数据](../../../extensibility/debugger/visualizing-and-viewing-data.md)
