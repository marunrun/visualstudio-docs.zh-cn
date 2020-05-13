---
title: BUILT_TYPE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BUILT_TYPE
helpviewer_keywords:
- BUILT_TYPE structure
ms.assetid: cc02c32c-0f65-4210-ad25-a9b1899066e8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 885f17b0841a39672c87be5bc7c947b2e0d9c7e0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737698"
---
# <a name="built_type"></a>BUILT_TYPE
此结构指定有关从元数据获取的字段类型的信息。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagTYPE_BUILT {
    ULONG32      ulAppDomainID;
    GUID         guidModule;
    IDebugField* pUnderlyingField;
} BUILT_TYPE;
```

```csharp
public struct BUILT_TYPE {
    public uint        ulAppDomainID;
    public Guid        guidModule;
    public IDebugField pUnderlyingField;
};
```

## <a name="members"></a>成员
`ulAppDomainID`\
符号来自的应用程序的 ID。 这用于唯一标识应用程序的实例。

`guidModule`\
包含此字段的模块的 GUID。

`pUnderlyingField`\
标识与此生成字段关联的基础字段的[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)对象。

## <a name="remarks"></a>备注
当`TYPE_INFO``TYPE_KIND_BUILT`结构字段设置为[（dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)枚举中的值[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)）时，`dwKind`此结构在TYPE_INFO结构中显示为联合的一部分。

## <a name="requirements"></a>要求
标题： sh.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
