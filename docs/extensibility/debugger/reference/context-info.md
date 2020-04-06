---
title: CONTEXT_INFO |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_INFO
helpviewer_keywords:
- CONTEXT_INFO structure
ms.assetid: 6b513f4e-e7b0-4969-adf0-2205ccc1e09b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4838df34c14b936af15b8a7a582a6d30ea12bee1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737564"
---
# <a name="context_info"></a>CONTEXT_INFO
此结构描述内存上下文或代码上下文。

## <a name="syntax"></a>语法

```cpp
typedef struct _tagCONTEXT_INFO {
    CONTEXT_INFO_FIELDS dwFields;
    BSTR                bstrModuleUrl;
    BSTR                bstrFunction;
    TEXT_POSITION       posFunctionOffset;
    BSTR                bstrAddress;
    BSTR                bstrAddressOffset;
    BSTR                bstrAddressAbsolute;
} CONTEXT_INFO;
```

```csharp
public struct CONTEXT_INFO {
    public uint          dwFields;
    public string        bstrModuleUrl;
    public string        bstrFunction;
    public TEXT_POSITION posFunctionOffset;
    public string        bstrAddress;
    public string        bstrAddressOffset;
    public string        bstrAddressAbsolute;
};
```

## <a name="members"></a>成员
`dwFields`\
[他CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)枚举中的标志的组合，用于指定填写哪些字段<strong>。</strong>

`bstrModuleUrl`\
上下文所在的模块的名称。

`bstrFunction`\
上下文所在的函数名称。

`posFunctionOffset`\
标识与代码上下文关联的函数的行和列偏移的[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构。

`bstrAddress`\
给定上下文所在的代码中的地址。

`bstrAddressOffset`\
给定上下文所在的代码中地址的偏移量。

`bstrAddressAbsolute`\
给定上下文所在的内存中的绝对地址。

## <a name="remarks"></a>备注
此结构从对[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)方法的调用返回。

此结构的典型用途是支持**内存**调试窗口。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)
- [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
