---
title: IDebugDisassemblyStream2::Read |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Read
helpviewer_keywords:
- IDebugDisassemblyStream2::Read
ms.assetid: 7db5f6bb-73ee-45bc-b187-c1b6aa2dfdd5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c74ed1de1d12cc7384ee8f7d27dad910c7b9c9d5
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310357"
---
# <a name="idebugdisassemblystream2read"></a>IDebugDisassemblyStream2::Read
读取从当前位置反汇编流中的说明。

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
[in]要拆装的指令数。 此值也是最大长度`prgDisassembly`数组。

`dwFields`\
[in]中的标志的组合[DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)枚举，用于指示哪些字段的`prgDisassembly`要填写。

`pdwInstructionsRead`\
[out]返回实际拆装的指令的数。

`prgDisassembly`\
[out]一个数组[DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)填充反汇编代码，每个已拆装的指令的一个结构的结构。 此数组的长度由`dwInstructions`参数。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 可以通过调用获取当前作用域中时所提供的说明的最大数目[GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)方法。

 可以通过调用更改的当前位置读取下一个指令是所在[Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)方法。

 `DSF_OPERANDS_SYMBOLS`标志可添加到`DSF_OPERANDS`标记中`dwFields`参数以指示应在拆装说明时使用的符号名称。

## <a name="see-also"></a>请参阅
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [GetSize](../../../extensibility/debugger/reference/idebugdisassemblystream2-getsize.md)
- [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)