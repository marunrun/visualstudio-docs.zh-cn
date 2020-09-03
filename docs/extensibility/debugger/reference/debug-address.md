---
title: DEBUG_ADDRESS |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
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
标识此地址的类或类型的标记。

> [!NOTE]
> 此值特定于符号提供程序，因此除了作为类类型的标识符外，没有任何常规含义。

`addr`\
一个 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 结构，它包含描述各个地址类型的结构的并集。 值 `addr` 。`dwKind` 来自 [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 枚举，该枚举说明了如何解释联合。

## <a name="remarks"></a>备注
此结构传递到要填写的 [GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md) 方法。

**警告 [仅 c + +]**

如果 `addr.dwKind` 为，并且不是 `ADDRESS_KIND_METADATA_LOCAL` `addr.addr.addrLocal.pLocal` null 值，则必须 `Release` 对标记指针调用：

```
if (addr.dwKind == ADDRESS_KIND_METADATA_LOCAL && addr.addr.addrLocal.pLocal != NULL)
{
    addr.addr.addrLocal.pLocal->Release();
}
```

## <a name="requirements"></a>要求
标头： sh。h

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [获取地址](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
