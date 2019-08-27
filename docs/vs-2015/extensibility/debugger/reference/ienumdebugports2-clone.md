---
title: IEnumDebugPorts2::Clone |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugPorts2::Clone
helpviewer_keywords:
- IEnumDebugPorts2::Clone
ms.assetid: d5ce77e8-bb99-409a-98fa-20fe5a0de25e
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8216882286bc1521043bfb8aafe3aa4ea588a8d3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180447"
---
# <a name="ienumdebugports2clone"></a>IEnumDebugPorts2::Clone
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

返回当前枚举作为一个单独的对象的副本。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Clone(  
   IEnumDebugPorts2** ppEnum  
);  
```  
  
```csharp  
int Clone(  
   out IEnumDebugPorts2 ppEnum  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppEnum`  
 [out]返回此枚举作为一个单独的对象的副本。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 枚举的副本在调用此方法时都具有与原始相同的状态。 但是，该副本的和原始的状态是独立的并且可以单独更改。  
  
## <a name="see-also"></a>请参阅  
 [IEnumDebugPorts2](../../../extensibility/debugger/reference/ienumdebugports2.md)
