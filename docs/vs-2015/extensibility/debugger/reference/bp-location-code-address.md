---
title: BP_LOCATION_CODE_ADDRESS | Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153517"
---
# <a name="bplocationcodeaddress"></a>BP_LOCATION_CODE_ADDRESS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

描述在代码中的一个地址断点的位置。  
  
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
 该断点的上下文，通常显示调用堆栈上的方法或函数名称。  
  
 `bstrModuleUrl`  
 包含断点的模块的 URL。  
  
 `bstrFunction`  
 包含断点的函数的名称。  
  
 `bstrAddress`  
 所需断点，以将其绑定到的表达式计算器通过分析它的地址[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象。  
  
## <a name="remarks"></a>备注  
 此结构是的成员[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构作为联合的一部分。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
