---
title: IDebugdisassemblystream2：：阅读 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Read
helpviewer_keywords:
- IDebugDisassemblyStream2::Read
ms.assetid: 7db5f6bb-73ee-45bc-b187-c1b6aa2dfdd5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4a4f5c0250405c2e2a0314b52c4cbc64d749fc0a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732091"
---
# <a name="idebugdisassemblystream2read"></a>IDebugDisassemblyStream2::Read
读取从拆解流中的当前位置开始的指令。

## <a name="syntax"></a>语法

```cpp
HRESULT Read( 
   DWORD                     dwInstructions,
   DISASSEMBLY_STREAM_FIELDS dwFields,
   DWORD*                    pdwInstructionsRead,
   DisassemblyData*          prgDisassembly
);
```

```csharp
int Read( 
   uint                           dwInstructions,
   enum_DISASSEMBLY_STREAM_FIELDS dwFields,
   out uint                       pdwInstructionsRead,
   DisassemblyData[]              prgDisassembly
);
```

## <a name="parameters"></a>参数
`dwInstructions`\
[在]要拆卸的说明数。 此值也是`prgDisassembly`数组的最大长度。

`dwFields`\
[在][DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)枚举中的标志的组合，指示要填写的`prgDisassembly`字段。

`pdwInstructionsRead`\
[出]返回实际拆解的说明数。

`prgDisassembly`\
[出]一系列用拆解代码填充[的拆解数据](../../../extensibility/debugger/reference/disassemblydata.md)结构，每个拆解指令一个结构。 此数组的长度由`dwInstructions`参数决定。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 可通过调用[GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)方法获取当前作用域中可用的最大指令数。

 可以通过调用[Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)方法更改读取下一个指令的当前位置。

 可以将`DSF_OPERANDS_SYMBOLS`标志添加到参数中`DSF_OPERANDS`的标志中`dwFields`，以指示在拆解指令时应使用符号名称。

## <a name="see-also"></a>请参阅
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)
- [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)
