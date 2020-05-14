---
title: BP_ERROR_TYPE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_ERROR_TYPE
helpviewer_keywords:
- BP_ERROR_TYPE enumeration
ms.assetid: c483eaab-db29-46de-bfdb-5c2a9a9cfb68
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e777e1f8cb67187a81f8f3bb4f79299939bfa31c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738080"
---
# <a name="bp_error_type"></a>BP_ERROR_TYPE
指定断点的错误类型。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_ERROR_TYPE {
    BPET_NONE            = 0x00000000,
    BPET_TYPE_WARNING    = 0x00000001,
    BPET_TYPE_ERROR      = 0x00000002,
    BPET_SEV_HIGH        = 0x0F000000,
    BPET_SEV_GENERAL     = 0x07000000,
    BPET_SEV_LOW         = 0x01000000,
    BPET_TYPE_MASK       = 0x0000ffff,
    BPET_SEV_MASK        = 0xffff0000,
    BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,
    BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,
    BPET_ALL             = 0xffffffff
};
typedef DWORD BP_ERROR_TYPE;
```

```csharp
public enum enum_BP_ERROR_TYPE {
    BPET_NONE            = 0x00000000,
    BPET_TYPE_WARNING    = 0x00000001,
    BPET_TYPE_ERROR      = 0x00000002,
    BPET_SEV_HIGH        = 0x0F000000,
    BPET_SEV_GENERAL     = 0x07000000,
    BPET_SEV_LOW         = 0x01000000,
    BPET_TYPE_MASK       = 0x0000ffff,
    BPET_SEV_MASK        = 0xffff0000,
    BPET_GENERAL_WARNING = BPET_SEV_GENERAL | BPET_TYPE_WARNING,
    BPET_GENERAL_ERROR   = BPET_SEV_GENERAL | BPET_TYPE_ERROR,
    BPET_ALL             = 0xffffffff
};
```

## <a name="fields"></a>字段
`BPET_NONE`\
指定无断点错误。

`BPET_TYPE_WARNING`\
指定警告样式断点错误。

`BPET_TYPE_ERROR`\
指定错误样式断点错误。

`BPET_SEV_HIGH`\
指定高严重性断点错误。

`BPET_SEV_GENERAL`\
指定中等严重性断点错误。

`BPET_SEV_LOW`\
指定低严重性断点错误。

`BPET_TYPE_MASK`\
指定蒙版样式断点错误。

`BPET_SEV_MASK`\
指定严重性蒙版样式断点错误。

`BPET_GENERAL_WARNING`\
指定常规警告样式断点错误。

`BPET_GENERAL_ERROR`\
指定一般错误样式断点错误。

`BPET_ALL`\
指定所有断点错误类型。

## <a name="remarks"></a>备注
这些值可以与位组合，`OR`并用于`dwType`[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)结构的成员。 作为参数传递给[EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)方法。

断点错误类型由类型和严重性组成。 这意味着断点错误类型本身不仅仅是一种类型（例如 ，，）`BPET_TYPE_ERROR`或严重性（例如）。 `BPET_SEV_GENERAL` `BPET_GENERAL_WARNING`并为`BPET_GENERAL_ERROR`常规警告和错误断点提供预定义值。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
- [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)
