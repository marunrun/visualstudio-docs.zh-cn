---
title: TYPE_INFO |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- TYPE_INFO
helpviewer_keywords:
- TYPE_INFO structure
ms.assetid: d725cb68-a565-49d1-a16f-ff0445c587a0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 82796c1d82dc3ca77151abcec3e1dd6ce13ac59d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713318"
---
# <a name="type_info"></a>TYPE_INFO
此结构指定有关字段类型的各种信息。

## <a name="syntax"></a>语法

```cpp
struct _tagTYPE_INFO_UNION {
   dwTYPE_KIND dwKind;
   union {
      METADATA_TYPE typeMeta;
      PDB_TYPE      typePdb;
      BUILT_TYPE    typeBuilt;
      DWORD         unused;
   } type;
} TYPE_INFO;
```

```csharp
public struct TYPE_INFO {
   public uint   dwKind;
   public IntPtr unionmember;
};
```

## <a name="members"></a>成员
 `dwKind`\
 [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)枚举中确定如何解释联合的值。

 `type.typeMeta`\
 [仅C++]如果`dwKind`是`TYPE_KIND_METADATA`，则包含[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)结构。

 `type.typePdb`\
 [仅C++]如果`dwKind`是`TYPE_KIND_PDB`，则包含[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)结构。

 `type.typeBuilt`\
 [仅C++]如果`dwKind`是`TYPE_KIND_BUILT`，则包含[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)结构。

 `type.unused`\
 未使用的填充。

 `type`\
 联合的名称。

 `unionmember`\
 [仅 C]将此情况编送到基于`dwKind`的相应结构类型。

## <a name="remarks"></a>备注
 此结构传递给填写该结构的[GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)方法。 结构内容的解释方式基于字段`dwKind`。

> [!NOTE]
> [仅C++]如果`dwKind`等于`TYPE_KIND_BUILT`，则在破坏`TYPE_INFO`结构时必须释放基础[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。 可以通过调用 `typeInfo.type.typeBuilt.pUnderlyingField->Release()` 来完成此操作。

 [仅 C]下表显示了如何解释每种类型`unionmember`的成员。 该示例演示如何针对一种类型进行此操作。

|`dwKind`|`unionmember`解释为|
|--------------|----------------------------------|
|`TYPE_KIND_METADATA`|[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)|
|`TYPE_KIND_PDB`|[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)|
|`TYPE_KIND_BUILT`|[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)|

## <a name="example"></a>示例
 此示例演示如何解释 C#`unionmember`中`TYPE_INFO`结构的成员。 此示例仅解释一种类型 （`TYPE_KIND_METADATA`），但其他类型的解释方式完全相同。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(TYPE_INFO ti)
        {
            if (ti.dwKind == (uint)enum_dwTypeKind.TYPE_KIND_METADATA)
            {
                 METADATA_TYPE dataType = (METADATA_TYPE)Marshal.PtrToStructure(ti.unionmember,
                                               typeof(METADATA_TYPE));
            }
        }
    }
}
```

## <a name="requirements"></a>要求
 标题： sh.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [获取类型信息](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
