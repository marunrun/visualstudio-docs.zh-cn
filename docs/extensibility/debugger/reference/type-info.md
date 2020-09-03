---
title: TYPE_INFO |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
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
 [DwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)枚举中的一个值，该值确定如何解释联合。

 `type.typeMeta`\
 [仅限 c + +]如果为，则包含 [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) 结构 `dwKind` `TYPE_KIND_METADATA` 。

 `type.typePdb`\
 [仅限 c + +]如果为，则包含 [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md) 结构 `dwKind` `TYPE_KIND_PDB` 。

 `type.typeBuilt`\
 [仅限 c + +]如果为，则包含 [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md) 结构 `dwKind` `TYPE_KIND_BUILT` 。

 `type.unused`\
 未使用的填充。

 `type`\
 联合的名称。

 `unionmember`\
 [仅限 c #]基于将此封送到适当的结构类型 `dwKind` 。

## <a name="remarks"></a>备注
 此结构被传递给 [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md) 方法，其中填充了此结构。 如何解释结构的内容基于 `dwKind` 字段。

> [!NOTE]
> [仅限 c + +]如果 `dwKind` 等于 `TYPE_KIND_BUILT` ，则在销毁结构时需要释放基础 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象 `TYPE_INFO` 。 可以通过调用 `typeInfo.type.typeBuilt.pUnderlyingField->Release()` 来完成此操作。

 [仅限 c #]下表显示了如何解释 `unionmember` 每种类型的成员。 该示例演示如何针对一种类型执行此操作。

|`dwKind`|`unionmember` 解释为|
|--------------|----------------------------------|
|`TYPE_KIND_METADATA`|[METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)|
|`TYPE_KIND_PDB`|[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)|
|`TYPE_KIND_BUILT`|[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)|

## <a name="example"></a>示例
 此示例演示如何 `unionmember` `TYPE_INFO` 在 c # 中解释结构的成员。 此示例显示只解释一种类型 (`TYPE_KIND_METADATA`) ，而其他类型则以完全相同的方式解释。

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
 标头： sh。h

 命名空间： VisualStudio

 程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>另请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
