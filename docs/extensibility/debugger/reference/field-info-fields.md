---
title: FIELD_INFO_FIELDS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_INFO_FIELDS
helpviewer_keywords:
- FIELD_INFO_FIELDS enumeration
ms.assetid: a69487d2-e701-4165-804a-8a011df9a3bd
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 01853df78bfe731ea4b7159f7b3ebe352f3c5eaa
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66337669"
---
# <a name="fieldinfofields"></a>FIELD_INFO_FIELDS
指定要检索相关信息[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。

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
初始化/用`bstrFullName`字段中[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)结构。

`FIF_NAME`\
初始化/用`bstrName`字段中`FIELD_INFO`结构。

`FIF_TYPE`\
初始化/用`bstrType`字段中`FIELD_INFO`结构。

`FIF_MODIFIERS`\
初始化/用`bstrModifiers`字段中`FIELD_INFO`结构。

## <a name="remarks"></a>备注
这些值也会作为参数传递[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)方法，以指定的哪些字段[FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)结构是进行初始化。

中还使用这些值`dwFields`的成员`FIELD_INFO`结构，用于指示哪些字段是使用，有效。

可能的按位组合这些标志`OR`。

## <a name="requirements"></a>要求
标头： sh.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
