---
title: BP_REQUEST_INFO2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_REQUEST_INFO2
helpviewer_keywords:
- BP_REQUEST_INFO2 structure
ms.assetid: 008c87f7-a76e-43d3-8904-11b225d6a9a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 04d1db2ca8176678d8a72a84ede2bddcbfa2f152
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737883"
---
# <a name="bp_request_info2"></a>BP_REQUEST_INFO2
包含实现断点所需的信息，包括供应商 GUID、约束和跟踪点。

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
[BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)枚举中的标志的组合，用于指定填写哪些字段。

`guidLanguage`\
语言 GUID。

`bpLocation`\
指定断点位置类型的[BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)结构。

`pProgram`\
[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)对象，表示发生断点的应用程序。

`bstrProgramName`\
发生断点的应用程序的名称。

`pThread`\
[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示发生断点的线程。

`bstrThreadName`\
发生断点线程的名称。

`bpCondition`\
描述断点触发条件[BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)结构。

`bpPassCount`\
包含断点通过计数信息的[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)结构。

`dwFlags`\
BP_FLAGS[枚举](../../../extensibility/debugger/reference/bp-flags.md)中的标志的组合，用于指定请求的断点的标志。

`guidVendor`\
供应商的 GUID。 可能是空值。

`bstrConstraint`\
断点约束的名称。 可能是空值。

`bstrTracepoint`\
跟踪点的名称。 可能是空值。

## <a name="remarks"></a>备注
此结构由[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)方法返回。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

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
