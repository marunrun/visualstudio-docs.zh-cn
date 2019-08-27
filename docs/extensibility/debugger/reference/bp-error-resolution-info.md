---
title: BP_ERROR_RESOLUTION_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_ERROR_RESOLUTION_INFO
helpviewer_keywords:
- BP_ERROR_RESOLUTION_INFO structure
ms.assetid: a6b83242-5728-4716-80f3-840c96d59c6c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dca7dcac5dc7ccf4d30d9b61165771ba464bbcf9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351827"
---
# <a name="bperrorresolutioninfo"></a>BP_ERROR_RESOLUTION_INFO
描述错误断点，包括位置、 程序和线程的解决方法。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_ERROR_RESOLUTION_INFO {
    BPERESI_FIELDS         dwFields;
    BP_RESOLUTION_LOCATION bpResLocation;
    IDebugProgram2*        pProgram;
    IDebugThread2*         pThread;
    BSTR                   bstrMessage;
    BP_ERROR_TYPE          dwType;
} BP_ERROR_RESOLUTION_INFO;
```

```csharp
public struct BP_ERROR_RESOLUTION_INFO {
    public uint                   dwFields;
    public BP_RESOLUTION_LOCATION bpResLocation;
    public IDebugProgram2         pProgram;
    public IDebugThread2          pThread;
    public string                 bstrMessage;
    public uint                   dwType;
};
```

## <a name="members"></a>成员
`dwFields`\
中值的组合[BPERESI_FIELDS](../../../extensibility/debugger/reference/bperesi-fields.md)枚举，它指定填充此结构的哪些字段。

`bpResLocation`\
[BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md) union，这将指定的断点解析位置。

`pProgram`\
[IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)表示应用程序发生断点错误的对象。

`pThread`\
[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)对象，表示生成断点错误的应用程序正在其运行的线程。

`bstrMessage`\
包含导致此错误解决方法的任何警告或错误消息的字符串。

`dwType`\
中的值[BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)枚举，用于指定断点错误类型。

## <a name="remarks"></a>备注
此结构返回从[GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)方法。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)
- [BPRESI_FIELDS](../../../extensibility/debugger/reference/bpresi-fields.md)
- [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [BP_ERROR_TYPE](../../../extensibility/debugger/reference/bp-error-type.md)
