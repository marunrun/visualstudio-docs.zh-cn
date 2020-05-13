---
title: BPERESI_FIELDS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BPERESI_FIELDS
helpviewer_keywords:
- BPERESI_FIELDS enumeration
ms.assetid: dd7dd89c-1043-46a1-a929-099cc039c344
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: af2f20e7d3abd79261dc18753a7eb940666fc186
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737766"
---
# <a name="bperesi_fields"></a>BPERESI_FIELDS
指定要检索有关断点解析失败的信息。

## <a name="syntax"></a>语法

```cpp
enum enum_BPERESI_FIELDS {
    PERESI_BPRESLOCATION = 0x0001,
    BPERESI_PROGRAM      = 0x0002,
    BPERESI_THREAD       = 0x0004,
    BPERESI_MESSAGE      = 0x0008,
    BPERESI_TYPE         = 0x0010,
    BPERESI_ALLFIELDS    = 0xffffffff
};
typedef DWORD BPERESI_FIELDS;
```

```csharp
public enum enum_BPERESI_FIELDS {
    PERESI_BPRESLOCATION = 0x0001,
    BPERESI_PROGRAM      = 0x0002,
    BPERESI_THREAD       = 0x0004,
    BPERESI_MESSAGE      = 0x0008,
    BPERESI_TYPE         = 0x0010,
    BPERESI_ALLFIELDS    = 0xffffffff
};
```

## <a name="fields"></a>字段
`PERESI_BPRESLOCATION`\
初始化/使用`bpResLocation`[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)结构的（断点分辨率位置）字段。

`BPERESI_PROGRAM`\
初始化/使用`pProgram`结构字段。 `BP_ERROR_RESOLUTION_INFO`

`BPERESI_THREAD`\
初始化/使用`pThread`结构字段。 `BP_ERROR_RESOLUTION_INFO`

`BPERESI_MESSAGE`\
初始化/使用`bstrMessage`结构字段。 `BP_ERROR_RESOLUTION_INFO`

`BPERESI_TYPE`\
初始化/使用`dwType``BP_ERROR_RESOLUTION_INFO`结构的（断点类型）字段。

`BPERESI_ALLFIELDS`\
初始化/使用`BP_ERROR_RESOLUTION_INFO`结构的所有字段。

## <a name="remarks"></a>备注
作为参数传递给[GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)方法，以指示要初始化[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)结构的字段。

这些值还用于指示在返回结构时使用结构`BP_ERROR_RESOLUTION_INFO`中的哪些字段并有效。

这些值可以稍微结合`OR`。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)
