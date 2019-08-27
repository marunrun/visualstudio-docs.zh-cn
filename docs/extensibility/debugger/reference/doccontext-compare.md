---
title: DOCCONTEXT_COMPARE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DOCCONTEXT_COMPARE
helpviewer_keywords:
- DOCCONTEXT_COMPARE enumeration
ms.assetid: ed947c34-b07e-4b69-8381-b6e7cb842862
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f31b33eeb782e71a87103d26a3bb78175611644e
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318143"
---
# <a name="doccontextcompare"></a>DOCCONTEXT_COMPARE
指定用于比较两个文档上下文的条件。

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
在列表中，它等于目标文档上下文中找到的第一个文档上下文。

`DOCCONTEXT_LESS_THAN`\
小于目标文档上下文在列表中找到的第一个文档上下文。

`DOCCONTEXT_GREATER_THAN`\
大于目标文档上下文在列表中找到的第一个文档上下文。

`DOCCONTEXT_SAME_DOCUMENT`\
在目标文档上下文与在同一文档中的列表中找到的第一个文档上下文。

## <a name="remarks"></a>备注
作为参数传递[比较](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)方法。

这些值用于指定用于在列表中查找第一个文档上下文比较条件。 文档上下文提供的文档上下文列表来比较本身对通过`IDebugDocumentContext2::Compare`方法。 为其所比较运算符列表中的第一个文档上下文`true`然后返回。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Compare](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)
