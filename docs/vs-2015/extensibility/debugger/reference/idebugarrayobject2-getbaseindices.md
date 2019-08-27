---
title: IDebugArrayObject2::GetBaseIndices | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- GetBaseIndices
- IDebugArrayObject2::GetBaseIndices
ms.assetid: 882951a2-3da0-49bf-8d1e-7daedd13ffe6
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3c10fb65ec698bf9c5c9b7623b29e2f47851afe8
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62423594"
---
# <a name="idebugarrayobject2getbaseindices"></a>IDebugArrayObject2::GetBaseIndices
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索给定数组中的维度数的每个索引 （下限） 的基索引。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetBaseIndices (  
   DWORD  dwRank,  
   DWORD* dwIndices  
);  
```  
  
```csharp  
int GetBaseIndices (  
   uint       dwRank,  
   out uint[] dwIndices  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwRank`  
 [in]数组的维数 （秩） 数。  
  
 `dwIndices`  
 [out]数组基索引 （下限）。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 例如，此函数将返回"5"的下面的 C# 代码创建的数组：  
  
```  
int[] lengths = { 12 };  
int[] lowerbounds = { 5 };  
Array.CreateInstance(typeof(int), lengths, lowerbounds);  
```  
  
## <a name="see-also"></a>请参阅  
 [IDebugArrayObject2](../../../extensibility/debugger/reference/idebugarrayobject2.md)
