---
title: METADATA_TYPE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_TYPE
helpviewer_keywords:
- METADATA_TYPE structure
ms.assetid: 2d8b78f6-0aef-4d79-809a-cff9b2c24659
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: afe5ea128775c7be0e48035ab4c7e7d370c9d233
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714288"
---
# <a name="metadata_type"></a>METADATA_TYPE
此结构指定有关从元数据获取的字段类型的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagTYPE_METADATA {
   ULONG32  ulAppDomainID;
   GUID     guidModule;
   _mdToken tokClass;
} METADATA_TYPE;
```

```csharp
public struct METADATA_TYPE {
   public uint ulAppDomainID;
   public Guid guidModule;
   public int  tokClass;
};
```

## <a name="parameters"></a>参数
 `ulAppDomainID`\
 符号来自的应用程序的 ID。 这用于唯一标识应用程序的实例。

 `guidModule`\
 包含此字段的模块的 GUID。

 `tokClass`\
 此类型的元数据令牌 ID。

 [C++]`_mdToken`是`typedef`32 位`int`的 。

## <a name="remarks"></a>备注
 当`TYPE_INFO``TYPE_KIND_METADATA`结构字段设置为[（dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)枚举中的值[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)）时，`dwKind`此结构在TYPE_INFO结构中显示为联合的一部分。

 该`tokClass`值是唯一标识类型的元数据令牌。 有关如何解释元数据令牌 ID 的上位的详细信息，请参阅 .NET`CorTokenType`框架 SDK 中的 corhdr.h 文件中的枚举。

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
