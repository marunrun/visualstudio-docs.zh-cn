---
title: IDebugPointerObject::GetBytes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::GetBytes
helpviewer_keywords:
- IDebugPointerObject::GetBytes method
ms.assetid: e986c188-87fb-4b51-86e9-ee6a0035bdab
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 247e1ff4c934ae581c7a0224c8f8cba8d4e9d946
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66308870"
---
# <a name="idebugpointerobjectgetbytes"></a>IDebugPointerObject::GetBytes
获取指向作为一系列连续字节的值。

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
[in]偏移量，以字节为单位，从一开始指向的对象。

`dwCount`\
[in]要检索的字节数。

`pBytes`\
[in、 out]指向填充为值为一系列连续字节的数组，该对象从给定的偏移量开始。

`pdwBytes`\
[out]返回实际检索的字节的数。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK;否则，返回错误代码。

## <a name="remarks"></a>备注
 如果使用此方法的指针表示由此[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)指向基元类型或基元类型 （即，可以通过简单的字节序列表示一个数组） 的简单数组。

## <a name="see-also"></a>请参阅
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
- [SetBytes](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)