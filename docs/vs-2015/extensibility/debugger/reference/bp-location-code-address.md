---
title: BP_LOCATION_CODE_ADDRESS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_ADDRESS
helpviewer_keywords:
- BP_LOCATION_CODE_ADDRESS structure
ms.assetid: 83c9da8b-19d9-4be5-b225-854543654901
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b23073c41f5da7d1563a6be46e0d114334527b35
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153517"
---
# <a name="bp_location_code_address"></a>BP_LOCATION_CODE_ADDRESS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

描述代码中某个地址处的断点位置。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct _BP_LOCATION_CODE_ADDRESS {   
   BSTR bstrContext;  
   BSTR bstrModuleUrl;  
   BSTR bstrFunction;  
   BSTR bstrAddress;  
} BP_LOCATION_CODE_ADDRESS;  
```  
  
## <a name="members"></a>成员  
 `bstrContext`  
 断点的上下文，通常是在调用堆栈上显示的方法或函数名称。  
  
 `bstrModuleUrl`  
 包含断点的模块的 URL。  
  
 `bstrFunction`  
 包含断点的函数的名称。  
  
 `bstrAddress`  
 断点的地址，表达式计算器会分析该地址，以将其绑定到 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象。  
  
## <a name="remarks"></a>备注  
 此结构是作为联合的一部分的 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md) 结构的成员。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
