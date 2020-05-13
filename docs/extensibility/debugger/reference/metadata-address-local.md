---
title: METADATA_ADDRESS_LOCAL |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_LOCAL
helpviewer_keywords:
- METADATA_ADDRESS_LOCAL structure
ms.assetid: 635f6bc5-c486-4e0e-83db-36f15e543843
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e3adf9ca5f679c7a526f10b1ee6c91d50dac52d2
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714478"
---
# <a name="metadata_address_local"></a>METADATA_ADDRESS_LOCAL

此结构表示作用域（通常是函数或方法）中的局部变量的地址。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagMETADATA_ADDRESS_LOCAL {
    _mdToken  tokMethod;
    IUnknown* pLocal;
    DWORD     dwIndex;
} METADATA_ADDRESS_LOCAL;
```

```csharp
public struct METADATA_ADDRESS_LOCAL {
    public int    tokMethod;
    public object pLocal;
    public uint   dwIndex;
}
```

## <a name="members"></a>成员

`tokMethod`\
本地变量的一部分的方法或函数的 ID。

[C++]`_mdToken`是`typedef`32 位`int`的 。

`pLocal`\
此结构表示的地址的令牌。

`dwIndex`\
可以是方法或函数中此局部变量的索引，也可以是其他一些值（特定于语言） 的索引。

## <a name="remarks"></a>备注

当`DEBUG_ADDRESS_UNION``ADDRESS_KIND_LOCAL`结构字段设置为[（ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举中[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)的值）时，`dwKind`此结构是DEBUG_ADDRESS_UNION结构中的联合的一部分。

> [!WARNING]
> [仅C++]如果`pLocal`不是 null，则必须调用`Release`令牌指针（`addr`是[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)结构中的字段）：
>
> ```cpp
> if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL && addr.addr.addrLocal.pLocal != NULL)
> {
>     addr.addr.addrLocal.pLocal->Release();
> }
> ```

## <a name="requirements"></a>要求

标题： sh.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
