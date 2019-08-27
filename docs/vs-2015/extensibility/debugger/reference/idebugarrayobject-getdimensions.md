---
title: 'IDebugArrayObject:: GetDimensions |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetDimensions
helpviewer_keywords:
- IDebugArrayObject::GetDimensions method
ms.assetid: 113e0aff-9028-49d6-b104-9fe7be4772d7
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 09902c60f87cfb92d0f0778fcbd106ade4d8dac4
ms.sourcegitcommit: 9cfd3ef6c65f671a26322320818212a1ed5955fe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/26/2019
ms.locfileid: "68197777"
---
# <a name="idebugarrayobjectgetdimensions"></a>IDebugArrayObject::GetDimensions
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取数组的尺寸。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetDimensions(   
   DWORD dwCount,  
   DWORD dwDimensions[]  
);  
```  
  
```csharp  
int GetDimensions(  
   [In] uint    dwCount,   
   [Out] uint[] dwDimensions  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwCount`  
 中要检索的维度数。  
  
 `dwDimensions`  
 [in, out]用每个维度的大小填充的数组。 `dwCount`指定`dwDimensions`数组的最大大小。  
  
## <a name="return-value"></a>返回值  
 如果成功, 则返回 S_OK;否则, 将返回错误代码。  
  
## <a name="remarks"></a>备注  
 多维数组每个维度的大小可以不同。 例如, 假设有一个三维数组`myarray[3][2][6]`, 则`dwDimensions`此方法会在参数中按顺序返回3、2和6。  
  
## <a name="see-also"></a>请参阅  
 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
