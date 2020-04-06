---
title: BPREQI_FIELDS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPREQI_FIELDS
helpviewer_keywords:
- BPREQI_FIELDS enumeration
ms.assetid: 679e771e-4a79-484e-af37-f962ef4aa245
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4c0e10b6c253c61a9e68e0cf161201f7d2520ae6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737749"
---
# <a name="bpreqi_fields"></a>BPREQI_FIELDS
指定要检索的关于断点请求的信息。

## <a name="syntax"></a>语法

```cpp
enum enum_BPREQI_FIELDS {
    BPREQI_BPLOCATION   = 0x0001,
    BPREQI_LANGUAGE     = 0x0002,
    BPREQI_PROGRAM      = 0x0004,
    BPREQI_PROGRAMNAME  = 0x0008,
    BPREQI_THREAD       = 0x0010,
    BPREQI_THREADNAME   = 0x0020,
    BPREQI_PASSCOUNT    = 0x0040,
    BPREQI_CONDITION    = 0x0080,
    BPREQI_FLAGS        = 0x0100,
    BPREQI_ALLOLDFIELDS = 0x01ff
    BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only
    BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only
    BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only
    BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only
};
typedef DWORD BPREQI_FIELDS;
```

```csharp
public enum enum_BPREQI_FIELDS {
    BPREQI_BPLOCATION   = 0x0001,
    BPREQI_LANGUAGE     = 0x0002,
    BPREQI_PROGRAM      = 0x0004,
    BPREQI_PROGRAMNAME  = 0x0008,
    BPREQI_THREAD       = 0x0010,
    BPREQI_THREADNAME   = 0x0020,
    BPREQI_PASSCOUNT    = 0x0040,
    BPREQI_CONDITION    = 0x0080,
    BPREQI_FLAGS        = 0x0100,
    BPREQI_ALLOLDFIELDS = 0x01ff
    BPREQI_VENDOR       = 0x0200,   // BP_REQUEST_INFO2 only
    BPREQI_CONSTRAINT   = 0x0400,   // BP_REQUEST_INFO2 only
    BPREQI_TRACEPOINT   = 0x0800,   // BP_REQUEST_INFO2 only
    BPREQI_ALLFIELDS    = 0x0fff    // BP_REQUEST_INFO2 only
};
```

## <a name="fields"></a>字段
`BPREQI_BPLOCATION`\
初始化/使用`bpLocation`[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)或[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构的（断点位置）字段。

`BPREQI_LANGUAGE`\
初始化/使用`guidLanguage``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI_PROGRAM`\
初始化/使用`pProgram``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI_PROGRAMNAME`\
初始化/使用`bstrProgramName``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI_THREAD`\
初始化/使用`pThread``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI_THREADNAME`\
初始化/使用`bstrThreadName``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI_PASSCOUNT`\
初始化/使用`bpPassCount``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI_CONDITION`\
初始化/使用`bpCondition``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的（断点条件）字段。

`BPREQI_FLAGS`\
初始化/使用`dwFlags``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI_ALLOLDFIELDS`\
初始化/使用`BP_REQUEST_INFO`结构的所有字段。

`BPREQI_VENDOR`\
初始化/使用结构`guidVendor`字段`BP_REQUEST_INFO2`。

`BPREQI_CONSTRAINT`\
初始化/使用结构`bstrConstraint`字段`BP_REQUEST_INFO2`。

`BPREQI_TRACEPOINT`\
初始化/使用结构`bstrTracepoint`字段`BP_REQUEST_INFO2`。

`BPREQI_ALLFIELDS`\
指定`BP_REQUEST_INFO2`结构的所有字段。

## <a name="remarks"></a>备注
作为参数传递给[GetRequestInfo，](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)[并BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)方法指定要初始化[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)和[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构的字段。

这些标志还用于指示返回每个结构时使用`BP_REQUEST_INFO`和`BP_REQUEST_INFO2`结构的字段并有效。

这些值可以稍微结合`OR`。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
