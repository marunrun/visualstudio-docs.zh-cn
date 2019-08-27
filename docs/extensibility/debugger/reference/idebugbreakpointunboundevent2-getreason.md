---
title: IDebugBreakpointUnboundEvent2::GetReason | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointUnboundEvent2::GetReason
helpviewer_keywords:
- IDebugBreakpointUnboundEvent2::GetReason
ms.assetid: 0f8a4fec-d3eb-417d-8516-4f7b51904033
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5b3c15b25ec6f4f2d7ddc56efc163ec2eb6b81c0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352839"
---
# <a name="idebugbreakpointunboundevent2getreason"></a>IDebugBreakpointUnboundEvent2::GetReason
获取断点是未绑定的原因。

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
[out]返回一个值从[BP_UNBOUND_REASON](../../../extensibility/debugger/reference/bp-unbound-reason.md)指定断点是未绑定的原因的枚举。

## <a name="return-value"></a>返回值
如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
原因包括： 正在重新绑定到另一个位置后编辑并继续操作或确定断点时在错误中绑定一个断点。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CBreakpointUnboundDebugEventBase**对象，它公开[IDebugBreakpointUnboundEvent2](../../../extensibility/debugger/reference/idebugbreakpointunboundevent2.md)接口。

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
