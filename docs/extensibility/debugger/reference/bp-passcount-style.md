---
title: BP_PASSCOUNT_STYLE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_PASSCOUNT_STYLE
helpviewer_keywords:
- BP_PASSCOUNT_STYLE structure
ms.assetid: 0a647047-e2d5-4724-a0b8-68108425ecad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1633c5e9aa6ff251fedce83a0243664cd9e0e0a7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737913"
---
# <a name="bp_passcount_style"></a>BP_PASSCOUNT_STYLE
指定与断点通过计数关联的条件，这些条件会导致断点触发。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_PASSCOUNT_STYLE {
    BP_PASSCOUNT_NONE             = 0x0000,
    BP_PASSCOUNT_EQUAL            = 0x0001,
    BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,
    BP_PASSCOUNT_MOD              = 0x0003
};
typedef DWORD BP_PASSCOUNT_STYLE;
```

```csharp
public enum enum_BP_PASSCOUNT_STYLE {
    BP_PASSCOUNT_NONE             = 0x0000,
    BP_PASSCOUNT_EQUAL            = 0x0001,
    BP_PASSCOUNT_EQUAL_OR_GREATER = 0x0002,
    BP_PASSCOUNT_MOD              = 0x0003
};
```

## <a name="fields"></a>字段
`BP_PASSCOUNT_NONE`\
指定无断点传递计数样式。

`BP_PASSCOUNT_EQUAL`\
将断点传递计数样式设置为相等。 当断点被击中的次数等于通过计数时，断点将触发。

`BP_PASSCOUNT_EQUAL_OR_GREATER`\
将断点传递计数样式设置为相等或更大。 当断点命中的次数等于或大于通过计数时，断点将触发。

`BP_PASSCOUNT_MOD`\
指定蒙杜洛通数。 例如，如果传递计数是类型`BP_PASSCOUNT_MOD`，并且通过计数值为 4，则每次命中计数为 4 的倍数时，断点都会触发。

## <a name="remarks"></a>备注
用于BP_PASSCOUNT结构`stylePassCount`的成员，该[BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)结构依次是[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)和[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构的成员。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
