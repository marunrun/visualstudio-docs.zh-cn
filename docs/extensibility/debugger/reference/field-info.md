---
title: FIELD_INFO |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- FIELD_INFO
helpviewer_keywords:
- FIELD_INFO structure
ms.assetid: bfafef6d-0c83-43d7-a779-1f0d24b166a1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6e2089746adecc583d04176afca18ad19826ea53
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736895"
---
# <a name="field_info"></a>FIELD_INFO
此结构描述局部变量、参数或其他字段。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagFieldInfo {
    FIELD_INFO_FIELDS dwFields;
    BSTR              bstrFullName;
    BSTR              bstrName;
    BSTR              bstrType;
    FIELD_MODIFIERS   dwModifiers;
} FIELD_INFO;
```

```csharp
public struct FIELD_INFO {
    public uint   dwFields;
    public string bstrFullName;
    public string bstrName;
    public string bstrType;
    public uint   dwModifiers;
};
```

## <a name="members"></a>成员
`dwFields`\
[FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md)枚举中的标志的组合，用于指定填充哪些成员。

`bstrFullName`\
字段的全名。

`bstrName`\
字段的短名称。

`bstrType`\
字段的类型。

`dwModifiers`\
描述字段[FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)枚举的标志的组合。

## <a name="remarks"></a>备注
此结构传递给填写它的[GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)方法。

## <a name="requirements"></a>要求
标题： sh.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [FIELD_INFO_FIELDS](../../../extensibility/debugger/reference/field-info-fields.md)
- [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugfield-getinfo.md)
