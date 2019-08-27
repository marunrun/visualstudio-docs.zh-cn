---
title: IDebugBreakpointBoundEvent2::EnumBoundBreakpoints | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
helpviewer_keywords:
- IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
ms.assetid: 1f588feb-522e-488d-be92-7bc19b9e3688
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2584e49209dd95c3d43673eadf72e138ac828f57
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66314389"
---
# <a name="idebugbreakpointboundevent2enumboundbreakpoints"></a>IDebugBreakpointBoundEvent2::EnumBoundBreakpoints
创建已绑定到此事件的断点的枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumBoundBreakpoints( 
    IEnumDebugBoundBreakpoints2** ppEnum
);
```

```csharp
int EnumBoundBreakpoints( 
    out IEnumDebugBoundBreakpoints2 ppEnum
);
```

## <a name="parameters"></a>参数
`ppEnum`\
[out]返回[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)此事件从绑定枚举所有断点的对象。

## <a name="return-value"></a>返回值
如果成功，则返回 `S_OK`。 返回`S_FALSE`是否存在任何绑定的断点; 否则，返回错误代码。

## <a name="remarks"></a>备注
绑定断点的列表用于这些绑定到此事件，可能不是绑定从挂起断点的断点的完整列表。 若要获取所有绑定到挂起断点的断点的列表，请调用[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)方法以获取相关联[IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)对象，然后调用[EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)方法以获取[IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)对象，其中包含有关挂起断点的所有绑定的断点。

## <a name="example"></a>示例
下面的示例演示如何实现此方法对于**CBreakpointSetDebugEventBase**对象，它公开[IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)接口。

```cpp
STDMETHODIMP CBreakpointSetDebugEventBase::EnumBoundBreakpoints(
    IEnumDebugBoundBreakpoints2 **ppEnum)
{
    HRESULT hRes = E_FAIL;

    if ( ppEnum )
    {
        if ( m_pEnumBound )
        {
            hRes = m_pEnumBound->Clone(ppEnum);

            if ( EVAL(S_OK == hRes) )
                (*ppEnum)->Reset();
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
- [IEnumDebugBoundBreakpoints2](../../../extensibility/debugger/reference/ienumdebugboundbreakpoints2.md)
- [GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointboundevent2-getpendingbreakpoint.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [EnumBoundBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumboundbreakpoints.md)
