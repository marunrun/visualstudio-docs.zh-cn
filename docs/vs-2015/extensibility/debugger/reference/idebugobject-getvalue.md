---
title: IDebugObject::GetValue |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject::GetValue
helpviewer_keywords:
- IDebugObject::GetValue method
ms.assetid: eec6051e-8ecb-49fa-bdd4-dd786f211692
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: de6e6888cfce338ebcee90e722f07e900ce25d0b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180536"
---
# <a name="idebugobjectgetvalue"></a>IDebugObject::GetValue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取对象的值作为一系列连续的字节数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetValue(   
   BYTE* pValue,  
   UINT  nSize  
);  
```  
  
```csharp  
int GetValue(  
   ref byte[] pValue,   
   uint nSize  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pValue`  
 [in、 out]使用一系列连续的字节数表示的对象的值填充数组。  
  
 `nSize`  
 [in]要提取的字节数目上限。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK;否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 获取可以通过调用提取的值字节总数[GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
