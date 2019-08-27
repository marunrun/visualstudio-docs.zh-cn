---
title: BP_REQUEST_INFO2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO2
helpviewer_keywords:
- BP_REQUEST_INFO2 structure
ms.assetid: 008c87f7-a76e-43d3-8904-11b225d6a9a5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8f9c601cf1620d002bd86b8bc110d28bdb533e61
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352951"
---
# <a name="bprequestinfo2"></a>BP_REQUEST_INFO2
包含实现一个断点，包括供应商的 GUID、 约束和跟踪点所需的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_REQUEST_INFO2 {
    BPREQI_FIELDS   dwFields;
    GUID            guidLanguage;
    BP_LOCATION     bpLocation;
    IDebugProgram2* pProgram;
    BSTR            bstrProgramName;
    IDebugThread2*  pThread;
    BSTR            bstrThreadName;
    BP_CONDITION    bpCondition;
    BP_PASSCOUNT    bpPassCount;
    BP_FLAGS        dwFlags;
    GUID            guidVendor;
    BSTR            bstrConstraint;
    BSTR            bstrTracepoint;
} BP_REQUEST_INFO2;
```

```csharp
public struct BP_REQUEST_INFO2 {
    public uint           dwFields;
    public Guid           guidLanguage;
    public BP_LOCATION    bpLocation;
    public IDebugProgram2 pProgram;
    public string         bstrProgramName;
    public IDebugThread2  pThread;
    public string         bstrThreadName;
    public BP_CONDITION   bpCondition;
    public BP_PASSCOUNT   bpPassCount;
    public uint           dwFlags;
    public Guid           guidVendor;
    public string         bstrConstraint;
    public string         bstrTracepoint;
};
```

## <a name="members"></a>成员
`dwFields`\
中的标志的组合[BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)枚举，用于指定哪些字段填写。

`guidLanguage`\
语言 GUID。

`bpLocation`\
[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构，它指定的断点位置的类型。

`pProgram`\
[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)表示应用程序中发生断点的对象。

`bstrProgramName`\
断点发生的应用程序的名称。

`pThread`\
[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示该断点所在的线程。

`bstrThreadName`\
断点所在的线程的名称。

`bpCondition`\
[BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)结构，它描述将在其下触发断点的条件。

`bpPassCount`\
[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)结构，其中包含断点的传递计数信息。

`dwFlags`\
中的标志的组合[BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)枚举，用于指定请求的断点的标志。

`guidVendor`\
供应商的 GUID。 可能是一个 null 值。

`bstrConstraint`\
断点约束的名称。 可能是一个 null 值。

`bstrTracepoint`\
跟踪点的名称。 可能是一个 null 值。

## <a name="remarks"></a>备注
返回此结构[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)方法。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)
- [BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)
- [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)
