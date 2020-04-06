---
title: FIELD_INFO_FIELDS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_INFO_FIELDS
helpviewer_keywords:
- FIELD_INFO_FIELDS enumeration
ms.assetid: a69487d2-e701-4165-804a-8a011df9a3bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9a3d2e796d37606c51918d8e49db920161d63f55
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736906"
---
# <a name="field_info_fields"></a>FIELD_INFO_FIELDS
指定要检索的关于[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象的信息。

## <a name="syntax"></a>语法

```cpp
enum enum_FIELD_INFO_FIELDS { 
    FIF_FULLNAME  = 0x0001,
    FIF_NAME      = 0x0002,
    FIF_TYPE      = 0x0004,
    FIF_MODIFIERS = 0x0008,
    FIF_ALL       = 0xffffffff,
    FIF_NONE      = 0x0000
};
typedef DWORD FIELD_INFO_FIELDS;
```

```csharp
public enum enum_FIELD_INFO_FIELDS {
    FIF_FULLNAME  = 0x0001,
    FIF_NAME      = 0x0002,
    FIF_TYPE      = 0x0004,
    FIF_MODIFIERS = 0x0008,
    FIF_ALL       = 0xffffffff,
    FIF_NONE      = 0x0000
};
```

## <a name="fields"></a>字段
`FIF_FULLNAME`\
初始化/使用`bstrFullName`[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)结构中的字段。

`FIF_NAME`\
初始化/使用结构`bstrName`中的`FIELD_INFO`字段。

`FIF_TYPE`\
初始化/使用结构`bstrType`中的`FIELD_INFO`字段。

`FIF_MODIFIERS`\
初始化/使用结构`bstrModifiers`中的`FIELD_INFO`字段。

## <a name="remarks"></a>备注
这些值也作为参数传递给[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)方法，以指定要初始化[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)结构的字段。

这些值还用于结构`dwFields`的成员中`FIELD_INFO`，以指示使用哪些字段有效。

这些标志可以稍微结合`OR`。

## <a name="requirements"></a>要求
标题： sh.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
