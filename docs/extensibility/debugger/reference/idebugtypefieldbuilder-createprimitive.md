---
title: IDebugTypeFieldBuilder::CreatePrimitive |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- CreatePrimitive
- IDebugTypeFieldBuilder::CreatePrimitive
ms.assetid: 512c6ff0-97c5-409f-939f-4cc969bc4bb9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 08394a62dc115f7bade9c417b8e39ba6b41eeb1b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319852"
---
# <a name="idebugtypefieldbuildercreateprimitive"></a>IDebugTypeFieldBuilder::CreatePrimitive
创建表示基元类型的对象。

## <a name="syntax"></a>语法

```cpp
HRESULT CreatePrimitive (
   DWORD          dwElementType,
   IDebugField ** pTypeField
);
```

```csharp
int CreatePrimitive (
   uint            dwElementType,
   out IDebugField pTypeField
);
```

## <a name="parameters"></a>参数
`dwElementType`\
[in]值从[CorElementType 枚举](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration)表示基元类型。

`pTypeField`\
[out]返回新类型的 IDebugField 接口。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)