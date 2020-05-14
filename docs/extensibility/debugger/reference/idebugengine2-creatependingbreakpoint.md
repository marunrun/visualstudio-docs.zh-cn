---
title: IDebugEngine2：：创建待处理断点 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2::CreatePendingBreakpoint
helpviewer_keywords:
- IDebugEngine2::CreatePendingBreakpoint
ms.assetid: 92e85b90-a931-48d9-89a7-a6edcb83ae5a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f88cae3610487b92fed0d8390d44c55d3f536c4b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731114"
---
# <a name="idebugengine2creatependingbreakpoint"></a>IDebugEngine2::CreatePendingBreakpoint
在调试引擎 （DE） 中创建挂起的断点。

## <a name="syntax"></a>语法

```cpp
HRESULT CreatePendingBreakpoint(
    IDebugBreakpointRequest2*  pBPRequest,
    IDebugPendingBreakpoint2** ppPendingBP
);
```

```csharp
int CreatePendingBreakpoint(
    IDebugBreakpointRequest2     pBPRequest,
    out IDebugPendingBreakpoint2 ppPendingBP
);
```

## <a name="parameters"></a>参数
`pBPRequest`\
[在]描述要创建的挂起断点的[IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)对象。

`ppPendingBP`\
[出]返回表示挂起断[点的 IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)对象。

## <a name="return-value"></a>返回值
如果成功，返回`S_OK`;否则，返回错误代码。 如果`E_FAIL``pBPRequest`参数与 DE 支持的任何语言不匹配，`pBPRequest`则通常返回该参数无效或不完整。

## <a name="remarks"></a>备注
挂起的断点实质上是绑定断点到代码所需的所有信息的集合。 在调用[Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)方法之前，从此方法返回的挂起断点不会绑定到代码。

对于用户设置的每个挂起的断点，会话调试管理器 （SDM） 在每个附加的 DE 中调用此方法。 由 DE 验证断点是否对运行在该 DE 中的程序有效。

当用户在代码行上设置断点时，DE 可以自由地将断点绑定到文档中对应于此代码的最近行。 这样，用户就可以在多行语句的第一行上设置断点，但将其绑定到最后一行（其中所有代码都归于调试信息中）。

## <a name="example"></a>示例
下面的示例演示如何实现此方法的简单`CProgram`对象。 然后，DE 的 实现`IDebugEngine2::CreatePendingBreakpoint`可以将所有调用转发到每个程序中的方法的此实现。

```
HRESULT CProgram::CreatePendingBreakpoint(IDebugBreakpointRequest2* pBPRequest, IDebugPendingBreakpoint2** ppPendingBP)
{
    // Create and initialize the CPendingBreakpoint object.
    CComObject<CPendingBreakpoint> *pPending;
    CComObject<CPendingBreakpoint>::CreateInstance(&pPending);
    pPending->Initialize(pBPRequest, m_pInterp, m_pCallback, m_pEngine);
    return pPending->QueryInterface(ppPendingBP);
}
```

## <a name="see-also"></a>请参阅
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [绑定](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
