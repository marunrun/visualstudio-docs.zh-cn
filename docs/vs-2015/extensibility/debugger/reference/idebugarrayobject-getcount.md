---
title: 'IDebugArrayObject:: GetCount |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetCount
helpviewer_keywords:
- IDebugArrayObject::GetCount method
ms.assetid: 7931f3f7-033c-4bf8-8abd-95183952ebb0
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 35cce37afc389501386ffec7b75b934e7933bc98
ms.sourcegitcommit: 9cfd3ef6c65f671a26322320818212a1ed5955fe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68197792"
---
# <a name="idebugarrayobjectgetcount"></a>IDebugArrayObject::GetCount
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取数组中元素的计数。  
  
## <a name="syntax"></a>语法  
  
```  
[C++]  
HRESULT GetCount(   
   DWORD* pdwElements  
);  
```  
  
```  
[C#]  
int GetCount(  
   out uint pdwElements  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdwElements`  
 弄返回计数。  
  
## <a name="return-value"></a>返回值  
 如果成功, 则返回 S_OK;否则, 将返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法将数组对象的所有元素视为一维数组, 即使数组对象是多维的。 例如, 给定数组`myarray[3][2][6]`, 此方法将`pdwElements`在参数中返回36。 使用[GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)方法每次检索一个元素。  
  
## <a name="see-also"></a>请参阅  
 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
