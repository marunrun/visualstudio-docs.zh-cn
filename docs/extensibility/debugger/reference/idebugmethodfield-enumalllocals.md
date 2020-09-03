---
title: IDebugMethodField：： EnumAllLocals |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727342"
---
# <a name="idebugmethodfieldenumalllocals"></a>IDebugMethodField::EnumAllLocals
创建方法的所有局部变量的枚举数，包括编译器在内部生成的变量。

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
中 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) 对象，表示方法中的调试地址，指向特定范围或上下文。

`ppLocals`\
弄返回一个 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) 对象，该对象表示指定范围内的所有局部变量的列表;否则，返回 null 值，指示没有局部变量。

## <a name="return-value"></a>返回值
 如果成功，则返回 S_OK 或返回 S_FALSE （如果没有局部变量）。 否则，返回错误代码。

## <a name="remarks"></a>备注
 仅枚举包含给定调试地址的块中定义的变量。 此方法包含编译器生成的任何局部变量。 如果所需的全部都是在源中显式定义的局部变量，请调用 [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md) 方法。

 一个方法可以包含多个范围上下文或块。

## <a name="see-also"></a>另请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumlocals.md)
