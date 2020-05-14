---
title: IDebug表达式评估器：：获取方法属性 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
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
[在]要使用的符号提供程序，表示为[IDebugSymbol 提供程序](../../../extensibility/debugger/reference/idebugsymbolprovider.md)对象。

`pAddress`\
[在]代码中的地址（表示为[IDebugAddress 对象](../../../extensibility/debugger/reference/idebugaddress.md)）应解析为最近的包含函数。

`pBinder`\
[在]要使用的活页夹，表示为[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)对象。

`fIncludeHiddenLocals`\
[在]非零`TRUE`（） 表示包括隐藏的局部变量;零`FALSE`（ ） 意味着排除隐藏的当地人

`ppProperty`\
[出]返回表示方法的[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)对象。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 隐藏的局部变量通常是编译器生成的变量。

## <a name="see-also"></a>请参阅
- [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
