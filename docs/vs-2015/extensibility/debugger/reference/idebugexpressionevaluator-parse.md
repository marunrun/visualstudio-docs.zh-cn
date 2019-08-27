---
title: IDebugExpressionEvaluator::Parse |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::Parse
helpviewer_keywords:
- IDebugExpressionEvaluator::Parse method
ms.assetid: e6e31b3a-63a7-4293-bcda-267eb78dffb6
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4039534b139eeeaf20f938c6d6c358c602f96227
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68155345"
---
# <a name="idebugexpressionevaluatorparse"></a>IDebugExpressionEvaluator::Parse
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法将一个表达式字符串转换为已分析的表达式。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT Parse(   
   LPCOLESTR                upstrExpression,  
   PARSEFLAGS               dwFlags,  
   UINT                     nRadix,  
   BSTR*                    pbstrError,  
   UINT*                    pichError,  
   IDebugParsedExpression** ppParsedExpression  
);  
```  
  
```csharp  
int Parse(  
   string                     upstrExpression,   
   enum_PARSEFLAGS            dwFlags,   
   uint                       nRadix,   
   out string                 pbstrError,   
   out uint                   pichError,   
   out IDebugParsedExpression ppParsedExpression  
);  
```  
  
#### <a name="parameters"></a>参数  
 `upstrExpression`  
 [in]要分析的表达式字符串。  
  
 `dwFlags`  
 [in]一系列[PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)确定表达式的分析方式的常量。  
  
 `nRadix`  
 [in]要用来解释任何数字信息的基数。  
  
 `pbstrError`  
 [out]以用户可读文本形式将返回错误。  
  
 `pichError`  
 [out]返回错误的起始字符的位置中的表达式字符串。  
  
 `ppParsedExpression`  
 [out]返回中的已分析的表达式[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)对象。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 此方法生成的已分析的表达式不是一个实际值。 已分析的表达式是可供计算，即，转换为值。  
  
## <a name="see-also"></a>请参阅  
 [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)   
 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)   
 [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)
