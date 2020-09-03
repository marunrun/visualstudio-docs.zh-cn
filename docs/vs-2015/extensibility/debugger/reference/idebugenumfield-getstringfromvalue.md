---
title: IDebugEnumField：： GetStringFromValue |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
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
 中要为其获取枚举常量名称的值。  
  
 `pbstrValue`  
 弄返回枚举常量的名称。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则， `S_FALSE` 如果值没有关联的名称，则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果有多个与同一值关联的名称，则将返回在枚举中定义的第一个名称。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
