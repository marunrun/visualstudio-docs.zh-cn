---
title: IDebugCustomAttributeQuery2：： GetCustomAttributeByName |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
helpviewer_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
ms.assetid: 7428dfeb-8929-41b2-9b99-cb343a86c02d
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e1af059cf4319c18b8f8bb63e7b50ec3d2822e93
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62568429"
---
# <a name="idebugcustomattributequery2getcustomattributebyname"></a>IDebugCustomAttributeQuery2::GetCustomAttributeByName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

给定自定义属性的名称，获取自定义属性字节。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetCustomAttributeByName(   
   LPCOLESTR pszCustomAttributeName,  
   BYTE*     ppBlob,  
   DWORD*    pdwLen  
);  
```  
  
```csharp  
int GetCustomAttributeByName(  
   [In] string        pszCustomAttributeName,   
   [In, Out] byte[]   ppBlob,   
   [In, Out] ref uint pdwLen  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszCustomAttributeName`  
 中一个字符串，其中包含要查找的自定义特性的名称。  
  
 `ppBlob`  
 [in，out]使用自定义属性字节填充的数组。  
  
 `pdwLen`  
 [in，out]指定要在数组中返回的最大字节数 `ppBlob` ，并返回实际写入到数组中的字节数。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK 或返回 S_FALSE （如果自定义特性不存在）。 否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 将 `ppBlob` 参数设置为 null 值，以返回可用的属性字节数。 然后，分配一个数组，然后将该数组传递给中的 `ppBlob` 参数。  
  
 属性 bytes 表示自定义属性的原始数据。  
  
 如果 `ppBlob` 将和 `pdwLen` 参数设置为 null 值，则可以使用此方法来确定自定义属性是否只存在。 但更简单的方法是调用 [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md) 方法。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)   
 [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)
