---
title: IDebugExpressionEvaluator：： GetMethodProperty |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionEvaluator::GetMethodProperty
helpviewer_keywords:
- IDebugExpressionEvaluator::GetMethodProperty method
ms.assetid: c394fe4d-eeb6-4feb-828c-098d84a6f1ba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ebcf24ee39505091ff79c1f2f31d505217f77efb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80729506"
---
# <a name="idebugexpressionevaluatorgetmethodproperty"></a>IDebugExpressionEvaluator::GetMethodProperty
此方法获取包含方法的局部变量、参数和其他属性的属性对象。

## <a name="syntax"></a>语法

```cpp
HRESULT GetMethodProperty( 
   IDebugSymbolProvider* pSymbolProvider,
   IDebugAddress*        pAddress,
   IDebugBinder*         pBinder,
   BOOL                  fIncludeHiddenLocals,
   IDebugProperty2**     ppProperty
);
```

```csharp
int GetMethodProperty(
   IDebugSymbolProvider pSymbolProvider,
   IDebugAddress        pAddress,
   IDebugBinder         pBinder,
   int                  fIncludeHiddenLocals,
   out IDebugProperty2  ppProperty
);
```

## <a name="parameters"></a>参数
`pSymbolProvider`\
中要使用的符号提供程序，以 [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md) 对象的形式表示。

`pAddress`\
中代码中表示为 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象的地址，应解析为最接近的包含函数。

`pBinder`\
中要使用的联编程序，表示为 [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md) 对象。

`fIncludeHiddenLocals`\
中非零 (`TRUE`) 意味着包含隐藏的局部变量; 零 (`FALSE`) 表示保留隐藏的局部变量

`ppProperty`\
弄返回表示方法的 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) 对象。

## <a name="return-value"></a>返回值
 如果成功， `S_OK` 则返回; 否则返回错误代码。

## <a name="remarks"></a>备注
 隐藏的局部变量通常是编译器生成的变量。

## <a name="see-also"></a>另请参阅
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
