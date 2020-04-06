---
title: IDebugsers表达式：：评估同步 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugParsedExpression::EvaluateSync
helpviewer_keywords:
- IDebugParsedExpression::EvaluateSync method
ms.assetid: 0ea04cfa-de87-4b6c-897e-4572c1a28942
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1f00b209ff5f91d160e89f5f55ad966fbe9e6414
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726009"
---
# <a name="idebugparsedexpressionevaluatesync"></a>IDebugParsedExpression::EvaluateSync
此方法计算解析的表达式，并选择性地将结果转换为另一种数据类型。

## <a name="syntax"></a>语法

```cpp
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

## <a name="parameters"></a>参数
`dwEvalFlags`\
[在][EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)常量的组合，用于控制表达式的计算方式。

`dwTimeout`\
[在]指定从此方法返回之前等待的最大时间（以毫秒为单位）。 用于`INFINITE`无限期等待。

`pSymbolProvider`\
[在]符号提供程序，表示为[IDebugSymbol 提供程序](../../../extensibility/debugger/reference/idebugsymbolprovider.md)接口。

`pAddress`\
[在]方法中的当前执行位置，表示为[IDebugAddress 接口](../../../extensibility/debugger/reference/idebugaddress.md)。

`pBinder`\
[在]活页夹，表示为[IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)接口。

`bstrResultType`\
[在]结果应强制转换为的类型。 此参数可以是 null 值。

`ppResult`\
[出]返回表示评估结果的[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)接口。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 表达式计算上下文由 提供`pAddress`，这样就可以确定包含方法，然后使用语言范围规则来确定表达式中符号的值。

## <a name="see-also"></a>请参阅
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)
