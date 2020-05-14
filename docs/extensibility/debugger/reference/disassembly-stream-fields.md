---
title: DISASSEMBLY_STREAM_FIELDS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_STREAM_FIELDS
helpviewer_keywords:
- DISASSEMBLY_STREAM_FIELDS enumeration
ms.assetid: cfc9b4de-c756-4844-bea7-d9f186a51d1b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d10f2143cbefa86442e4087ac098020f5f2bd6ac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737363"
---
# <a name="disassembly_stream_fields"></a>DISASSEMBLY_STREAM_FIELDS
指定要检索的有关拆解字段的信息。

## <a name="syntax"></a>语法

```cpp
enum enum_DISASSEMBLY_STREAM_FIELDS {
    DSF_ADDRESS          = 0x00000001,
    DSF_ADDRESSOFFSET    = 0x00000002,
    DSF_CODEBYTES        = 0x00000004,
    DSF_OPCODE           = 0x00000008,
    DSF_OPERANDS         = 0x00000010,
    DSF_SYMBOL           = 0x00000020,
    DSF_CODELOCATIONID   = 0x00000040,
    DSF_POSITION         = 0x00000080,
    DSF_DOCUMENTURL      = 0x00000100,
    DSF_BYTEOFFSET       = 0x00000200,
    DSF_FLAGS            = 0x00000400,
    DSF_OPERANDS_SYMBOLS = 0x00010000,
    DSF_ALL              = 0x000107ff
};
typedef DWORD DISASSEMBLY_STREAM_FIELDS;
```

```csharp
public enum enum_DISASSEMBLY_STREAM_FIELDS {
    DSF_ADDRESS          = 0x00000001,
    DSF_ADDRESSOFFSET    = 0x00000002,
    DSF_CODEBYTES        = 0x00000004,
    DSF_OPCODE           = 0x00000008,
    DSF_OPERANDS         = 0x00000010,
    DSF_SYMBOL           = 0x00000020,
    DSF_CODELOCATIONID   = 0x00000040,
    DSF_POSITION         = 0x00000080,
    DSF_DOCUMENTURL      = 0x00000100,
    DSF_BYTEOFFSET       = 0x00000200,
    DSF_FLAGS            = 0x00000400,
    DSF_OPERANDS_SYMBOLS = 0x00010000,
    DSF_ALL              = 0x000107ff
};
```

## <a name="fields"></a>字段
`DSF_ADDRESS`\
初始化/使用`bstrAddress`字段。

`DSF_ADDRESSOFFSET`\
初始化/使用`bstrAddressOffset`字段。

`DSF_CODEBYTES`\
初始化/使用`bstrCodeBytes`字段。

`DSF_OPCODE`\
初始化/使用`bstrOpCode`字段。

`DSF_OPERANDS`\
初始化/使用`bstrOperands`字段。

`DSF_SYMBOL`\
初始化/使用`bstrSymbol`字段。

`DSF_CODELOCATIONID`\
初始化/使用`uCodeLocationId`字段。

`DSF_POSITION`\
初始化/使用`posBeg`和`posEnd`字段。

`DSF_DOCUMENTURL`\
初始化/使用`bstrDocumentUrl`字段。

`DSF_BYTEOFFSET`\
初始化/使用`dwByteOffset`字段。

`DSF_FLAGS`\
初始化/使用`dwFlags`（[DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)） 字段。

`DSF_OPERANDS_SYMBOLS`\
在`bstrOperands`字段中包括符号名称。

`DSF_ALL`\
指定拆解流的所有字段。

## <a name="remarks"></a>备注
作为参数传递给[Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)方法，以指示要初始化[拆解数据](../../../extensibility/debugger/reference/disassemblydata.md)结构的哪些字段。

用于`dwFields``DisassemblyData`结构的成员，用于指示在返回结构时使用哪些字段并有效。

这些值可以稍微结合`OR`。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [读取](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
