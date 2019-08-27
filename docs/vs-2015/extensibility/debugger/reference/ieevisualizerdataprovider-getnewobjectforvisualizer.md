---
title: IEEVisualizerDataProvider::GetNewObjectForVisualizer |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEEVisualizerDataProvider::GetNewObjectForVisualizer
helpviewer_keywords:
- IEEVisualizerDataProvider::GetNewObjectForVisualizer method
ms.assetid: a898d549-4898-4fde-aad1-e8bb89129652
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dfd7045ebe846d79d51c0351a3e8d53b7a7128bd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196162"
---
# <a name="ieevisualizerdataprovidergetnewobjectforvisualizer"></a>IEEVisualizerDataProvider::GetNewObjectForVisualizer
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法获取可视化工具的一个新的对象。 此方法将始终从现有对象创建一个新的对象。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetNewObjectForVisualizer(  
   IDebugObject** ppObject  
);  
```  
  
```csharp  
int GetNewObjectForVisualizer(  
   out IDebugObject ppObject  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppObject`  
 [out]新的对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 `This method` 重新计算结果的对象，它当前表示并返回一个新的对象形式的结果。 将更新现有对象，作为评估结果。  
  
## <a name="see-also"></a>请参阅  
 [IEEVisualizerDataProvider](../../../extensibility/debugger/reference/ieevisualizerdataprovider.md)   
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
