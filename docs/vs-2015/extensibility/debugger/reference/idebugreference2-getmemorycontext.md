---
title: IDebugReference2::GetMemoryContext |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugReference2::GetMemoryContext
helpviewer_keywords:
- IDebugReference2::GetMemoryContext
ms.assetid: 47fc3827-07a0-4eee-b7f4-fc1c62e6b25c
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0d9f3aa8ef59997a326eeae54df1216d96508207
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202495"
---
# <a name="idebugreference2getmemorycontext"></a>IDebugReference2::GetMemoryContext
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取引用的内存上下文。 留待将来使用。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetMemoryContext (   
   IDebugMemoryContext2** ppMemory  
);  
```  
  
```csharp  
int GetMemoryContext (   
   out IDebugMemoryContext2 ppMemory  
);  
```  
  
#### <a name="parameters"></a>Parameters  
 `ppMemory`  
 [out]返回[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)对象，表示与引用的值相关联的内存。  
  
## <a name="return-value"></a>返回值  
 始终返回 `E_NOTIMPL`。  
  
## <a name="see-also"></a>请参阅  
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)   
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
