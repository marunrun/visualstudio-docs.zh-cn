---
title: PARSEFLAGS | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- PARSEFLAGS
helpviewer_keywords:
- PARSEFLAGS enumeration
ms.assetid: 47943f0a-54cb-4493-a62e-5dba97bd4c35
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0a9ebe244f3e1c1f3f95508d6df979edee2d4aed
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205124"
---
# <a name="parseflags"></a>PARSEFLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定如何分析表达式。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_PARSEFLAGS {   
   PARSE_EXPRESSION            = 0x0001,  
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,  
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000  
};  
typedef DWORD PARSEFLAGS;  
```  
  
```csharp  
public enum enum_PARSEFLAGS {   
   PARSE_EXPRESSION            = 0x0001,  
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,  
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000  
};  
```  
  
## <a name="members"></a>成员  
 PARSE_EXPRESSION  
 指示该表达式不是一个语句。  
  
 PARSE_FUNCTION_AS_ADDRESS  
 指示表达式是以进行分析 （和更高版本评估） 地址。  
  
 PARSE_DESIGN_TIME_EXPR_EVAL  
 指示在设计时正在分析表达式 （即，设计器打开时）。  
  
## <a name="remarks"></a>备注  
 作为参数传递给[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)并[分析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)方法。  
  
## <a name="requirements"></a>要求  
 标头： msdbg.h  
  
 命名空间:Microsoft.VisualStudio.Debugger.Interop  
  
 程序集：Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>请参阅  
 [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)   
 [分析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
