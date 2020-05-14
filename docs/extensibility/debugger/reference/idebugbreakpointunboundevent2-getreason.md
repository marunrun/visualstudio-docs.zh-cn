---
title: IDebugBreakpoint 无绑定事件2：：获取原因 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointUnboundEvent2::GetReason
helpviewer_keywords:
- IDebugBreakpointUnboundEvent2::GetReason
ms.assetid: 0f8a4fec-d3eb-417d-8516-4f7b51904033
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9830309f0a40aee37982554e8920a95d289eb74c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734718"
---
# <a name="idebugbreakpointunboundevent2getreason"></a>IDebugBreakpointUnboundEvent2::GetReason
获取断点未绑定的原因。

## <a name="syntax"></a>语法

```cpp
HRESULT GetReason(
    BP_UNBOUND_REASON* pdwUnboundReason
);
```

```csharp
int GetReason(
    out enum_ BP_UNBOUND_REASON pdwUnboundReason
);
```

## <a name="parameters"></a>参数
`pdwUnboundReason`\
[出]从[BP_UNBOUND_REASON](../../../extensibility/debugger/reference/bp-unbound-reason.md)枚举返回值，指定断点未绑定的原因。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
原因包括断点在编辑和继续操作后反弹到其他位置，或者确定断点被错误地绑定。

## <a name="example"></a>示例
下面的示例演示如何为公开[IDebugBreakpoint UnbundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)接口的**CBreakpoint 未绑定 DebugEventBase**对象实现此方法。

```cpp
STDMETHODIMP CBreakpointUnboundDebugEventBase::GetReason(
    BP_UNBOUND_REASON* pdwUnboundReason)
{
    HRESULT hRes = E_FAIL;

    if ( EVAL(pdwUnboundReason) )
    {
        *pdwUnboundReason = m_dwReason;

        hRes = S_OK;
    }
    else
        hRes = E_INVALIDARG;

    return ( hRes );
}
```

## <a name="see-also"></a>请参阅
- [IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)
