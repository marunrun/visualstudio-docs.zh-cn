---
title: IDebugdisassemblystream2：：寻求 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Seek
helpviewer_keywords:
- IDebugDisassemblyStream2::Seek
ms.assetid: afec3008-b1e0-4803-ad24-195dbfb6497e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4954b3b278b3c7a6b798a4ffda3856ab8bb200c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732082"
---
# <a name="idebugdisassemblystream2seek"></a>IDebugDisassemblyStream2::Seek
相对于指定位置，在拆解流中移动读取指针的给定指令数。

## <a name="syntax"></a>语法

```cpp
HRESULT Seek( 
   SEEK_START          dwSeekStart,
   IDebugCodeContext2* pCodeContext,
   UINT64              uCodeLocationId,
   INT64               iInstructions
);
```

```csharp
int Seek( 
   enum_SEEK_START    dwSeekStart,
   IDebugCodeContext2 pCodeContext,
   ulong              uCodeLocationId,
   long               iInstructions
);
```

## <a name="parameters"></a>参数
`dwSeekStart`\
[在][SEEK_START](../../../extensibility/debugger/reference/seek-start.md)枚举中的值，用于指定开始寻价过程的相对位置。

`pCodeContext`\
[在][IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象表示查找操作相对于的代码上下文。 仅当 使用 时，`dwSeekStart` = `SEEK_START_CODECONTEXT`才使用此参数。否则，将忽略此参数，并且可以是 null 值。

`uCodeLocationId`\
[在]查找操作相对于的代码位置标识符。 `dwSeekStart` = 此`SEEK_START_CODELOCID`参数用于否则，将忽略此参数，并可以设置为 0。 有关代码位置标识符的说明，请参阅[GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)方法的备注部分。

`iInstructions`\
[在]相对于 中`dwSeekStart`指定的位置移动的指令数。 此值可以是负值，以便向后移动。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 如果`S_FALSE`寻用位置超出可用指令列表的点，则返回。 否则，返回错误代码。

## <a name="remarks"></a>备注
 如果搜索位于列表开头之前的位置，则读取位置将设置为列表中的第一个指令。 如果 see 位于列表末尾之后的位置，则读取位置将设置为列表中的最后一个指令。

## <a name="see-also"></a>请参阅
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [SEEK_START](../../../extensibility/debugger/reference/seek-start.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)
