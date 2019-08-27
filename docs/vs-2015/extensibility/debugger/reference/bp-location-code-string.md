---
title: BP_LOCATION_CODE_STRING |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION_CODE_STRING
helpviewer_keywords:
- BP_LOCATION_CODE_STRING structure
ms.assetid: a4cd71c6-5052-45fe-907b-ebc6ca1df2e4
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 50c48098aee3b1077edec99210e7ab624d2a8d6c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68153453"
---
# <a name="bplocationcodestring"></a>BP_LOCATION_CODE_STRING
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

用于设置基于用户可以从集成的开发环境 (IDE) 中输入的字符串的代码断点。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
typedef struct _BP_LOCATION_CODE_STRING {   
   BSTR bstrContext;  
   BSTR bstrCodeExpr;  
} BP_LOCATION_CODE_STRING;  
```  
  
## <a name="members"></a>成员  
 `bstrContext`  
 在代码内的断点，通常显示调用堆栈上的方法或函数名称的上下文。  
  
 `bstrCodeExpr`  
 在用户键入来描述代码断点字符串。  
  
## <a name="remarks"></a>备注  
 此结构是的成员[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构作为联合的一部分。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
