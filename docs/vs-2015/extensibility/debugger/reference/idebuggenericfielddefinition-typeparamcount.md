---
title: IDebugGenericFieldDefinition：： TypeParamCount |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- TypeParamCount
- IDebugGenericFieldDefinition::TypeParamCount
ms.assetid: d41dd5ea-aa25-4bf3-bcfd-e0bf451ead49
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6459b7b6d1297085b7311e8e7ae20dbfa9c0f366
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180883"
---
# <a name="idebuggenericfielddefinitiontypeparamcount"></a>IDebugGenericFieldDefinition::TypeParamCount
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索与泛型字段关联的类型参数的数目。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT TypeParamCount(  
   ULONG32* pcParams  
);  
```  
  
```csharp  
int TypeParamCount(  
   ref uint pcParams  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pcParams`  
 [in，out]类型参数的数目。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果为 List \<T> ，则此方法返回 1; 如果为 list \<T1,T2> ，则此方法返回2。 如果没有类型参数，则此方法返回0。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugGenericFieldDefinition](../../../extensibility/debugger/reference/idebuggenericfielddefinition.md)
