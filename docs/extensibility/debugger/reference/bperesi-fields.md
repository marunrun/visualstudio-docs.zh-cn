---
title: BPERESI_FIELDS |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737766"
---
# <a name="bperesi_fields"></a>BPERESI_FIELDS
指定要检索的有关断点的失败解决方法的信息。

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
初始化/使用 `bpResLocation` [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 结构的 (断点解析位置) "字段。

`BPERESI_PROGRAM`\
初始化/使用 `pProgram` 结构的字段 `BP_ERROR_RESOLUTION_INFO` 。

`BPERESI_THREAD`\
初始化/使用 `pThread` 结构的字段 `BP_ERROR_RESOLUTION_INFO` 。

`BPERESI_MESSAGE`\
初始化/使用 `bstrMessage` 结构的字段 `BP_ERROR_RESOLUTION_INFO` 。

`BPERESI_TYPE`\
初始化/使用 `dwType` 结构) 字段的 (断点类型 `BP_ERROR_RESOLUTION_INFO` 。

`BPERESI_ALLFIELDS`\
初始化/使用结构的所有字段 `BP_ERROR_RESOLUTION_INFO` 。

## <a name="remarks"></a>备注
作为参数传递给 [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md) 方法，以指示要初始化 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md) 结构的哪些字段。

这些值还用于指示结构中的哪些字段 `BP_ERROR_RESOLUTION_INFO` 已使用并且在返回该结构时有效。

这些值可以与按位组合 `OR` 。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)
