---
title: DEBUGREF_INFO_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUGREF_INFO_FLAGS
helpviewer_keywords:
- DEBUGREF_INFO_FLAGS enumeration
ms.assetid: 1b043327-302a-4f6d-b51d-f94f9d7c7f9d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1adab87ed09ca2ff16d837da084d8cc0b76956fe
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318358"
---
# <a name="debugrefinfoflags"></a>DEBUGREF_INFO_FLAGS
指定要检索有关调试引用对象的信息。

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
初始化/使用`bstrName`结构中的字段。

`DEBUGREF_INFO_TYPE`\
初始化/使用`bstrType`结构中的字段。

`DEBUGREF_INFO_VALUE`\
初始化/使用`bstrValue`结构中的字段。

`DEBUGREF_INFO_ATTRIB`\
初始化/使用`dwAttrib`结构中的字段。

`DEBUGREF_INFO_REFTYPE`\
初始化/使用`dwRefType`结构中的字段。

`DEBUGREF_INFO_REF`\
初始化/使用`pReference`结构中的字段。

`DEBUGREF_INFO_VALUE_AUTOEXPAND`\
值字段应包含自动扩展值中，如果可用，此类型的对象。

`DEBUGREF_INFO_NONE`\
指示未设置任何标志。

`DEBUGREF_INFO_ALL`\
表示的标志的掩码。

## <a name="remarks"></a>备注
这些标志传递给[EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)并[GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)方法，以指示的哪些字段[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)结构是进行初始化。

用于`dwFields`的成员`DEBUG_REFERENCE_INFO`结构，用于指示哪些字段是使用，有效时返回该结构。

可能的按位组合这些值`OR`。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
- [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)
