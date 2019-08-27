---
title: IDebugExpressionContext2::ParseText | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExpressionContext2::ParseText
helpviewer_keywords:
- IDebugExpressionContext2::ParseText
ms.assetid: f58575db-f926-4ac8-83ff-7b3b86ab61e2
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 170183924c31933f77903a89851c15c463c326e6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325914"
---
# <a name="idebugexpressioncontext2parsetext"></a>IDebugExpressionContext2::ParseText
分析中以供以后计算的文本形式的表达式。

## <a name="syntax"></a>语法

```cpp
HRESULT ParseText(
    LPCOLESTR           pszCode,
    PARSEFLAGS          dwFlags,
    UINT                nRadix,
    IDebugExpression2** ppExpr,
    BSTR*               pbstrError,
    UINT*               pichError
);
```

```csharp
int ParseText(
    string                pszCode,
    enum_PARSEFLAGS       dwFlags,
    uint                  nRadix,
    out IDebugExpression2 ppExpr,
    out string            pbstrError,
    out uint              pichError
);
```

## <a name="parameters"></a>参数
`pszCode`\
[in]要分析的表达式。

`dwFlags`\
[in]中的标志的组合[PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)控制分析的枚举。

`nRadix`\
[in]若要在分析中的任何数字信息中使用的基数`pszCode`。

`ppExpr`\
[out]返回[IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)对象，表示已分析的表达式，即准备好进行绑定和评估。

`pbstrError`\
[out]如果表达式包含错误，则返回错误消息。

`pichError`\
[out]返回中的错误的字符索引`pszCode`如果表达式包含错误。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
调用此方法时，调试引擎 (DE) 应分析表达式，并验证正确。 `pbstrError`和`pichError`可能填充参数，如果表达式无效。

请注意，不会计算表达式，只能分析。 稍后调用[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)或[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)方法计算已分析的表达式的值。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于简单`CEnvBlock`公开的对象[IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)接口。 此示例将视为的表达式无法被分析为环境变量的名称，并从该变量中检索值。

```cpp
HRESULT CEnvBlock::ParseText(
    LPCOLESTR           pszCode,
    PARSEFLAGS          dwFlags,
    UINT                nRadix,
    IDebugExpression2 **ppExpr,
    BSTR               *pbstrError,
    UINT               *pichError)
{
    HRESULT hr = E_OUTOFMEMORY;
    // Create an integer variable with a value equal to one plus
    // twice the length of the passed expression to be parsed.
    int iAnsiLen      = 2 * (wcslen(pszCode)) + 1;
    // Allocate a character string of the same length.
    char *pszAnsiCode = (char *) malloc(iAnsiLen);

    // Check for successful memory allocation.
    if (pszAnsiCode) {
        // Map the wide-character pszCode string to the new pszAnsiCode character string.
        WideCharToMultiByte(CP_ACP, 0, pszCode, -1, pszAnsiCode, iAnsiLen, NULL, NULL);
        // Check to see if the app can succesfully get the environment variable.
        if (GetEnv(pszAnsiCode)) {

            // Create and initialize a CExpression object.
            CComObject<CExpression> *pExpr;
            CComObject<CExpression>::CreateInstance(&pExpr);
            pExpr->Init(pszAnsiCode, this, NULL);

            // Assign the pointer to the new object to the passed argument
            // and AddRef the object.
            *ppExpr = pExpr;
            (*ppExpr)->AddRef();
            hr = S_OK;
        // If the program cannot succesfully get the environment variable.
        } else {
            // Set the errror message and return E_FAIL.
            *pbstrError = SysAllocString(L"No such environment variable.");
            hr = E_FAIL;
        }
        // Free the local character string.
        free(pszAnsiCode);
    }
    return hr;
}
```

## <a name="see-also"></a>请参阅
- [IDebugExpressionContext2](../../../extensibility/debugger/reference/idebugexpressioncontext2.md)
- [PARSEFLAGS](../../../extensibility/debugger/reference/parseflags.md)
- [IDebugExpression2](../../../extensibility/debugger/reference/idebugexpression2.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
