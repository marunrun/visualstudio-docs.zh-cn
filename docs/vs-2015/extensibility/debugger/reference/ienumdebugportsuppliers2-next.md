---
title: IEnumDebugPortSuppliers2：： Next |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugPortSuppliers2::Next
helpviewer_keywords:
- IEnumDebugPortSuppliers2::Next
ms.assetid: e2a2d226-e70b-42c2-bf00-a936517940c8
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0a2e887c6e00587c4101c73c9cc6b5bdd0a47789
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68164710"
---
# <a name="ienumdebugportsuppliers2next"></a>IEnumDebugPortSuppliers2::Next
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

返回枚举中的下一个元素集。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Next(  
   ULONG                 celt,  
   IDebugPortSupplier2** rgelt,  
   ULONG*                pceltFetched  
);  
```  
  
```csharp  
int Next(  
   uint                  celt,  
   IDebugPortSupplier2[] rgelt,  
   ref uint              pceltFetched  
);  
```  
  
#### <a name="parameters"></a>参数  
 `celt`  
 中要检索的元素的数目。 还指定数组的最大大小 `rgelt` 。  
  
 `rgelt`  
 [in，out]要填充的 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md) 元素的数组。  
  
 `pceltFetched`  
 弄返回中实际返回的元素数 `rgelt` 。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 `S_OK`。 `S_FALSE`如果返回的元素数少于所请求的数目，则返回; 否则返回错误代码。  
  
## <a name="see-also"></a>另请参阅  
 [IEnumDebugPortSuppliers2](../../../extensibility/debugger/reference/ienumdebugportsuppliers2.md)   
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
