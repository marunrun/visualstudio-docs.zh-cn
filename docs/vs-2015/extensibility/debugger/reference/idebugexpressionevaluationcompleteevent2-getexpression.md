---
title: IDebugExpressionEvaluationCompleteEvent2::GetExpression |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluationCompleteEvent2::GetExpression
helpviewer_keywords:
- IDebugExpressionEvaluationCompleteEvent2::GetExpression
ms.assetid: faf6b2dd-2afd-4852-b21c-7e8d3130e141
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9f33c374d8aa4087ca90d7c2a4fa1d26f9a0842b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68148747"
---
# <a name="idebugexpressionevaluationcompleteevent2getexpression"></a>IDebugExpressionEvaluationCompleteEvent2::GetExpression
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

获取原始表达式。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetExpression(   
   IDebugExpression2** ppExpr  
);  
```  
  
```csharp  
int GetExpression(   
   out IDebugExpression2 ppExpr  
);  
```  
  
#### <a name="parameters"></a>参数  
 `ppExpr`  
 [out]返回[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)对象，表示已分析的表达式。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法返回的调用中创建的对象[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)方法。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExpressionEvaluationCompleteEvent2](../../../extensibility/debugger/reference/idebugexpressionevaluationcompleteevent2.md)   
 [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)   
 [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
