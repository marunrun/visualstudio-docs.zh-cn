---
title: IDebugObject：： GetManagedDebugObject |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject::GetManagedDebugObject
helpviewer_keywords:
- IDebugObject::GetManagedDebugObject method
ms.assetid: cb89692e-7657-47ff-846d-311943521951
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4f2917135f5e25648cf08cd9030e3fdf31aedb52
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68162475"
---
# <a name="idebugobjectgetmanageddebugobject"></a>IDebugObject::GetManagedDebugObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

在调试引擎的地址空间中创建托管对象的副本。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetManagedDebugObject(   
   IDebugManagedObject** ppObject  
);  
```  
  
```csharp  
int GetManagedDebugObject(  
   out IDebugManagedObject ppObject  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppObject`  
 弄返回表示新创建的托管对象的 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) 对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，将返回 S_OK;否则，将返回错误代码。 如果此 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 不表示托管值类实例，则返回 E_FAIL。  
  
## <a name="remarks"></a>备注  
 此 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) 对象必须表示托管值类实例，如 `System.Decimal` 实例。 通过使用本地副本，可消除调用 [计算](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) 的开销。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
