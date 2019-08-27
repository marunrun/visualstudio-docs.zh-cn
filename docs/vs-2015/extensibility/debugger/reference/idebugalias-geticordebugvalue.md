---
title: IDebugAlias::GetICorDebugValue |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugAlias::GetICorDebugValue
helpviewer_keywords:
- IDebugAlias::GetICorDebugValue method
ms.assetid: b9eb39ee-84af-4ace-9cfe-236b3d48aff5
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 67ab8a7343cd320470515b757dfca905a0a4690e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68156282"
---
# <a name="idebugaliasgeticordebugvalue"></a>IDebugAlias::GetICorDebugValue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索表示与此别名关联的值的托管的代码接口。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT GetICorDebugValue(  
   IUnknown** ppUnk  
);  
```  
  
```csharp  
int GetICorDebugValue(  
   out object ppUnk  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppUnk`  
 [out]`IUnknown`接口，表示与此别名关联的值。 此接口可以查询有关`ICorDebugValue`接口。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回 S_OK;否则，返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法仅适用于托管值 (`ICorDebugValue`是一个接口中可用[!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]中定义， [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] cordebug.idl 文件中的 SDK)。  
  
## <a name="see-also"></a>请参阅  
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
