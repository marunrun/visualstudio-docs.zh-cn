---
title: PDB_TYPE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PDB_TYPE
helpviewer_keywords:
- PDB_TYPE structure
ms.assetid: 1c1bb772-77d6-4870-90b2-fd9247d0004e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1f736d7d9b190fc46945e2f4f7c309b88c3e851f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714108"
---
# <a name="pdb_type"></a>PDB_TYPE

此结构指定有关从 PDB 符号获取的字段类型的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagTYPE_PDB {
    ULONG32 ulAppDomainID;
    GUID    guidModule;
    DWORD   symid;
} PDB_TYPE;
```

```csharp
public struct PDB_TYPE {
    public uint ulAppDomainID;
    public Guid guidModule;
    public uint symid;
};
```

## <a name="members"></a>成员

`ulAppDomainID`\
符号来自的应用程序的 ID。 这用于唯一标识应用程序的实例。

`guidModule`\
包含此字段的模块的 GUID。

`symid`\
对应于此字段的符号的 ID。

## <a name="remarks"></a>备注

当`TYPE_INFO``TYPE_KIND_PDB`结构字段设置为[（dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)枚举中的值[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)）时，`dwKind`此结构在TYPE_INFO结构中显示为联合的一部分。

## <a name="requirements"></a>要求

标题： sh.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅

- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
