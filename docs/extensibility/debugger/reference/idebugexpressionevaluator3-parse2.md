---
title: IDebugExpressionEvaluator3::Parse2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator3::Parse2
ms.assetid: 78099628-d600-4f76-b7c8-ee07c864af1e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 308ef67bab1d91ace71a5e741a1ed998037a9868
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352738"
---
# <a name="idebugexpressionevaluator3parse2"></a>IDebugExpressionEvaluator3::Parse2
将一个表达式字符串转换为给定的符号提供程序和评估的帧的地址的已分析表达式。

## <a name="syntax"></a>语法

```cpp
HRESULT Parse2 (
    LPCOLESTR                upstrExpression,
    PARSEFLAGS               dwFlags,
    UINT                     nRadix,
    IDebugSymbolProvider*    pSymbolProvider,
    IDebugAddress*           pAddress,
    BSTR*                    pbstrError,
    UINT*                    pichError,
    IDebugParsedExpression** ppParsedExpression
);
```

```csharp
HRESULT Parse2 (
    string                     upstrExpression,
    enum_PARSEFLAGS            dwFlags,
    uint                       nRadix,
    IDebugSymbolProvider       pSymbolProvider,
    IDebugAddress              pAddress,
    out string                 pbstrError,
    out uint                   pichError,
    out IDebugParsedExpression ppParsedExpression
);
```

## <a name="parameters"></a>参数
`upstrExpression`\
[in]要分析的表达式字符串。

`dwFlags`\
[in]一系列[PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)确定表达式的分析方式的常量。

`nRadix`\
[in]要用来解释任何数字信息的基数。

`pSymbolProvider`\
[in]符号提供程序的接口。

`pAddress`\
[in]评估帧的地址。

`pbstrError`\
[out]以用户可读文本形式将返回错误。

`pichError`\
[out]返回错误的起始字符的位置中的表达式字符串。

`ppParsedExpression`\
[out]返回中的已分析的表达式[IDebugParsedExpression](../../../extensibility/debugger/reference/idebugparsedexpression.md)对象。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
此方法生成的已分析的表达式不是一个实际值。 已分析的表达式是可供计算，即，转换为值。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CEE**对象，它公开[IDebugExpressionEvaluator3](../../../extensibility/debugger/reference/idebugexpressionevaluator3.md)接口。

```cpp
HRESULT CEE::Parse2 ( LPCOLESTR in_szExprText,
  PARSEFLAGS in_FLAGS,
  UINT in_RADIX,
  IDebugSymbolProvider *pSymbolProvider,
  IDebugAddress *pAddress,
  BSTR* out_pbstrError,
  UINT* inout_pichError,
  IDebugParsedExpression** out_ppParsedExpression )
{
    // precondition
    REQUIRE( NULL != in_szExprText );
    //REQUIRE( NULL != out_pbstrError );
    REQUIRE( NULL != inout_pichError );
    REQUIRE( NULL != out_ppParsedExpression );

    if (NULL == in_szExprText)
        return E_INVALIDARG;

    if (NULL == inout_pichError)
        return E_POINTER;

    if (NULL == out_ppParsedExpression)
        return E_POINTER;

    if (out_pbstrError)
        *out_pbstrError = NULL;

    *out_ppParsedExpression = NULL;

    INVARIANT( this );

    if (!this->ClassInvariant())
        return E_UNEXPECTED;

    // function body
    EEDomain::fParseExpression DomainVal =
    {
        this,                   // CEE*
        in_szExprText,          // LPCOLESTR
        in_FLAGS,               // EVALFLAGS
        in_RADIX,               // RADIX
        out_pbstrError,         // BSTR*
        inout_pichError,        // UINT*
        pSymbolProvider,
        out_ppParsedExpression  // Output
    };

    return (*m_LanguageSpecificUseCases.pfParseExpression)(DomainVal);
}
```

## <a name="see-also"></a>请参阅
- [IDebugExpressionEvaluator3](../../../extensibility/debugger/reference/idebugexpressionevaluator3.md)
