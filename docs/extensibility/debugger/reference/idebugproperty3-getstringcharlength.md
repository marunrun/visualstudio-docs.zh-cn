---
title: IDebugProperty3::GetStringCharLength |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::GetStringCharLength
helpviewer_keywords:
- IDebugProperty3::GetStringCharLength
ms.assetid: 89a8676b-6da9-4358-91c2-039bf33f99e4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2d8cedb7ceb5b1b73a86e9c1b93aaa2ae54da579
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66348793"
---
# <a name="idebugproperty3getstringcharlength"></a>IDebugProperty3::GetStringCharLength
返回关联的属性的字符串中的字符数。

## <a name="syntax"></a>语法

```cpp
HRESULT GetStringCharLength(
    ULONG *pLen
);
```

```csharp
int GetStringCharLength(
    out uint pLen
);
```

## <a name="parameters"></a>参数

|参数|描述|
|---------------|-----------------|
|`pLen`|[out]返回属性的字符串中的字符数。|

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则返回错误代码。

## <a name="remarks"></a>备注
通常情况下，此方法用作调用分配一个缓冲区的 prelude [GetStringChars](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md)方法。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CProperty**对象，它公开[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)接口。

```cpp
STDMETHODIMP CProperty::GetStringCharLength(ULONG *pLen)
{
    HRESULT hr = E_INVALIDARG;

    EVALFLAGS oldEVALFLAGS = m_EVALFLAGS;

    m_EVALFLAGS &= ~EVAL_NOFUNCEVAL;

    if (pLen)
    {
        DEBUG_PROPERTY_INFO dpInfo;
        dpInfo.bstrValue = NULL;
        ULONG ulen = 0;
        hr = GetPropertyInfo(DEBUGPROP_INFO_VALUE,10,DEFAULT_TIMEOUT,NULL,0,&dpInfo);
        if (hr == S_OK && dpInfo.bstrValue)
        {
            if (wcscmp(dpInfo.bstrValue,L"Nothing") == 0)
            {
                ulen = 0; //VSWhidbey#64815
            }
            else
            {
                ulen = ::SysStringLen(dpInfo.bstrValue);
                if( ulen > 2 &&
                    dpInfo.bstrValue[0] == L'"' &&
                    dpInfo.bstrValue[ulen-1] == L'"')
                {
                    ulen = ulen > 2 ? ulen - 2 : ulen; //remove two double quotes
                }
            }
        }
        ::SysFreeString(dpInfo.bstrValue);
        *pLen = ulen;
    }
    m_EVALFLAGS = oldEVALFLAGS;
    return hr;
}
```

## <a name="see-also"></a>请参阅
- [GetStringChars](../../../extensibility/debugger/reference/idebugproperty3-getstringchars.md)
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
