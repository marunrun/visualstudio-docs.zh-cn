---
title: METADATA_ADDRESS_RETVAL |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_RETVAL
helpviewer_keywords:
- METADATA_ADDRESS_RETVAL structure
ms.assetid: 5b0ec0fb-84b3-4ce7-8e24-becf3d881d7d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f2437d10078eb623e063b3292d96ef9bb4a9cf64
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714277"
---
# <a name="metadata_address_retval"></a>METADATA_ADDRESS_RETVAL
此结构表示方法或函数的返回值。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagMETADATA_ADDRESS_RETVAL {
   _mdToken tokMethod;
   DWORD    dwCorType;
   DWORD    dwSigSize;
   BYTE     rgSig[10];
} METADATA_ADDRESS_RETVAL;
```

```csharp
public struct METADATA_ADDRESS_RETVAL {
   public int    tokMethod;
   public uint   dwCorType;
   public uint   dwSigSize;
   public byte[] rgSig;
}
```

## <a name="members"></a>成员
 `tokMethod`\
 此返回值所针对的方法的 ID。

 `dwCorType`\
 返回值的基本类型。 这是 .NET 框架`CorElementType`SDK corhdr.h 文件中定义的枚举中的值。

 `dwSigSize`\
 返回值签名的大小（存储在 中`rgSig`）。

 `rgSig`\
 组成返回值签名的字节数组。

## <a name="remarks"></a>备注
 当`DEBUG_ADDRESS_UNION``ADDRESS_KIND_RETVAL`结构字段设置为[（ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举中[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)的值）时，`dwKind`此结构是DEBUG_ADDRESS_UNION结构中的联合的一部分。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
