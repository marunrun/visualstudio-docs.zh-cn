---
title: IDebugBinder::GetMemoryContext | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBinder::GetMemoryContext
helpviewer_keywords:
- IDebugBinder::GetMemoryContext method
ms.assetid: 801c5b60-acff-4822-b23d-e9c7bbca8a0f
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: db8d8d820c43d17194feda0bf228227a279dccc6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62423408"
---
# <a name="idebugbindergetmemorycontext"></a>IDebugBinder::GetMemoryContext
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法将转换为内存上下文的对象位置或内存地址。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetMemoryContext(   
   IDebugField*           pField,  
   DWORD                  dwConstant,  
   IDebugMemoryContext2** ppMemCxt  
);  
```  
  
```csharp  
int GetMemoryContext(  
   IDebugField              pField,   
   uint                     dwConstant,   
   out IDebugMemoryContext2 ppMemCxt  
);  
```  
  
#### <a name="parameters"></a>参数  
 `pField`  
 [in][IDebugField](../../../extensibility/debugger/reference/idebugfield.md)描述要查找的对象。 如果`NULL`，然后使用`dwConstant`相反。  
  
 `dwConstant`  
 [in]常量的内存地址，例如 0x5000。  
  
 `ppMemCxt`  
 [out]返回[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)表示的地址对象或在内存中的地址的接口。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="see-also"></a>请参阅  
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)   
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
