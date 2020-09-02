---
title: IDebugProperty2：： SetValueAsString |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193436"
---
# <a name="idebugproperty2setvalueasstring"></a>IDebugProperty2::SetValueAsString
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

设置给定字符串的属性的值。  
  
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
 中包含要设置的值的字符串。  
  
 `nRadix`  
 中用于解释任何数值信息的基数。 这可以是0，尝试自动确定基数。  
  
 `dwTimeout`  
 中指定从此方法返回之前要等待的最长时间（以毫秒为单位）。 使用 `INFINITE` 无限期等待。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。 下表显示了其他可能的值。  
  
|值|说明|  
|-----------|-----------------|  
|`E_SETVALUE_VALUE_CANNOT_BE_SET`|无法将该字符串转换为属性值，或者无法设置该属性的值。|  
|`E_SETVALUE_VALUE_IS_READONLY`|属性为只读属性。|  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
