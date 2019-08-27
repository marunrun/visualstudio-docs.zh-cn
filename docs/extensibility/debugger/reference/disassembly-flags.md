---
title: DISASSEMBLY_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_FLAGS
helpviewer_keywords:
- DISASSEMBLY_FLAGS enumeration
ms.assetid: c1ec5a4d-5d42-4660-932c-7348550140cb
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0160a14a4ad20e7144e48f767fad88951ca1e473
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318392"
---
# <a name="disassemblyflags"></a>DISASSEMBLY_FLAGS
指定反汇编的标志。

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
指示此指令比前一个不同的文档。

`DF_DISABLED`\
指示此指令将不会执行。

`DF_INSTRUCTION_ACTIVE`\
指示此指令是一个要执行的下一步说明 （可能有多个）。

`DF_DATA`\
指示此指令实际上是数据 （而不是代码）。

`DF_HASSOURCE`\
指示此指令具有源。 一些说明，如分析或进行垃圾收集代码中，有没有相应的源。

`DF_DOCUMENT_CHECKSUM`\
指示`bstrDocumentUrl`字段后的文档 URL 包含校验和数据。 请参阅备注部分[DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)校验和数据的存储方式的结构。

## <a name="remarks"></a>备注
用作`dwFlags`的成员[DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)结构。

可能的按位组合这些标志`OR`。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
