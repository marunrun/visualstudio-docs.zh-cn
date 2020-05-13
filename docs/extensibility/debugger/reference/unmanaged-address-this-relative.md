---
title: UNMANAGED_ADDRESS_THIS_RELATIVE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- UNMANAGED_ADDRESS_THIS_RELATIVE
helpviewer_keywords:
- UNMANAGED_ADDRESS_THIS_RELATIVE structure
ms.assetid: e6a91ace-2d47-4ff9-aefb-8d8b68eab0b2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ea493170c7b422129485fcea4248981a2b506001
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713257"
---
# <a name="unmanaged_address_this_relative"></a>UNMANAGED_ADDRESS_THIS_RELATIVE
此结构表示相对于`this`指针（`Me`在可视化基本中）的地址。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagUNMANAGED_THIS_RELATIVE {
   DWORD dwOffset;
   DWORD dwBitOffset;
   DWORD dwBitLength;
} UNMANAGED_ADDRESS_THIS_RELATIVE;
```

```csharp
public struct UNMANAGED_THIS_RELATIVE {
   public uint dwOffset;
   public uint dwBitOffset;
   public uint dwBitLength;
}
```

## <a name="members"></a>成员
 `dwOffset`\
 与基本位置的字节偏移量（例如，类 vtable 的开头）。

 `dwBitOffset`\
 与基位的偏移（始终为 0，除非引用位字段）。

 `dwBitLength`\
 表示地址的位数（除非引用位字段，否则始终为 0）。

## <a name="remarks"></a>备注
 当`DEBUG_ADDRESS_UNION``ADDRESS_KIND_UNMANAGED_THIS_RELATIVE`结构字段设置为[（ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举中[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)的值）时，`dwKind`此结构是DEBUG_ADDRESS_UNION结构中的联合的一部分。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
