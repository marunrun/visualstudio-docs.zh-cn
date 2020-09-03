---
title: EVALFLAGS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- EVALFLAGS
helpviewer_keywords:
- EVALFLAGS enumeration
ms.assetid: 7b2cb14a-511a-4fef-9e4f-308139719fba
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9e6ee00402c13b2a79e4e6757a127211eda9c3c0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68149387"
---
# <a name="evalflags"></a>EVALFLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定控制表达式计算的标志。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
enum enum_EVALFLAGS {  
   EVAL_RETURNVALUE = 0x0002,  
   EVAL_NOSIDEEFFECTS = 0x0004,  
   EVAL_ALLOWBPS = 0x0008,  
   EVAL_ALLOWERRORREPORT = 0x0010,  
   EVAL_FUNCTION_AS_ADDRESS = 0x0040,  
   EVAL_NOFUNCEVAL = 0x0080,  
   EVAL_NOEVENTS = 0x1000  
};  
typedef DWORD EVALFLAGS;  
```  
  
```csharp  
public enum enum_EVALFLAGS {  
   EVAL_RETURNVALUE = 0x0002,  
   EVAL_NOSIDEEFFECTS = 0x0004,  
   EVAL_ALLOWBPS = 0x0008,  
   EVAL_ALLOWERRORREPORT = 0x0010,  
   EVAL_FUNCTION_AS_ADDRESS = 0x0040,  
   EVAL_NOFUNCEVAL = 0x0080,  
   EVAL_NOEVENTS = 0x1000  
}  
```  
  
## <a name="members"></a>成员  
 EVAL_RETURNVALUE  
 指定将计算返回值（如果有）。  
  
 EVAL_NOSIDEEFFECTS  
 指定不允许副作用。  
  
 EVAL_ALLOWBPS  
 指定在断点处停止。  
  
 EVAL_ALLOWERRORREPORT  
 指定将错误报告给允许的主机。 主要用于 Internet Explorer 中的脚本中的表达式计算。  
  
 EVAL_FUNCTION_AS_ADDRESS  
 强制将函数作为地址进行计算，而不是调用函数。  
  
 EVAL_NOFUNCEVAL  
 禁止计算函数。 例如，请考虑 `int` 表达式中的标记 `myExpression(int) + 10` 。 此函数可以正确地作为地址进行计算，但不能作为值来计算。  
  
 EVAL_NOEVENTS  
 一个标志，用于指示在表达式计算过程中发生的事件不应发送到会话调试管理器 (SDM) 或 IDE。  
  
## <a name="remarks"></a>备注  
 这些标志作为参数传递给 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md) 和 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) 方法。  
  
 这些标志可以与按位 "或" 组合在一起。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>另请参阅  
 [计数](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)   
 [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
