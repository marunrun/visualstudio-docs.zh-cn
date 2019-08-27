---
title: IDebugParsedExpression::EvaluateSync | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugParsedExpression::EvaluateSync
helpviewer_keywords:
- IDebugParsedExpression::EvaluateSync method
ms.assetid: 0ea04cfa-de87-4b6c-897e-4572c1a28942
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6761cd5ec9df67d511ab905e173ac0f286c5ee7d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194549"
---
# <a name="idebugparsedexpressionevaluatesync"></a>IDebugParsedExpression::EvaluateSync
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法分析的表达式的计算结果并根据需要将结果转换为另一种数据类型。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT EvaluateSync(   
   DWORD                 dwEvalFlags,  
   DWORD                 dwTimeout,  
   IDebugSymbolProvider* pSymbolProvider,  
   IDebugAddress*        pAddress,  
   IDebugBinder*         pBinder,  
   BSTR                  bstrResultType,  
   IDebugProperty2**     ppResult  
);  
```  
  
```csharp  
int EvaluateSync(  
   uint                 dwEvalFlags,   
   uint                 dwTimeout,   
   IDebugSymbolProvider pSymbolProvider,   
   IDebugAddress        pAddress,   
   IDebugBinder         pBinder,   
   string               bstrResultType,   
   out IDebugProperty2  ppResult  
);  
```  
  
#### <a name="parameters"></a>参数  
 `dwEvalFlags`  
 [in]组合[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)控制如何计算该表达式的常量。  
  
 `dwTimeout`  
 [in]指定以毫秒为单位，此方法返回前等待的最长时间。 使用`INFINITE`无限期等待。  
  
 `pSymbolProvider`  
 [in]符号提供程序，以表示[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)接口。  
  
 `pAddress`  
 [in]在方法中，以表示当前执行位置[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)接口。  
  
 `pBinder`  
 [in]联编程序，以表示[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)接口。  
  
 `bstrResultType`  
 [in]应转换结果的类型。 此参数可以为 null 值。  
  
 `ppResult`  
 [out]返回[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)表示计算的结果的接口。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 由给定表达式的计算上下文`pAddress`，从而无法确定包含方法，然后使用语言范围规则来确定在表达式中的符号的值。  
  
## <a name="see-also"></a>请参阅  
 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)   
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
