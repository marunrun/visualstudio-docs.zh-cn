---
title: IDebugArrayField：： GetRank |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetRank
helpviewer_keywords:
- IDebugArrayField::GetRank method
ms.assetid: 2364b876-5be1-4bab-9b8f-3b6121da35c6
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5d0396718482c9ce90527155a3612160612f66d3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198733"
---
# <a name="idebugarrayfieldgetrank"></a>IDebugArrayField::GetRank
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取数组的秩或维度数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetRank(   
   DWORD* pdwRank  
);  
```  
  
```csharp  
int GetRank(  
   out uint pdwRank  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pdwRank`  
 弄返回秩。  
  
## <a name="return-value"></a>返回值  
 如果成功，将返回 S_OK;否则，将返回错误代码。  
  
## <a name="remarks"></a>备注  
 数组的秩对应于维数。 在 c + + 和 c # 中，多维数组实际上是数组的数组，因此可以只将一维数组视为 (并且 `GetRank` 方法始终返回 1) 。 另一方面，在中， [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 多维数组的处理方式不同，此类数组的秩反映 (的维数， `GetRank` 方法始终返回) 的维度数。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)
