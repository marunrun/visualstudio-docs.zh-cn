---
title: DEBUG_ADDRESS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS
helpviewer_keywords:
- DEBUG_ADDRESS structure
ms.assetid: 79f5e765-9aac-4b6e-82ef-bed88095e9ba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fe778ba3ed80930a4cd7b4fa1170f286b3ccf6ec
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737521"
---
# <a name="debug_address"></a>DEBUG_ADDRESS
此结构表示地址。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagDEBUG_ADDRESS {
    ULONG32             ulAppDomainID;
    GUID                guidModule;
    _mdToken            tokClass;
    DEBUG_ADDRESS_UNION addr;
} DEBUG_ADDRESS;
```

```csharp
public struct DEBUG_ADDRESS {
    public uint                ulAppDomainID;
    public Guid                guidModule;
    public int                 tokClass;
    public DEBUG_ADDRESS_UNION addr;
}
```

## <a name="members"></a>成员
`ulAppDomainID`\
进程 ID。

`guidModule`\
包含此地址的模块的 GUID。

`tokClass`\
标识此地址的类或类型的令牌。

> [!NOTE]
> 此值特定于符号提供程序，因此除了作为类类型的标识符之外，没有一般含义。

`addr`\
[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)结构，其中包含描述各个地址类型的结构联合。 值`addr`。`dwKind` 来自[ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举，它解释了如何解释联合。

## <a name="remarks"></a>备注
此结构传递给要填充的[GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)方法。

**警告 [仅限C++]**

如果`addr.dwKind`为`ADDRESS_KIND_METADATA_LOCAL`，如果不是`addr.addr.addrLocal.pLocal`空值，则必须调用`Release`令牌指针：

```
if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL && addr.addr.addrLocal.pLocal != NULL)
{
    addr.addr.addrLocal.pLocal->Release();
}
```

## <a name="requirements"></a>要求
标题： sh.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [获取地址](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
