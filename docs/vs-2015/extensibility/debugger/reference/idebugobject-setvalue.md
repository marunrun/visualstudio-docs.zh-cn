---
title: IDebugObject::SetValue |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject::SetValue
helpviewer_keywords:
- IDebugObject::SetValue method
ms.assetid: d652e09c-cdc1-4519-8116-d7c743f5679b
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a7d898852c6bcca42cb0df1e7fab1597df74427a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203263"
---
# <a name="idebugobjectsetvalue"></a>IDebugObject::SetValue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

设置对象的值从一系列连续的字节数。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT SetValue(   
   BYTE* pValue,  
   UINT  nSize  
);  
```  
  
```csharp  
int SetValue(  
   byte[] pValue,   
   uint   nSize  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `pValue`  
 [in]一个表示新值的字节数组。  
  
 `nSize`  
 [in]以字节为单位的值的大小。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK;否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 数组中的值复制到此[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)对象，并将任何现有值替换。 新值的大小可大于或小于现有值。 这`IDebugObject`不能为 null 引用。  
  
## <a name="see-also"></a>请参阅  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
