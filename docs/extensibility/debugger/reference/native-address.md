---
title: NATIVE_ADDRESS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- NATIVE_ADDRESS
helpviewer_keywords:
- NATIVE_ADDRESS structure
ms.assetid: 7a0cd085-bfc8-45cc-a3d4-4459070e207a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7c62bbea846f3d486ead8add4dfab2182df1e1bb
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714331"
---
# <a name="native_address"></a>NATIVE_ADDRESS

此结构表示本机地址。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagNATIVE_ADDRESS {
    DWORD unknown;
} NATIVE_ADDRESS;
```

```csharp
public struct NATIVE_ADDRESS {
    public uint unknown;
}
```

## <a name="members"></a>成员

`unknown`\
本机地址（其含义取决于运行时和操作系统）。

## <a name="remarks"></a>备注

当`DEBUG_ADDRESS_UNION``ADDRESS_KIND_NATIVE`结构字段设置为[（ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举中[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)的值）时，`dwKind`此结构是DEBUG_ADDRESS_UNION结构中的联合的一部分。

## <a name="requirements"></a>要求

标题： sh.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
