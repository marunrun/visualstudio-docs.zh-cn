---
title: IDebug 突破点错误事件2：：获取错误断点 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointErrorEvent2::GetErrorBreakpoint
helpviewer_keywords:
- IDebugBreakpointErrorEvent2::GetErrorBreakpoint
ms.assetid: e5acfd19-ac17-47f3-a31a-b2aa8baca36d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fe22f18d4574ffde48cea975bff8d8f5801ca465
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735070"
---
# <a name="idebugbreakpointerrorevent2geterrorbreakpoint"></a>IDebugBreakpointErrorEvent2::GetErrorBreakpoint
获取[IDebugError 断点 2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)对象，该对象描述断点未绑定的原因。

## <a name="syntax"></a>语法

```cpp
HRESULT GetErrorBreakpoint( 
    IDebugErrorBreakpoint2** ppErrorBP
);
```

```csharp
int GetErrorBreakpoint( 
    out IDebugErrorBreakpoint2 ppErrorBP
);
```

## <a name="parameters"></a>参数
`ppErrorBP`\
[出]返回描述警告或错误的[IDebugErrorBreakpointpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)对象。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
获取`IDebugErrorBreakpoint2`接口后，调用[GetBreakpoint 解析](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)方法获取[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)对象。 然后[，GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)方法可用于确定无效位置、无效表达式或未绑定挂起断点的原因，例如尚未加载代码等。

## <a name="example"></a>示例
下面的示例演示如何为公开[IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)接口的**CBreakpointSetDebugEventBase**对象实现此方法。

```cpp
STDMETHODIMP CBreakpointErrorDebugEventBase::GetErrorBreakpoint(
    IDebugErrorBreakpoint2 **ppbp)
{
    HRESULT hRes = E_FAIL;

    if ( ppbp )
    {
        if ( m_pError )
        {
            *ppbp = m_pError;

            m_pError->AddRef();

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
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
- [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
