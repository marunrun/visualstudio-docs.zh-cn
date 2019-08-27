---
title: METADATA_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_TYPE
helpviewer_keywords:
- METADATA_TYPE structure
ms.assetid: 2d8b78f6-0aef-4d79-809a-cff9b2c24659
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3d608e4e9bf9987eb1dd430a9e22660c1da6a90a
ms.sourcegitcommit: 12f2851c8c9bd36a6ab00bf90a020c620b364076
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2019
ms.locfileid: "66746699"
---
# <a name="metadatatype"></a>METADATA_TYPE
此结构指定从元数据字段类型有关的信息。

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
 符号所来自的应用程序 ID。 这用于唯一标识应用程序的实例。

 `guidModule`\
 包含此字段的模块的 GUID。

 `tokClass`\
 此类型的元数据令牌 ID。

 [C++]`_mdToken`是`typedef`适用于 32 位`int`。

## <a name="remarks"></a>备注
 此结构显示为中的联合的一部分[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)结构时`dwKind`字段`TYPE_INFO`结构设置为`TYPE_KIND_METADATA`(从值[dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)枚举）。

 `tokClass`值是唯一标识某个类型的元数据标记。 有关如何解释高位的元数据令牌 ID 的详细信息，请参阅`CorTokenType`corhdr.h 中的文件在.NET Framework SDK 中的枚举。

## <a name="requirements"></a>要求
 标头： sh.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)