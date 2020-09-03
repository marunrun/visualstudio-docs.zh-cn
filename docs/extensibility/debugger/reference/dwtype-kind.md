---
title: dwTYPE_KIND |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- dwTYPE_KIND
helpviewer_keywords:
- dwTYPE_KIND enumeration
ms.assetid: 6ff56b0f-c502-4e6c-9829-bfa05361b783
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a9d790f12d3fc21bbae7373470746af2ebfe6dc9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80737191"
---
# <a name="dwtype_kind"></a>dwTYPE_KIND
指定如何解释 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 对象的类型。

## <a name="syntax"></a>语法

```cpp
enum enum_dwTYPE_KIND {
    TYPE_KIND_METADATA = 0x0001,
    TYPE_KIND_PDB      = 0x0002,
    TYPE_KIND_BUILT    = 0x0003,
};

typedef DWORD dwTYPE_KIND;
```

```csharp
public enum enum_dwTYPE_KIND {
    TYPE_KIND_METADATA = 0x0001,
    TYPE_KIND_PDB      = 0x0002,
    TYPE_KIND_BUILT    = 0x0003,
};
```

## <a name="fields"></a>字段
`TYPE_KIND_METADATA`\
应将 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 联合解释为 [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md) 结构。

`TYPE_KIND_PDB`\
`TYPE_INFO`Union 应解释为[PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)结构。

`TYPE_KIND_BUILT`\
`TYPE_INFO`Union 应解释为[BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)结构。

## <a name="remarks"></a>备注
此枚举的值将显示在 `dwKind` [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 结构的字段中，并用于确定如何解释 `type` 联合成员。 此 `TYPE_INFO` 结构由对 [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md) 方法的调用返回。

## <a name="requirements"></a>要求
标头： sh。h

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [GetTypeInfo](../../../extensibility/debugger/reference/idebugfield-gettypeinfo.md)
- [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)
- [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)
- [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)
