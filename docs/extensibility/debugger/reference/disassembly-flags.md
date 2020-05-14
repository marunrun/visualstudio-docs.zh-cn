---
title: DISASSEMBLY_FLAGS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_FLAGS
helpviewer_keywords:
- DISASSEMBLY_FLAGS enumeration
ms.assetid: c1ec5a4d-5d42-4660-932c-7348550140cb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ba6d9db3ad2cb1f9bbc9e3cea27aba939c6dd499
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737371"
---
# <a name="disassembly_flags"></a>DISASSEMBLY_FLAGS
指定拆卸的标志。

## <a name="syntax"></a>语法

```cpp
enum enum_DISASSEMBLY_FLAGS {
    DF_DOCUMENTCHANGE     = 0x00000001,
    DF_DISABLED           = 0x00000002,
    DF_INSTRUCTION_ACTIVE = 0x00000004,
    DF_DATA               = 0x00000008,
    DF_HASSOURCE          = 0x00000010,
    DF_DOCUMENT_CHECKSUM  = 0x00000020
};
typedef DWORD DISASSEMBLY_FLAGS;
```

```csharp
public enum enum_DISASSEMBLY_FLAGS {
    DF_DOCUMENTCHANGE     = 0x00000001,
    DF_DISABLED           = 0x00000002,
    DF_INSTRUCTION_ACTIVE = 0x00000004,
    DF_DATA               = 0x00000008,
    DF_HASSOURCE          = 0x00000010,
    DF_DOCUMENT_CHECKSUM  = 0x00000020
};
```

## <a name="fields"></a>字段
`DF_DOCUMENTCHANGE`\
指示此指令位于与前一个不同的文档中。

`DF_DISABLED`\
指示此指令不会执行。

`DF_INSTRUCTION_ACTIVE`\
指示此指令是要执行的下一个指令之一（可能有多个指令）。

`DF_DATA`\
指示此指令实际上是数据（不是代码）。

`DF_HASSOURCE`\
指示此指令具有源。 某些说明（如分析代码或垃圾回收代码）没有相应的源。

`DF_DOCUMENT_CHECKSUM`\
指示`bstrDocumentUrl`字段包含文档 URL 之后的校验和数据。 有关如何存储校验和数据的，请参阅["拆解数据](../../../extensibility/debugger/reference/disassemblydata.md)结构的备注"部分。

## <a name="remarks"></a>备注
用作`dwFlags`[拆解数据](../../../extensibility/debugger/reference/disassemblydata.md)结构的成员。

这些标志可以稍微结合`OR`。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
