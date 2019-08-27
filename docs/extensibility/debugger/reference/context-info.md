---
title: CONTEXT_INFO | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CONTEXT_INFO
helpviewer_keywords:
- CONTEXT_INFO structure
ms.assetid: 6b513f4e-e7b0-4969-adf0-2205ccc1e09b
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6c50d5ea930f05d22b68416978909cceca17727d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66346465"
---
# <a name="contextinfo"></a>CONTEXT_INFO
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
从他的标志的组合[CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)枚举，用于指定哪些字段填完<strong>。</strong>

`bstrModuleUrl`\
上下文的位置的模块的名称。

`bstrFunction`\
函数名称上下文所在的位置。

`posFunctionOffset`\
一个[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构，它标识与代码上下文关联的函数的行和列偏移量。

`bstrAddress`\
给定的上下文的位置的代码中的地址。

`bstrAddressOffset`\
在代码中给定的上下文的位置的地址的偏移量。

`bstrAddressAbsolute`\
给定的上下文的位置的内存中的绝对地址。

## <a name="remarks"></a>备注
此结构从调用返回[GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)方法。

此结构的典型用法是支持**内存**调试窗口。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)
- [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
