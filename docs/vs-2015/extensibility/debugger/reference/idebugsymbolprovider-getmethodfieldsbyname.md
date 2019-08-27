---
title: IDebugSymbolProvider::GetMethodFieldsByName | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetMethodFieldsByName
helpviewer_keywords:
- IDebugSymbolProvider::GetMethodFieldsByName method
ms.assetid: 1f781320-81ef-4037-b068-f1864b271258
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: eb26d7382c9c501a1c3235153c2364b2a3e677fb
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62421156"
---
# <a name="idebugsymbolprovidergetmethodfieldsbyname"></a>IDebugSymbolProvider::GetMethodFieldsByName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法获取表示完全限定的方法名称的字段。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetMethodFieldsByName(   
   LPCOLESTR          pszFullName,  
   NAME_MATCH         nameMatch,  
   IEnumDebugFields** ppEnum  
);  
```  
  
```csharp  
int GetMethodFieldsByName(  
   string               pszFullName,   
   NAME_MATCH           nameMatch,   
   out IEnumDebugFields ppEnum  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pszFullName`  
 [in]方法名称。  
  
 `nameMatch`  
 [in]选择区分大小写的匹配项，例如，类型。  
  
 `ppEnum`  
 [out]返回[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)与此方法关联的字段的枚举器。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 如果它重载函数，例如，一种方法可以具有多个字段相关联。  
  
## <a name="see-also"></a>请参阅  
 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
