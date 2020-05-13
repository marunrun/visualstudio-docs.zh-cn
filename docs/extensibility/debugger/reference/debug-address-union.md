---
title: DEBUG_ADDRESS_UNION |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_ADDRESS_UNION
helpviewer_keywords:
- DEBUG_ADDRESS_UNION union
ms.assetid: e3d11aab-de0d-4109-b5dc-11e07e64382d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ad531ee10914e404459632c98aae4a9bbda8e437
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737523"
---
# <a name="debug_address_union"></a>DEBUG_ADDRESS_UNION
描述不同类型的地址。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagDEBUG_ADDRESS_UNION {
   ADDRESS_KIND dwKind;
   union {
      NATIVE_ADDRESS                  addrNative;
      UNMANAGED_ADDRESS_THIS_RELATIVE addrThisRel;
      UNMANAGED_ADDRESS_PHYSICAL      addrUPhysical;
      METADATA_ADDRESS_METHOD         addrMethod;
      METADATA_ADDRESS_FIELD          addrField;
      METADATA_ADDRESS_LOCAL          addrLocal;
      METADATA_ADDRESS_PARAM          addrParam;
      METADATA_ADDRESS_ARRAYELEM      addrArrayElem;
      METADATA_ADDRESS_RETVAL         addrRetVal;
      DWORD                           unused;
   } addr;
} DEBUG_ADDRESS_UNION;
```

```csharp
public struct DEBUG_ADDRESS_UNION {
   public ADDRESS_KIND dwKind;
   public IntPtr       unionmember;
}
```

## <a name="members"></a>成员
`dwKind`\
[ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)枚举中的值，指定如何解释联合。

`addr.addrNative`\
[仅C++]如果 = [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md) ADDRESS_KIND_NATIVE，`dwKind`则包含NATIVE_ADDRESS结构。

`addr.addrThisRel`\
[仅C++]如果 =[UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md) ADDRESS_KIND_UNMANAGED_THIS_RELATIVE，`dwKind`则包含UNMANAGED_ADDRESS_THIS_RELATIVE结构。

`addr.addUPhysical`\
[仅C++]如果 =[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md) ADDRESS_KIND_UNMANAGED_PHYSICAL，`dwKind`则包含UNMANAGED_ADDRESS_PHYSICAL结构。

`addr.addrMethod`\
[仅C++]如果 =[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md) ADDRESS_KIND_METHOD，`dwKind`则包含METADATA_ADDRESS_METHOD结构。

`addr.addrField`\
[仅C++]如果 =[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md) ADDRESS_KIND_FIELD，`dwKind`则包含METADATA_ADDRESS_FIELD结构。

`addr.addrLocal`\
[仅C++]如果 =[METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md) ADDRESS_KIND_LOCAL，`dwKind`则包含METADATA_ADDRESS_LOCAL结构。

`addr.addrParam`\
[仅C++]如果 =[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md) ADDRESS_KIND_PARAM，`dwKind`则包含METADATA_ADDRESS_PARAM结构。

`addr.addrArrayElem`\
[仅C++]如果 =[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md) ADDRESS_KIND_ARRAYELEM，`dwKind`则包含METADATA_ADDRESS_ARRAYELEM结构。

`addr.addrRetVal`\
[仅C++]如果 =[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md) ADDRESS_KIND_RETVAL，`dwKind`则包含METADATA_ADDRESS_RETVAL结构。

`addr.unused`\
[仅C++] 填充。

`addr`\
[仅C++]联合的名称。

`unionmember`\
[仅 C]此值需要根据`dwKind`进行封送到相应的结构类型。 有关联合之间的`dwKind`关联和解释，请参阅备注。

## <a name="remarks"></a>备注
此结构是[DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)结构的一部分，表示多种不同类型的地址之一（`DEBUG_ADDRESS`结构由对[GetAddress](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)方法的调用填充）。

 [仅 C]下表显示了如何解释每种地址`unionmember`的成员。 "示例"显示了如何针对一种地址执行此操作。

|`dwKind`|`unionmember`解释为|
|--------------|----------------------------------|
|`ADDRESS_KIND_NATIVE`|[NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)|
|`ADDRESS_KIND_UNMANAGED_THIS_RELATIVE`|[UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)|
|`ADDRESS_KIND_UNMANAGED_PHYSICAL`|[UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)|
|`ADDRESS_KIND_METHOD`|[METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)|
|`ADDRESS_KIND_FIELD`|[METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)|
|`ADDRESS_KIND_LOCAL`|[METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)|
|`ADDRESS_KIND_PARAM`|[METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)|
|`ADDRESS_KIND_ARRAYELEM`|[METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)|
|`ADDRESS_KIND_RETVAL`|[METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)|

## <a name="example"></a>示例
此示例演示如何解释 C# 中结构的`METADATA_ADDRESS_ARRAYELEM``DEBUG_ADDRESS_UNION`一种地址 （ ） 。 其余元素的解释方式完全相同。

```csharp
using System;
using System.Runtime.Interop.Services;
using Microsoft.VisualStudio.Debugger.Interop;

namespace MyPackage
{
    public class MyClass
    {
        public void Interpret(DEBUG_ADDRESS_UNION dau)
        {
            if (dau.dwKind == (uint)enum_ADDRESS_KIND.ADDRESS_KIND_METADATA_ARRAYELEM)
            {
                 METADATA_ADDRESS_ARRAYELEM arrayElem =
                     (METADATA_ADDRESS_ARRAYELEM)Marshal.PtrToStructure(dau.unionmember,
                                 typeof(METADATA_ADDRESS_ARRAYELEM));
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
- [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
- [获取地址](../../../extensibility/debugger/reference/idebugaddress-getaddress.md)
