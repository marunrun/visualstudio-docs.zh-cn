---
title: IDebugPointer对象：：设置字节 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::SetBytes
helpviewer_keywords:
- IDebugPointerObject::SetBytes method
ms.assetid: 8c578b38-38d7-46f3-bb2e-8a730fccd334
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dede3ee5291afbfbeab4d6e60dcbd56e205e4526
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725504"
---
# <a name="idebugpointerobjectsetbytes"></a>IDebugPointerObject::SetBytes
设置从一系列连续字节指向的值。

## <a name="syntax"></a>语法

```cpp
HRESULT SetBytes( 
   DWORD  dwStart,
   DWORD  dwCount,
   BYTE*  pBytes,
   DWORD* pdwBytes
);
```

```csharp
int SetBytes(
   uint     dwStart,
   uint     dwCount,
   byte[]   pBytes,
   out uint pdwBytes
);
```

## <a name="parameters"></a>参数
`dwStart`\
[在]从对象开头指向的偏移（以字节为单位）。

`dwCount`\
[在]要设置的字节数。

`pBytes`\
[在]表示新值的字节数组。 此值存储在对象中，从给定偏移量开始。

`pdwBytes`\
[出]返回实际设置的字节数。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 如果此[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)表示的指针指向基元类型或基元类型的简单数组（即可以由字节的简单序列表示的数组），则使用此方法。 此`IDebugPointerObject`对象不能为空引用（它必须指向内存中的地址）。

## <a name="see-also"></a>请参阅
- [GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
