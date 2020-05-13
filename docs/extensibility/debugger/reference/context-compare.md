---
title: CONTEXT_COMPARE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_COMPARE
helpviewer_keywords:
- CONTEXT_COMPARE enumeration
ms.assetid: 701ed61c-a320-4c20-a335-0b840024abc0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1c88b50644d1adda2dd0eaa3b74a828f9739d70b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737603"
---
# <a name="context_compare"></a>CONTEXT_COMPARE
指定比较两个内存上下文的条件。

## <a name="syntax"></a>语法

```cpp
enum enum_CONTEXT_COMPARE {
    CONTEXT_EQUAL                 = 0x0001,
    CONTEXT_LESS_THAN             = 0x0002,
    CONTEXT_GREATER_THAN          = 0x0003,
    CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,
    CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,
    CONTEXT_SAME_SCOPE            = 0x0006,
    CONTEXT_SAME_FUNCTION         = 0x0007,
    CONTEXT_SAME_MODULE           = 0x0008,
    CONTEXT_SAME_PROCESS          = 0x0009
};
typedef DWORD CONTEXT_COMPARE;
```

```csharp
public enum enum_CONTEXT_COMPARE {
    CONTEXT_EQUAL                 = 0x0001,
    CONTEXT_LESS_THAN             = 0x0002,
    CONTEXT_GREATER_THAN          = 0x0003,
    CONTEXT_LESS_THAN_OR_EQUAL    = 0x0004,
    CONTEXT_GREATER_THAN_OR_EQUAL = 0x0005,
    CONTEXT_SAME_SCOPE            = 0x0006,
    CONTEXT_SAME_FUNCTION         = 0x0007,
    CONTEXT_SAME_MODULE           = 0x0008,
    CONTEXT_SAME_PROCESS          = 0x0009
};
```

## <a name="fields"></a>字段
`CONTEXT_EQUAL`\
在列表中查找与目标内存上下文相等的第一个内存上下文。

`CONTEXT_LESS_THAN`\
查找列表中的第一个内存上下文，该上下文小于目标内存上下文。

`CONTEXT_GREATER_THAN`\
查找列表中大于目标内存上下文的第一个内存上下文。

`CONTEXT_LESS_THAN_OR_EQUAL`\
查找列表中小于或等于目标内存上下文的第一个内存上下文。

`CONTEXT_GREATER_THAN_OR_EQUAL`\
查找列表中大于或等于目标内存上下文的第一个内存上下文。

`CONTEXT_SAME_SCOPE`\
查找列表中与目标内存上下文位于同一作用域中的第一个内存上下文。

`CONTEXT_SAME_FUNCTION`\
查找列表中与目标内存作用域具有相同函数的第一个内存上下文。

`CONTEXT_SAME_MODULE`\
查找列表中与目标内存上下文位于同一模块中的第一个内存上下文。

`CONTEXT_SAME_PROCESS`\
查找列表中与目标内存上下文处于相同进程的第一个内存上下文。

## <a name="remarks"></a>备注
作为参数传递给[比较](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)方法。

这些值用于查找列表中满足指定比较条件的第一个内存上下文。 为内存上下文提供内存上下文的列表，以便通过 方法`IDebugMemoryContext2::Compare`比较自身。 然后返回列表中的第一个内存上下文，`true`然后返回比较运算符。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [比较](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)
