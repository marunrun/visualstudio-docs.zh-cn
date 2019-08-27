---
title: IDebugTypeFieldBuilder::CreatePointerToType | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- CreatePointerToType
- IDebugTypeFieldBuilder::CreatePointerToType
ms.assetid: 73966e8a-b643-43e0-9b4e-0aa4b402ebbe
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b8947090c56376b03da83cfd81296604b6bd642a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319907"
---
# <a name="idebugtypefieldbuildercreatepointertotype"></a>IDebugTypeFieldBuilder::CreatePointerToType
创建为指定类型的指针。

## <a name="syntax"></a>语法

```cpp
HRESULT CreatePointerToType(
   IDebugField*  pTypeField,
   IDebugField** pPtrToTypeField
);
```

```csharp
int CreatePointerToType(
   IDebugField     pTypeField,
   out IDebugField pPtrToTypeField
);
```

## <a name="parameters"></a>参数
`pTypeField`\
[in]若要指向的类型。 表示由[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)接口。

`pPtrToTypeField`\
[out]返回表示由一个新的指针**IDebugField**对象。

## <a name="return-value"></a>返回值
 如果成功，则返回`S_OK`; 否则为返回错误代码。

## <a name="see-also"></a>请参阅
- [IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)