---
title: IDebugExpressionEvaluator::GetMethodLocationProperty |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodLocationProperty method
ms.assetid: 52c42a2e-f144-476b-8bef-442464c8fe8e
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d82b002d9253b2d48f78e74fdf964cf42d241d9a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68144391"
---
# <a name="idebugexpressionevaluatorgetmethodlocationproperty"></a>IDebugExpressionEvaluator::GetMethodLocationProperty
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此方法转换为方法位置和偏移量的内存地址。  
  
## <a name="syntax"></a>语法  
  
```cpp#  
HRESULT GetMethodLocationProperty(   
   LPCOLESTR             upstrFullyQualifiedMethodPlusOffset,  
   IDebugSymbolProvider* pSymbolProvider,  
   IDebugAddress*        pAddress,  
   IDebugBinder*         pBinder,  
   IDebugProperty2**     ppProperty  
);  
```  
  
```csharp  
int GetMethodLocationProperty(  
   string               upstrFullyQualifiedMethodPlusOffset,   
   IDebugSymbolProvider pSymbolProvider,   
   IDebugAddress        pAddress,   
   IDebugBinder         pBinder,   
   out IDebugProperty2  ppProperty  
);  
```  
  
#### <a name="parameters"></a>参数  
 `upstrFullyQualifiedMethodPlusOffset`  
 [in]方法的位置和偏移量，表示为字符串。  
  
 `pSymbolProvider`  
 [in]符号提供程序以表示[IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)对象。  
  
 `pAddress`  
 [in]在方法中，表示为一个地址[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象。  
  
 `pBinder`  
 [in]此联编程序表示为[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)对象。  
  
 `ppProperty`  
 [out]返回[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)表示的内存地址的接口。  
  
## <a name="return-value"></a>返回值  
 如果成功，则返回`S_OK`; 否则为返回错误代码。  
  
## <a name="remarks"></a>备注  
 返回的地址可以用于设置断点，例如。  
  
 不管名称如何`upstrFullyQualifiedMethodPlusOffset`，此参数可以传递部分限定的方法名称。 在这种情况下，所选的方法是包含一个`pAddress`。 如何解释此参数是由该表达式计算器和它所支持的语言的实现。  
  
## <a name="see-also"></a>请参阅  
 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)   
 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
