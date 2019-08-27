---
title: IDebugMethodField::EnumAllLocals |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumAllLocals
helpviewer_keywords:
- IDebugMethodField::EnumAllLocals method
ms.assetid: 0bc7cc13-2628-4bd8-8c06-4d2aa6755ea8
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd0bc879cccf2bc806d73bfac47bc4795749e0cf
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346945"
---
# <a name="idebugmethodfieldenumalllocals"></a>IDebugMethodField::EnumAllLocals
创建方法，包括那些由编译器在内部生成的所有局部变量的枚举器。

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
[in][IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象，表示指向特定作用域或上下文的方法中的调试地址。

`ppLocals`\
[out]返回[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象，表示指定范围内的所有局部变量的列表; 否则，返回 null 值，该值指示没有局部变量。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK 或如果没有局部变量，则返回 S_FALSE。 否则，返回错误代码。

## <a name="remarks"></a>备注
 将枚举中仅包含给定的调试地址块中定义的变量。 此方法包括任何编译器生成的局部变量。 如果所需的所有源，调用中显式定义的局部变量[EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)方法。

 一种方法可以包含多个作用域的上下文或块。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)