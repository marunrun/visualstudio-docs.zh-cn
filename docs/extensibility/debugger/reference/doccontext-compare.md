---
title: DOCCONTEXT_COMPARE |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737230"
---
# <a name="doccontext_compare"></a>DOCCONTEXT_COMPARE
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
在列表中查找与目标文档上下文相同的第一个文档上下文。

`DOCCONTEXT_LESS_THAN`\
在列表中查找小于目标文档上下文的第一个文档上下文。

`DOCCONTEXT_GREATER_THAN`\
在列表中查找大于目标文档上下文的第一个文档上下文。

`DOCCONTEXT_SAME_DOCUMENT`\
在与目标文档上下文相同的文档中查找列表中的第一个文档上下文。

## <a name="remarks"></a>备注
作为参数传递给 [Compare](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md) 方法。

这些值用于指定在列表中查找第一个文档上下文的比较条件。 将为文档上下文提供一个文档上下文列表，以通过方法对自身进行比较 `IDebugDocumentContext2::Compare` 。 然后返回该列表中比较运算符所属的第一个文档上下文 `true` 。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [比较](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)
