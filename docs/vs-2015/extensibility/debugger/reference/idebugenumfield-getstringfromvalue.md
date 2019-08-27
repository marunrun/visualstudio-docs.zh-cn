---
title: IDebugEnumField::GetStringFromValue |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetStringFromValue
helpviewer_keywords:
- IDebugEnumField::GetStringFromValue method
ms.assetid: 5f95fd0c-fdce-497f-9f54-2ad8749494e9
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ecdd60c363e30afbe4c61e8e18660a17a06a5ce8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68188995"
---
# <a name="idebugenumfieldgetstringfromvalue"></a>IDebugEnumField::GetStringFromValue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法获取给定其值的枚举常量的名称。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetStringFromValue(  
   ULONGLONG value,  
   BSTR*     pbstrValue  
);  
```  
  
```csharp  
int GetStringFromValue(  
   ulong      value,  
   out string pbstrValue  
);  
```  
  
#### <a name="parameters"></a>参数  
 `value`  
 [in]要为其获取枚举的名称的常量值。  
  
 `pbstrValue`  
 [out]返回的枚举常量的名称。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回`S_FALSE`如果的值没有关联的名称，或返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果有多个相同的值与关联的名称，将返回在枚举中定义的第一个名称。  
  
## <a name="see-also"></a>请参阅  
 [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
