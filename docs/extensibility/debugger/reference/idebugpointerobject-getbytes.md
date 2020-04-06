---
title: IDebugPointer对象：：获取字节 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::GetBytes
helpviewer_keywords:
- IDebugPointerObject::GetBytes method
ms.assetid: e986c188-87fb-4b51-86e9-ee6a0035bdab
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 17bc39f65d7c4c42b4f958b559df7c5b7d3bbdf7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725514"
---
# <a name="idebugpointerobjectgetbytes"></a>IDebugPointerObject::GetBytes
获取指向的一系列连续字节的值。

## <a name="syntax"></a>语法

```cpp
HRESULT GetBytes( 
   DWORD  dwStart,
   DWORD  dwCount,
   BYTE*  pBytes,
   DWORD* pdwBytes
);
```

```csharp
int GetBytes(
   uint       dwStart,
   uint       dwCount,
   out byte[] pBytes,
   out uint   pdwBytes
);
```

## <a name="parameters"></a>参数
`dwStart`\
[在]从对象开头指向的偏移（以字节为单位）。

`dwCount`\
[在]要检索的字节数。

`pBytes`\
[进出]以一系列连续字节填充该值的数组，从指向的对象的给定偏移开始。

`pdwBytes`\
[出]返回实际检索的字节数。

## <a name="return-value"></a>返回值
 如果成功，返回S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 如果此[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)表示的指针指向基元类型或基元类型的简单数组（即可以由字节的简单序列表示的数组），则使用此方法。

## <a name="see-also"></a>请参阅
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
- [设置字节](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)
