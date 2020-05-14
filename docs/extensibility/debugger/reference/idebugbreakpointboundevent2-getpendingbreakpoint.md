---
title: IDebug 突破点绑定事件2：：获取待定断点 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2::GetPendingBreakpoint
helpviewer_keywords:
- IDebugBreakpointBoundEvent2::GetPendingBreakpoint
ms.assetid: 6da7ed86-b412-4964-b6a3-0687a66f63fe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 85c137445e2255a76f7fa3be2fb56e2579e578c6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735251"
---
# <a name="idebugbreakpointboundevent2getpendingbreakpoint"></a>IDebugBreakpointBoundEvent2::GetPendingBreakpoint
获取正在绑定的挂起断点。

## <a name="syntax"></a>语法

```cpp
HRESULT GetPendingBreakpoint(
    IDebugPendingBreakpoint2** ppPendingBP
);
```

```cpp
int GetPendingBreakpoint(
    out IDebugPendingBreakpoint2 ppPendingBP
);
```

## <a name="parameters"></a>参数
`ppPendingBP`\
[出]返回表示要绑定的挂起断点的[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)对象。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="example"></a>示例
下面的示例演示如何为公开[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)接口的**CBreakpointSetDebugEventBase**对象实现此方法。

```cpp
STDMETHODIMP CBreakpointSetDebugEventBase::GetPendingBreakpoint(
    IDebugPendingBreakpoint2 **ppPendingBP)
{
    HRESULT hRes = E_FAIL;

    if ( ppPendingBP )
    {
        if ( m_pPendingBP )
        {
            *ppPendingBP = m_pPendingBP;

            m_pPendingBP->AddRef();

            hRes = S_OK;
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
- [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
