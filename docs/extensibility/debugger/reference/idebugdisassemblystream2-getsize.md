---
title: IDebugDisassemblyStream2::GetSize |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetSize
helpviewer_keywords:
- IDebugDisassemblyStream2::GetSize
ms.assetid: 8f512704-12d0-46d2-959a-4f8dffe117b5
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: cb13ac24aaa542d3111ff3480ac340615226a0a7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66310416"
---
# <a name="idebugdisassemblystream2getsize"></a>IDebugDisassemblyStream2::GetSize
获取此反汇编流的说明中的大小。

## <a name="syntax"></a>语法

```cpp
HRESULT GetSize( 
   UINT64* pnSize
);
```

```csharp
int GetSize( 
   out ulong pnSize
);
```

## <a name="parameters"></a>参数
`pnSize`\
[out]返回的大小，以说明。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="remarks"></a>备注
 此方法返回的值可用于分配的数组[DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)结构随后将传递到[读取](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
- [Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)