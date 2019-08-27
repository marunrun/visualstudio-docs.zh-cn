---
title: BP_LOCATION | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_LOCATION
helpviewer_keywords:
- BP_LOCATION union
ms.assetid: ed1e874c-f289-4c31-8b6c-04dde03ad0f5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d0d196342c834ed9f7fd9bf70859ae2b061344e2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66353031"
---
# <a name="bplocation"></a>BP_LOCATION
指定用于描述该断点的位置的结构的类型。

## <a name="syntax"></a>语法

```cpp
typedef struct _BP_LOCATION {
    BP_LOCATION_TYPE bpLocationType;
    union {
        BP_LOCATION_CODE_FILE_LINE   bplocCodeFileLine;
        BP_LOCATION_CODE_FUNC_OFFSET bplocCodeFuncOffset;
        BP_LOCATION_CODE_CONTEXT     bplocCodeContext;
        BP_LOCATION_CODE_STRING      bplocCodeString;
        BP_LOCATION_CODE_ADDRESS     bplocCodeAddress;
        BP_LOCATION_DATA_STRING      bplocDataString;
        BP_LOCATION_RESOLUTION       bplocResolution;
        DWORD                        unused;
    } bpLocation;
} BP_LOCATION;
```

```csharp
public struct BP_LOCATION {
    public uint   bpLocationType;
    public IntPtr unionmember1;
    public IntPtr unionmember2;
    public IntPtr unionmember3;
    public IntPtr unionmember4;
};
```

## <a name="members"></a>成员
`bpLocationType`\
中的值[BP_LOCATION_TYPE](../../../extensibility/debugger/reference/bp-location-type.md)枚举，用于解释`bpLocation`union 或`unionmemberX`成员。

`bpLocation`.`bplocCodeFileLine`\
[C++仅]包含[BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)结构，如果`bpLocationType`  =  `BPLT_CODE_FILE_LINE`。

`bpLocation.bplocCodeFuncOffset`\
[C++仅]包含[BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)结构，如果`bpLocationType`  =  `BPLT_CODE_FUNC_OFFSET`。

`bpLocation.bplocCodeContext`\
[C++仅]包含[BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)结构，如果`bpLocationType`  =  `BPLT_CODE_CONTEXT`。

`bpLocation.bplocCodeString`\
[C++仅]包含[BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)结构，如果`bpLocationType`  =  `BPLT_CODE_STRING`。

`bpLocation.bplocCodeAddress`\
[C++仅]包含[BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)结构，如果`bpLocationType`  =  `BPLT_CODE_ADDRESS`。

`bpLocation.bplocDataString`\
[C++仅]包含[BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)结构，如果`bpLocationType`  =  `BPLT_DATA_STRING`。

`bpLocation.bplocResolution`\
[C++仅]包含[BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)结构，如果`bpLocationType`  =  `BPLT_RESOLUTION`。

`unionmember1`\
[C#仅]请参阅关于如何解释的备注。

`unionmember2`\
[C#仅]请参阅关于如何解释的备注。

`unionmember3`\
[C#仅]请参阅关于如何解释的备注。

`unionmember4`\
[C#仅]请参阅关于如何解释的备注。

## <a name="remarks"></a>备注
此结构是的成员[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)并[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构。

 [C#仅]`unionmemberX`成员根据下表解释。 查看左侧列下方`bpLocationType`值，然后查看其他列来确定每个跨`unionmemberX`成员表示和封送`unionmemberX`相应地。 请参阅解释 C# 中的此结构的一部分的方法的示例。

|`bpLocationType`|`unionmember1`|`unionmember2`|`unionmember3`|`unionmember4`|
|----------------------|--------------------|--------------------|--------------------|--------------------|
|`BPLT_CODE_FILE_LINE`|`string` （上下文）|[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)|-|-|
|`BPLT_CODE_FUNC_OFFSET`|`string` （上下文）|[IDebugFunctionPosition2](../../../extensibility/debugger/reference/idebugfunctionposition2.md)|-|-|
|`BPLT_CODE_CONTEXT`|[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)|-|-|-|
|`BPLT_CODE_STRING`|`string` （上下文）|`string` （条件表达式）|-|-|
|`BPLT_CODE_ADDRESS`|`string` （上下文）|`string` (模块 URL)|`string` （函数名称）|`string` （地址）|
|`BPLT_DATA_STRING`|[IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)|`string` （上下文）|`string` （数据表达式）|`uint` （元素数）|
|`BPLT_RESOLUTION`|[IDebugBreakpointResolution2](../../../extensibility/debugger/reference/idebugbreakpointresolution2.md)|-|-|-|

## <a name="example"></a>示例
此示例显示了如何解释`BP_LOCATION`的 C# 中的结构`BPLT_DATA_STRING`类型。 这种特定类型显示了如何解释所有四个`unionmemberX`中所有可能的格式 （对象、 字符串和数字） 的成员。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(BP_LOCATION bp)
        {
            if (bp.bpLocationType == (uint)enum_BP_LOCATION_TYPE.BPLT_DATA_STRING)
            {
                IDebugThread2 pThread = (IDebugThread2)Marshal.GetObjectForIUnknown(bp.unionmember1);
                string context = Marshal.PtrToStringBSTR(bp.unionmember2);
                string dataExpression = Marshal.PtrToStringBSTR(bp.unionmember3);
                uint numElements = (uint)Marshal.ReadInt32(bp.unionmember4);
            }
        }
    }
}
```

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)
- [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)
- [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)
- [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)
- [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)
- [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)
- [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)
