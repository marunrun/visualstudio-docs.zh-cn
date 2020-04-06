---
title: DOCCONTEXT_COMPARE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DOCCONTEXT_COMPARE
helpviewer_keywords:
- DOCCONTEXT_COMPARE enumeration
ms.assetid: ed947c34-b07e-4b69-8381-b6e7cb842862
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 75e4453cae63f484961cb2d0f3385a703709f83b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737230"
---
# <a name="doccontext_compare"></a>DOCCONTEXT_COMPARE
指定比较两个文档上下文的条件。

## <a name="syntax"></a>语法

```cpp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
typedef DWORD DOCCONTEXT_COMPARE;
```

```csharp
enum enum_DOCCONTEXT_COMPARE {
    DOCCONTEXT_EQUAL         = 0x0001,
    DOCCONTEXT_LESS_THAN     = 0x0002,
    DOCCONTEXT_GREATER_THAN  = 0x0003,
    DOCCONTEXT_SAME_DOCUMENT = 0x0004
};
```

## <a name="fields"></a>字段
`DOCCONTEXT_EQUAL`\
查找列表中与目标文档上下文相等的第一个文档上下文。

`DOCCONTEXT_LESS_THAN`\
查找列表中的第一个小于目标文档上下文的文档上下文。

`DOCCONTEXT_GREATER_THAN`\
查找列表中大于目标文档上下文的第一个文档上下文。

`DOCCONTEXT_SAME_DOCUMENT`\
查找列表中与目标文档上下文位于同一文档中的第一个文档上下文。

## <a name="remarks"></a>备注
作为参数传递给[比较](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)方法。

这些值用于指定查找列表中的第一个文档上下文的比较条件。 文档上下文将给出文档上下文的列表，以便通过 方法`IDebugDocumentContext2::Compare`比较自身。 然后返回列表中的第一个文档上下文，`true`然后返回比较运算符。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [比较](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)
