---
title: CONTEXT_COMPARE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_COMPARE
helpviewer_keywords:
- CONTEXT_COMPARE enumeration
ms.assetid: 701ed61c-a320-4c20-a335-0b840024abc0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 28e81e8247e0ab7a7b2e972209805c8bcff053a7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346404"
---
# <a name="contextcompare"></a>CONTEXT_COMPARE
指定用于比较两个内存上下文的条件。

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
在列表中，它等于目标内存上下文中找到的第一个内存上下文。

`CONTEXT_LESS_THAN`\
小于目标内存上下文在列表中找到的第一个内存上下文。

`CONTEXT_GREATER_THAN`\
在列表的最大目标内存上下文中找到的第一个内存上下文。

`CONTEXT_LESS_THAN_OR_EQUAL`\
小于或等于目标内存上下文在列表中找到的第一个内存上下文。

`CONTEXT_GREATER_THAN_OR_EQUAL`\
大于或等于目标内存上下文在列表中找到的第一个内存上下文。

`CONTEXT_SAME_SCOPE`\
目标内存上下文与同一作用域中在列表中找到的第一个内存上下文。

`CONTEXT_SAME_FUNCTION`\
在与目标内存范围内相同的功能是在列表中找到的第一个内存上下文。

`CONTEXT_SAME_MODULE`\
中的目标内存上下文是相同的模块列表中找到的第一个内存上下文。

`CONTEXT_SAME_PROCESS`\
在与目标内存上下文相同的进程列表中找到的第一个内存上下文。

## <a name="remarks"></a>备注
作为参数传递[比较](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)方法。

这些值用于满足指定的比较条件列表中找到的第一个内存上下文。 内存上下文提供一系列内存上下文来比较本身对通过`IDebugMemoryContext2::Compare`方法。 为其所比较运算符列表中的第一个内存上下文`true`然后返回。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Compare](../../../extensibility/debugger/reference/idebugmemorycontext2-compare.md)
