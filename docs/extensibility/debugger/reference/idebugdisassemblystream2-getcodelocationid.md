---
title: IDebugdisassemblystream2：：获取代码定位Id |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeLocationId
ms.assetid: 567adfb8-2f54-499a-a027-e4ecb82277ef
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 32be70e11776177a0e68f09689c2262497703ab1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732250"
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
[在]要转换为标识符的[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)对象。

`puCodeLocationId`[出]返回代码位置标识符。 请参阅“备注”。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。 如果`E_CODE_CONTEXT_OUT_OF_SCOPE`代码上下文有效但超出范围，请返回。

## <a name="remarks"></a>备注
 代码位置标识符特定于支持拆卸的调试引擎 （DE）。 此位置标识符由 DE 在内部用于跟踪代码中的位置，通常是某种地址或偏移量。 唯一的要求是，如果一个位置的代码上下文小于另一个位置的代码上下文，则第一个代码上下文的相应代码位置标识符也必须小于第二个代码上下文的代码位置标识符。

 若要检索代码位置标识符的代码上下文，请调用[GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodecontext.md)
