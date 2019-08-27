---
title: IEnumDebugReferenceInfo2::Next |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugReferenceInfo2::Next
helpviewer_keywords:
- IEnumDebugReferenceInfo2::Next
ms.assetid: 70b31a57-1701-4757-9e7e-63ec60a71b3c
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 382587a351cebb7bb836759c1e6e994ea435057c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68147801"
---
# <a name="ienumdebugreferenceinfo2next"></a>IEnumDebugReferenceInfo2::Next
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

枚举中返回下一组元素。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Next(  
   ULONG                   celt,  
   DEBUG_REFERENCE_INFO ** rgelt,  
   ULONG*                  pceltFetched  
);  
```  
  
```csharp  
int Next(  
   uint                   celt,  
   DEBUG_REFERENCE_INFO[] rgelt,  
   ref uint               pceltFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 [in]要检索的元素数。 此外可以指定的最大大小`rgelt`数组。  
  
 `rgelt`  
 [in、 out]数组[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)要填充的元素。  
  
 `pceltFetched`  
 [out]返回中实际返回的元素数目`rgelt`。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果无法返回请求的元素数少于; 否则，返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)   
 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
