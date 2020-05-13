---
title: CONTEXT_INFO_FIELDS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_INFO_FIELDS
helpviewer_keywords:
- CONTEXT_INFO_FIELDS enumeration
ms.assetid: ef436bd3-738e-47e8-828c-8febce752439
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b398e7ee549026750cbdff7b7fede8522116f346
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737592"
---
# <a name="context_info_fields"></a>CONTEXT_INFO_FIELDS
指定要检索有关内存上下文的信息。

## <a name="syntax"></a>语法

```cpp
enum enum_CONTEXT_INFO_FIELDS {
    CIF_MODULEURL =       0x00000001,
    CIF_FUNCTION =        0x00000002,
    CIF_FUNCTIONOFFSET =  0x00000004,
    CIF_ADDRESS =         0x00000008,
    CIF_ADDRESSOFFSET =   0x00000010,
    CIF_ADDRESSABSOLUTE = 0x00000020,
    CIF_ALLFIELDS =       0x0000003f
};
typedef DWORD CONTEXT_INFO_FIELDS;
```

```csharp
public enum enum_CONTEXT_INFO_FIELDS {
    CIF_MODULEURL =       0x00000001,
    CIF_FUNCTION =        0x00000002,
    CIF_FUNCTIONOFFSET =  0x00000004,
    CIF_ADDRESS =         0x00000008,
    CIF_ADDRESSOFFSET =   0x00000010,
    CIF_ADDRESSABSOLUTE = 0x00000020,
    CIF_ALLFIELDS =       0x0000003f
};
```

## <a name="fields"></a>字段
`CIF_MODULEURL`\
初始化/使用`bstrModuleUrl`[CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)结构的字段。

`CIF_FUNCTION`\
初始化/使用`bstrFunction`结构字段。 `CONTEXT_INFO`

`CIF_FUNCTIONOFFSET`\
初始化/使用`posFunctionOffset`结构字段。 `CONTEXT_INFO`

`CIF_ADDRESS`\
初始化/使用`bstrAddress`结构字段。 `CONTEXT_INFO`

`CIF_ADDRESSOFFSET`\
初始化/使用`bstrAddressOffset`结构字段。 `CONTEXT_INFO`

`CIF_ALLFIELDS`\
初始化/使用`CONTEXT_INFO`结构的所有字段。

## <a name="remarks"></a>备注
这些值将参数传递给[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)方法，以指示要初始化[CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)结构的字段。

这些标志还用于指示在返回`CONTEXT_INFO`结构时使用结构的字段并有效。

这些值可以与位或组合。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)
