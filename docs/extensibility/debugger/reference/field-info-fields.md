---
title: FIELD_INFO_FIELDS |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80736906"
---
# <a name="field_info_fields"></a>FIELD_INFO_FIELDS
指定要检索的有关 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象的信息。

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
初始化/使用 `bstrFullName` [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) 结构中的字段。

`FIF_NAME`\
初始化/使用 `bstrName` 结构中的字段 `FIELD_INFO` 。

`FIF_TYPE`\
初始化/使用 `bstrType` 结构中的字段 `FIELD_INFO` 。

`FIF_MODIFIERS`\
初始化/使用 `bstrModifiers` 结构中的字段 `FIELD_INFO` 。

## <a name="remarks"></a>备注
还会将这些值作为参数传递给 [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md) 方法，以指定要初始化 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md) 结构的哪些字段。

还在结构的成员中使用这些值 `dwFields` `FIELD_INFO` 来指示使用和有效的字段。

这些标志可以与按位组合 `OR` 。

## <a name="requirements"></a>要求
标头： sh。h

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
