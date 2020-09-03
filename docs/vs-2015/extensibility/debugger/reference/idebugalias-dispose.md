---
title: IDebugAlias：:D ispose |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugAlias::Dispose
helpviewer_keywords:
- IDebugAlias::Dispose method
ms.assetid: e84909a4-d378-4f48-bf25-2c014c77c8e3
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 082398c9a8718b5814c417b9e3d3393de91f0ffb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68206056"
---
# <a name="idebugaliasdispose"></a>IDebugAlias::Dispose
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

将此别名标记为删除。  
  
## <a name="syntax"></a>语法  
  
```cpp  
HRESULT Dispose();  
```  
  
```csharp  
int Dispose();  
```  
  
#### <a name="parameters"></a>参数  
 无。  
  
## <a name="return-value"></a>返回值  
 如果成功，将返回 S_OK;否则，将返回错误代码。  
  
## <a name="remarks"></a>备注  
 调用此方法后，该别名将不再可用。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
