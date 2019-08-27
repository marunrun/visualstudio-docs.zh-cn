---
title: IDebugProperty2::SetValueAsReference |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsReference
helpviewer_keywords:
- IDebugProperty2::SetValueAsReference method
ms.assetid: 341b1b89-4ab8-4e1c-abe2-fb955df5c6b0
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a94e3767ee05e39e847af27dc5999fa8bbbe2d44
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193451"
---
# <a name="idebugproperty2setvalueasreference"></a>IDebugProperty2::SetValueAsReference
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将此属性的值设置为给定引用的值。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT SetValueAsReference(  
   IDebugReference2** rgpArgs,  
   DWORD              dwArgCount,  
   IDebugReference2*  pValue,  
   DWORD              dwTimeout  
);  
```  
  
```csharp  
int SetValueAsReference(  
   IDebugReference2[] rgpArgs,  
   uint               dwArgCount,  
   IDebugReference2   pValue,  
   uint               dwTimeout  
);  
```  
  
#### <a name="parameters"></a>参数  
 `rgpArgs`  
 [in]要传递给托管的代码属性 setter 参数的数组。 如果属性 setter 不采用自变量，或如果此[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)对象不是此类属性 setter，指`rgpArgs`应为 null 值。 此参数通常是一个 null 值。  
  
 `dwArgCount`  
 [in]中的参数数目`rgpArgs`数组。  
  
 `pValue`  
 [in]中的窗体的引用[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)对象，用于设置此属性的值。  
  
 `dwTimeout`  
 [in]需要设置值，以毫秒为单位的时间。 典型值为`INFINITE`。 这会影响任何可能的评估需要花费的时间的长度。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码，通常下列项之一：  
  
|Error|描述|  
|-----------|-----------------|  
|`E_SETVALUEASREFERENCE_NOTSUPPORTED`|不支持从引用设置值。|  
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|无法设置值，因为此属性是指一种方法。|  
|`E_SETVALUE_VALUE_IS_READONLY`|值是只读的不能设置。|  
|`E_NOTIMPL`|未实现方法。|  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
