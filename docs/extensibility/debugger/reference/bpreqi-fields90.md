---
title: BPREQI_FIELDS90 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- BPREQI_FIELDS90 enumeration
ms.assetid: bf6f7efc-39f2-46a2-906d-c3647bf89995
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ea46939118ec48490280d6a85cc84e144d320d4e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737735"
---
# <a name="bpreqi_fields90"></a>BPREQI_FIELDS90
枚举指定要检索的关于断点请求的信息的有效值。 此枚举扩展了[BPREQI_FIELDS](../../../extensibility/debugger/reference/bpreqi-fields.md)枚举。

## <a name="syntax"></a>语法

```cpp
enum enum_BPREQI_FIELDS90
{
    // VS 8.0 values
    BPREQI90_BPLOCATION                = 0x0001,
    BPREQI90_LANGUAGE                  = 0x0002,
    BPREQI90_PROGRAM                   = 0x0004,
    BPREQI90_PROGRAMNAME               = 0x0008,
    BPREQI90_THREAD                    = 0x0010,
    BPREQI90_THREADNAME                = 0x0020,
    BPREQI90_PASSCOUNT                 = 0x0040,
    BPREQI90_CONDITION                 = 0x0080,
    BPREQI90_FLAGS                     = 0x0100,
    BPREQI90_ALLOLDFIELDS              = 0x01ff,
    BPREQI90_VENDOR                    = 0x0200,
    BPREQI90_CONSTRAINT                = 0x0400,
    BPREQI90_TRACEPOINT                = 0x0800,

    // Values added in VS 9.0
    BPREQI90_MACROTRACEPOINT           = 0x1000,

    BPREQI90_ALLFIELDS                 = 0xffff
};
typedef DWORD BPREQI_FIELDS90;
```

```csharp
public enum enum_BPREQI_FIELDS90
{
    // VS 8.0 values
    BPREQI90_BPLOCATION                = 0x0001,
    BPREQI90_LANGUAGE                  = 0x0002,
    BPREQI90_PROGRAM                   = 0x0004,
    BPREQI90_PROGRAMNAME               = 0x0008,
    BPREQI90_THREAD                    = 0x0010,
    BPREQI90_THREADNAME                = 0x0020,
    BPREQI90_PASSCOUNT                 = 0x0040,
    BPREQI90_CONDITION                 = 0x0080,
    BPREQI90_FLAGS                     = 0x0100,
    BPREQI90_ALLOLDFIELDS              = 0x01ff,
    BPREQI90_VENDOR                    = 0x0200,
    BPREQI90_CONSTRAINT                = 0x0400,
    BPREQI90_TRACEPOINT                = 0x0800,

    // Values added in VS 9.0
    BPREQI90_MACROTRACEPOINT           = 0x1000,

    BPREQI90_ALLFIELDS                 = 0xffff
};
```

## <a name="fields"></a>字段
`BPREQI90_BPLOCATION`\
初始化或使用[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)或`bpLocation`[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构的（断点位置）字段。

`BPREQI90_LANGUAGE`\
初始化或使用`guidLanguage``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI90_PROGRAM`\
初始化或使用`pProgram``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI90_PROGRAMNAME`\
初始化或使用`bstrProgramName``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI90_THREAD`\
初始化或使用`pThread``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI90_THREADNAME`\
初始化或使用`bstrThreadName``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI90_PASSCOUNT`\
初始化或使用`bpPassCount``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI90_CONDITION`\
初始化或使用`bpCondition``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的（断点条件）字段。

`BPREQI90_FLAGS`\
初始化或使用`dwFlags``BP_REQUEST_INFO`或`BP_REQUEST_INFO2`结构的字段。

`BPREQI90_ALLOLDFIELDS`\
初始化或使用`BP_REQUEST_INFO`结构的所有字段。

`BPREQI90_VENDOR`\
初始化或使用结构`guidVendor`字段。 `BP_REQUEST_INFO2`

`BPREQI90_CONSTRAINT`\
初始化或使用结构`bstrConstraint`字段。 `BP_REQUEST_INFO2`

`BPREQI90_TRACEPOINT`\
初始化或使用结构`bstrTracepoint`字段。 `BP_REQUEST_INFO2`

`BPREQI90_MACROTRACEPOINT`\
初始化或使用结构`bstrMacroTracepoint`字段。 `BP_REQUEST_INFO2` BPREQI_ALLFIELDS不包括此字段。

`BPREQI90_ALLFIELDS`\
指定`BP_REQUEST_INFO2`结构的所有字段。

## <a name="requirements"></a>要求
标题： Msdbg90.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
