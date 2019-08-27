---
title: IDebugBreakpointUnboundEvent2::GetBreakpoint |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointUnboundEvent2::GetBreakpoint
helpviewer_keywords:
- IDebugBreakpointUnboundEvent2::GetBreakpoint
ms.assetid: ad73a207-b778-4dc5-b645-5ec668a63333
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: db0042e3c7d6f4c8ce7eabeef6e488d18cd0ad27
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352811"
---
# <a name="idebugbreakpointunboundevent2getbreakpoint"></a>IDebugBreakpointUnboundEvent2::GetBreakpoint
获取未绑定的断点。

## <a name="syntax"></a>语法

```cpp
HRESULT GetBreakpoint(
    IDebugBoundBreakpoint2** ppBP
);
```

```csharp
int GetBreakpoint(
    out IDebugBoundBreakpoint2 ppBP
);
```

## <a name="parameters"></a>参数
`ppBP`\
[out]返回[IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)表示未绑定断点的对象。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CBreakpointUnboundDebugEventBase**对象，它公开[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)接口。

```cpp
STDMETHODIMP CBreakpointUnboundDebugEventBase::GetBreakpoint(
    IDebugBoundBreakpoint2 **ppbp)
{
    HRESULT hRes = E_FAIL;

    if ( ppbp )
    {
        if ( m_pbp )
        {
            IDebugBoundBreakpoint2 *pibp;

            hRes = m_pbp->QueryInterface(IID_IDebugBoundBreakpoint2, (void **) & pibp);

            if ( S_OK == hRes )
                *ppbp = pibp;
        }
        else
            hRes = E_FAIL;
    }
    else
        hRes = E_INVALIDARG;

    return ( hRes );
}
```

## <a name="see-also"></a>请参阅
- [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)
- [IDebugBoundBreakpoint2](../../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
