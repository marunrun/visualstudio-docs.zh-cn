---
title: IDebugMethodfield：：EnumAllLocals |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumAllLocals
helpviewer_keywords:
- IDebugMethodField::EnumAllLocals method
ms.assetid: 0bc7cc13-2628-4bd8-8c06-4d2aa6755ea8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 50da5af616c56276a0299a0d08e6eeb0b88181cc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727342"
---
# <a name="idebugmethodfieldenumalllocals"></a>IDebugMethodField::EnumAllLocals
为方法的所有局部变量创建枚举器，包括编译器内部生成的变量。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumAllLocals( 
   IDebugAddress*     pAddress,
   IEnumDebugFields** ppLocals
);
```

```csharp
int EnumAllLocals(
   IDebugAddress        pAddress,
   out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>参数
`pAddress`\
[在][IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象表示方法中的调试地址，指向特定范围或上下文。

`ppLocals`\
[出]返回表示指定作用域中所有局部变量列表的[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象;否则，返回一个 null 值，指示没有局部变量。

## <a name="return-value"></a>返回值
 如果成功，则返回S_OK或返回S_FALSE如果没有局部变量。 否则，返回错误代码。

## <a name="remarks"></a>备注
 仅枚举在包含给定调试地址的块中定义的变量。 此方法包括任何编译器生成的局部变量。 如果所需的全部是源中显式定义的局部变量，请调用[EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)方法。

 方法可以包含多个范围上下文或块。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)
