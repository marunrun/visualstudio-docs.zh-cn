---
title: IDebugDisassemblyStream2::Seek |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Seek
helpviewer_keywords:
- IDebugDisassemblyStream2::Seek
ms.assetid: afec3008-b1e0-4803-ad24-195dbfb6497e
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e97da5b4b65b18c9d4c745dea2cb5f0915862731
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310371"
---
# <a name="idebugdisassemblystream2seek"></a>IDebugDisassemblyStream2::Seek
将读取的指针移动反汇编流给定数量的相对于指定位置的说明中。

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
[in]中的值[SEEK_START](../../../extensibility/debugger/reference/seek-start.md)枚举，用于指定开始查找过程的相对位置。

`pCodeContext`\
[in][IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象，表示查找操作是相对于代码上下文。 仅当使用此参数`dwSeekStart`  =  `SEEK_START_CODECONTEXT`; 否则为此参数将被忽略并且可以为 null 值。

`uCodeLocationId`\
[in]查找操作是相对于代码位置标识符。 如果使用此参数`dwSeekStart`  =  `SEEK_START_CODELOCID`; 否则为此参数将被忽略，可以设置为 0。 请参阅备注部分[GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)方法有关的代码位置标识符的说明。

`iInstructions`\
[in]要移动相对于指定的位置的指令数`dwSeekStart`。 此值可以是负数，以向后移动。

## <a name="return-value"></a>返回值
 如果成功，则返回 `S_OK`。 返回`S_FALSE`如果搜寻位置到可用的指令的一个点，该列表。 否则，返回错误代码。

## <a name="remarks"></a>备注
 如果搜索到列表的开头之前位置，读取的位置设置为列表中的第一个指令。 如果看到的是将其置于列表末尾之后，读取的位置设置的最后一个指令列表中。

## <a name="see-also"></a>请参阅
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [SEEK_START](../../../extensibility/debugger/reference/seek-start.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)