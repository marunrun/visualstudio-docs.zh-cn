---
title: IDebugExpressionEvaluator2::SetCallback | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugExpressionEvaluator2::SetCallback
- SetCallback
ms.assetid: 31e3a99e-e784-44a3-8b19-cc5ef31ed546
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f347b687066578d5572a89a6e057fd2cb3b79e0b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66325489"
---
# <a name="idebugexpressionevaluator2setcallback"></a>IDebugExpressionEvaluator2::SetCallback
使表达式计算器 (EE) 来指定调试器引擎 (DE) 将用于读取指标设置的回调接口。

## <a name="syntax"></a>语法

```cpp
HRESULT SetCallback (
    IDebugSettingsCallback2* pCallback
);
```

```csharp
int SetCallback (
    IDebugSettingsCallback2 pCallback
);
```

## <a name="parameters"></a>参数
`pCallback`\
[in]要用于设置回调的接口。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
此方法提供的表达式计算器可用于读取指标设置会话调试管理器的接口。 适用于远程调试上读取指标[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]计算机。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CEE**对象，它公开[IDebugSettingsCallback2](../../../extensibility/debugger/reference/idebugsettingscallback2.md)接口。

```cpp
HRESULT CEE::SetCallback(IDebugSettingsCallback2* in_pCallback)
{
    // precondition
    INVARIANT( this );

    // function body
    if (NULL != this->m_LanguageSpecificUseCases.pfSetCallback)
    {
        EEDomain::fSetCallback DomainVal =
        {
            in_pCallback
        };

        BOOL bSuccess = (*this->m_LanguageSpecificUseCases.pfSetCallback)(DomainVal);
        ENSURE( bSuccess );
    }

    // postcondition
    INVARIANT( this );

    return S_OK;
}
```

## <a name="see-also"></a>请参阅
- [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)
