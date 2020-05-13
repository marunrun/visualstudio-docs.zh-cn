---
title: METADATA_ADDRESS_PARAM |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_PARAM
helpviewer_keywords:
- METADATA_ADDRESS_PARAM structure
ms.assetid: 90904f19-0e71-4cb3-a56e-6a2e92f66dfc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a0319cfc6f2be817a25126e67cdc470bc727a4ca
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714442"
---
# <a name="metadata_address_param"></a>METADATA_ADDRESS_PARAM
此结构表示方法或函数的参数。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagMETADATA_ADDRESS_PARAM {
   _mdToken tokMethod;
   _mdToken tokParam;
   DWORD    dwIndex;
} METADATA_ADDRESS_PARAM;
```

```csharp
public struct METADATA_ADDRESS_PARAM {
   public int  tokMethod;
   public int  tokParam;
   public uint dwIndex;
}
```

## <a name="members"></a>成员
 `tokMethod`\
 参数为之一的方法的 ID。

 `tokParam`\
 参数的 ID。

 `dwIndex`\
 参数列表中的参数索引。

## <a name="remarks"></a>备注
 当`DEBUG_ADDRESS_UNION``ADDRESS_KIND_PARAM`结构字段设置为[（ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举中[DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)的值）时，`dwKind`此结构是DEBUG_ADDRESS_UNION结构中的联合的一部分。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
