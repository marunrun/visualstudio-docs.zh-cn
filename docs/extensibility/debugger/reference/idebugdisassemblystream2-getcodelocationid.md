---
title: IDebugDisassemblyStream2::GetCodeLocationId |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
ms.assetid: 567adfb8-2f54-499a-a027-e4ecb82277ef
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 58e3b12ecbc75b7d07d60ac399412dc5b0deb73b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351683"
---
# <a name="idebugdisassemblystream2getcodelocationid"></a>IDebugDisassemblyStream2::GetCodeLocationId
返回特定代码上下文的代码位置标识符。

## <a name="syntax"></a>语法

```cpp
HRESULT GetCodeLocationId( 
   IDebugCodeContext2* pCodeContext,
   UINT64*             puCodeLocationId
);
```

```csharp
int GetCodeLocationId( 
   IDebugCodeContext2 pCodeContext,
   out ulong          puCodeLocationId
);
```

## <a name="parameters"></a>参数
`pCodeContext`\
[in][IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象要转换为标识符。

`puCodeLocationId` [out]返回的代码位置标识符。 请参阅“备注”。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。 返回`E_CODE_CONTEXT_OUT_OF_SCOPE`代码上下文是否有效，但作用域之外。

## <a name="remarks"></a>备注
 代码位置标识符是特定于调试引擎 (DE) 支持反汇编。 此位置标识符由在内部用于 DE 跟踪代码中的位置，通常是地址或某种类型的偏移量。 唯一要求是，如果代码上下文的一个位置小于另一个位置的代码上下文则相应的代码位置标识符的第一个代码上下文也必须是小于第二个代码上下文的代码位置标识符。

 若要检索的代码位置标识符代码上下文，请调用[GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)