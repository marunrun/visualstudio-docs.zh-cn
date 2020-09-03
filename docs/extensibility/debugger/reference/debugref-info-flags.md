---
title: DEBUGREF_INFO_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUGREF_INFO_FLAGS
helpviewer_keywords:
- DEBUGREF_INFO_FLAGS enumeration
ms.assetid: 1b043327-302a-4f6d-b51d-f94f9d7c7f9d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cb10ae5d3b4ce9f8aa777f643d412e075bd5293f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737386"
---
# <a name="debugref_info_flags"></a>DEBUGREF_INFO_FLAGS
指定要检索的有关调试引用对象的信息。

## <a name="syntax"></a>语法

```cpp
enum enum_DEBUGREF_INFO_FLAGS {
    DEBUGREF_INFO_NAME             = 0x00000001,
    DEBUGREF_INFO_TYPE             = 0x00000002,
    DEBUGREF_INFO_VALUE            = 0x00000004,
    DEBUGREF_INFO_ATTRIB           = 0x00000008,
    DEBUGREF_INFO_REFTYPE          = 0x00000010,
    DEBUGREF_INFO_REF              = 0x00000020,
    DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,
    DEBUGREF_INFO_NONE             = 0x00000000,
    DEBUGREF_INFO_ALL              = 0xffffffff
};
typedef DWORD DEBUGREF_INFO_FLAGS;
```

```csharp
public enum enum_DEBUGREF_INFO_FLAGS {
    DEBUGREF_INFO_NAME             = 0x00000001,
    DEBUGREF_INFO_TYPE             = 0x00000002,
    DEBUGREF_INFO_VALUE            = 0x00000004,
    DEBUGREF_INFO_ATTRIB           = 0x00000008,
    DEBUGREF_INFO_REFTYPE          = 0x00000010,
    DEBUGREF_INFO_REF              = 0x00000020,
    DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,
    DEBUGREF_INFO_NONE             = 0x00000000,
    DEBUGREF_INFO_ALL              = 0xffffffff
};
```

## <a name="fields"></a>字段
`DEBUGREF_INFO_NAME`\
初始化/使用 `bstrName` 结构中的字段。

`DEBUGREF_INFO_TYPE`\
初始化/使用 `bstrType` 结构中的字段。

`DEBUGREF_INFO_VALUE`\
初始化/使用 `bstrValue` 结构中的字段。

`DEBUGREF_INFO_ATTRIB`\
初始化/使用 `dwAttrib` 结构中的字段。

`DEBUGREF_INFO_REFTYPE`\
初始化/使用 `dwRefType` 结构中的字段。

`DEBUGREF_INFO_REF`\
初始化/使用 `pReference` 结构中的字段。

`DEBUGREF_INFO_VALUE_AUTOEXPAND`\
值字段应包含此类对象的自动扩展值（如果可用）。

`DEBUGREF_INFO_NONE`\
指示未设置任何标志。

`DEBUGREF_INFO_ALL`\
指示标志的掩码。

## <a name="remarks"></a>备注
这些标志传递给 [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md) 和 [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md) 方法，以指示要初始化 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 结构的哪些字段。

用于结构的 `dwFields` 成员，用于 `DEBUG_REFERENCE_INFO` 指示在返回结构时使用和有效的字段。

这些值可以与按位组合 `OR` 。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
- [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)
