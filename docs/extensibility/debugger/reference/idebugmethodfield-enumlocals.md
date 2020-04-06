---
title: IDebugMethodfield：：枚举本地人 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::EnumLocals
helpviewer_keywords:
- IDebugMethodField::EnumLocals method
ms.assetid: b0456a6d-2b96-49e2-a871-516571b4f6a5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 08872160860d0d442f9807705dea70190dff9b28
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727201"
---
# <a name="idebugmethodfieldenumlocals"></a>IDebugMethodField::EnumLocals
为方法的选定局部变量创建枚举器。

## <a name="syntax"></a>语法

```cpp
HRESULT EnumLocals(
    IDebugAddress*     pAddress,
    IEnumDebugFields** ppLocals
);
```

```csharp
int EnumLocals(
    IDebugAddress        pAddress,
    out IEnumDebugFields ppLocals
);
```

## <a name="parameters"></a>参数
`pAddress`\
[在][IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)对象，表示选择从中获取局部变量的上下文或作用域的调试地址。

`ppLocals`\
[出]返回表示局部变量列表的[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)对象;否则，如果没有局部变量，则返回 null 值。

## <a name="return-value"></a>返回值
如果成功，则返回S_OK或返回S_FALSE如果没有局部变量。 否则，返回错误代码。

## <a name="remarks"></a>备注
仅枚举在包含给定调试地址的块中定义的变量。 如果需要所有局部变量（包括任何编译器生成的局部变量），请调用[EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)方法。

方法可以包含多个范围上下文或块。 例如，以下精心设计的方法包含三个作用域，两个内部块和方法体本身。

```csharp
public void func(int index)
{
    // Method body scope
    int a = 0;
    if (index == 1)
    {
        // Inner scope 1
        int temp1 = a;
    }
    else
    {
        // Inner scope 2
        int temp2 = a;
    }
}
```

[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)对象表示`func`方法本身。 例如，`EnumLocals`使用[IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)设置为`Inner Scope 1`地址调用方法将返回包含变量的`temp1`枚举。

## <a name="see-also"></a>请参阅
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)
