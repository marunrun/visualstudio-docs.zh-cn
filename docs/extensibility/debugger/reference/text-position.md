---
title: TEXT_POSITION |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TEXT_POSITION
helpviewer_keywords:
- TEXT_POSITION structure
ms.assetid: 6dcec574-a852-49fa-8c2e-2e71cbb5e3c6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1a36c585a09afbd1dec60e1d4399dca258399ae3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80713415"
---
# <a name="text_position"></a>TEXT_POSITION
描述给定文本中的行和列的位置。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagTEXT_POSITION { 
   DWORD dwLine;
   DWORD dwColumn;
} TEXT_POSITION;
```

```csharp
public struct TEXT_POSITION { 
   public uint dwLine;
   public uint dwColumn;
};
```

## <a name="members"></a>成员

`dwLine`\
源文件中的行的索引。

`dwColumn`\
行的字符偏移量。

## <a name="remarks"></a>备注

此结构用于 [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md) 和 [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md) 结构。

通过调用以下方法填充此结构：

- [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)

- [GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)

- [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)

- [GetOffset](../../../extensibility/debugger/reference/idebugfunctionposition2-getoffset.md)

此结构作为参数传递给以下方法：

- [GetText](../../../extensibility/debugger/reference/idebugdocumenttext2-gettext.md)

- [onInsertText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-oninserttext.md)

- [onRemoveText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onremovetext.md)

- [onReplaceText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onreplacetext.md)

- [onUpdateTextAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatetextattributes.md)

## <a name="requirements"></a>要求

 标头： msdbg

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)
- [GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)
- [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)
- [GetOffset](../../../extensibility/debugger/reference/idebugfunctionposition2-getoffset.md)
- [GetText](../../../extensibility/debugger/reference/idebugdocumenttext2-gettext.md)
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
