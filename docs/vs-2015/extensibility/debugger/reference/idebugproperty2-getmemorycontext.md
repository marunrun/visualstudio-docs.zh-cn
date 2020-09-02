---
title: IDebugProperty2：： GetMemoryContext |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetMemoryContext
helpviewer_keywords:
- IDebugProperty2::GetMemoryContext
ms.assetid: 91793d25-790f-4881-a5c0-d0458e534514
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a3ad83bfe36f468dd0e2d7d040c188fd69970a82
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193487"
---
# <a name="idebugproperty2getmemorycontext"></a>IDebugProperty2::GetMemoryContext
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取属性值的内存上下文。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetMemoryContext (   
   IDebugMemoryContext2** ppMemory  
);  
```  
  
```csharp  
int GetMemoryContext(  
   out IDebugMemoryContext2 ppMemory  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppMemory`  
 弄返回 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) 对象，该对象表示与此属性关联的内存。  
  
## <a name="return-value"></a>返回值  
 如果成功， `S_OK` 则返回; 否则返回错误代码。 `S_GETMEMORYCONTEXT_NO_MEMORY_CONTEXT`如果没有要检索的内存上下文，则返回。  
  
## <a name="see-also"></a>另请参阅  
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
