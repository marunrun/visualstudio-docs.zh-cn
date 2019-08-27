---
title: IDebugObject::IsProxy |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugObject::IsProxy
- IsProxy
ms.assetid: 06c66b87-db95-4400-ab26-5d33e743a439
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0777a7e9696009124841ba177af70e5a23a6ea52
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180521"
---
# <a name="idebugobjectisproxy"></a>IDebugObject::IsProxy
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

确定对象是否透明代理。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT IsProxy (  
   BOOL* pfIsProxy  
);  
```  
  
```csharp  
int IsProxy (  
   out bool pfIsProxy  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pfIsProxy`  
 [out]`TRUE`的对象是否透明代理; 否则为`FALSE`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 默认情况下实现此方法C++调试引擎。  
  
## <a name="see-also"></a>请参阅  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
