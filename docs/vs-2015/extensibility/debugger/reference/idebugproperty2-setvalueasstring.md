---
title: IDebugProperty2::SetValueAsString |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProperty2::SetValueAsString
helpviewer_keywords:
- IDebugProperty2::SetValueAsString
ms.assetid: 9e6a5054-41b7-4223-b509-b93689d366a5
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d50057570b5b067447321f975d4d33da8aa3de43
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193436"
---
# <a name="idebugproperty2setvalueasstring"></a>IDebugProperty2::SetValueAsString
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

从给定字符串中设置属性的值。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT SetValueAsString (   
   LPCOLESTR pszValue,  
   UINT      nRadix,  
   DWORD     dwTimeout  
);  
```  
  
```csharp  
int SetValueAsString (   
   string pszValue,  
   uint   nRadix,  
   uint   dwTimeout  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszValue`  
 [in]包含要设置的值的字符串。  
  
 `nRadix`  
 [in]用于解释任何数字信息的基数。 这可以是 0，以尝试自动确定基数。  
  
 `dwTimeout`  
 [in]指定以毫秒为单位，此方法返回前等待的最长时间。 使用`INFINITE`无限期等待。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则返回错误代码。 下表显示了其他可能的值。  
  
|值|描述|  
|-----------|-----------------|  
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|字符串可以转换为属性值，或无法设置属性值。|  
|`E_SETVALUE_VALUE_IS_READONLY`|该属性是只读的。|  
  
## <a name="see-also"></a>请参阅  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
