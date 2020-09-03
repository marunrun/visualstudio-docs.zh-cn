---
title: IDebugAlias：： GetICorDebugValue |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68156282"
---
# <a name="idebugaliasgeticordebugvalue"></a>IDebugAlias::GetICorDebugValue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

检索表示与此别名关联的值的托管代码接口。  
  
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
  
#### <a name="parameters"></a>参数  
 `ppUnk`  
 [out] `IUnknown` 表示与此别名关联的值的接口。 可以查询此接口的接口 `ICorDebugValue` 。  
  
## <a name="return-value"></a>返回值  
 如果成功，将返回 S_OK;否则，将返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法仅适用于托管的值 (`ICorDebugValue` 是中可用的接口 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ，并且在 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK 中的 cordebug.idl 文件) 中定义。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
