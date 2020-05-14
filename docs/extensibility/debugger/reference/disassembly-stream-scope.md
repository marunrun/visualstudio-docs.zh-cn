---
title: DISASSEMBLY_STREAM_SCOPE |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_STREAM_SCOPE
helpviewer_keywords:
- DISASSEMBLY_STREAM_SCOPE enumeration
ms.assetid: 43e2b364-cbbe-4755-a7e6-a03f3054c965
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fae1f22c6db22cd6cff93cfb1b98a28620a1537c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737268"
---
# <a name="disassembly_stream_scope"></a>DISASSEMBLY_STREAM_SCOPE
指定拆解流的范围。

## <a name="syntax"></a>语法

```cpp
enum enum_DISASSEMBLY_STREAM_SCOPE {
    DSS_HUGE     = 0x10000000,
    DSS_FUNCTION = 0x0001,
    DSS_MODULE   = (DSS_HUGE) | 0x0002,
    DSS_ALL      = (DSS_HUGE) | 0x0003
};
typedef DWORD DISASSEMBLY_STREAM_SCOPE;
```

```csharp
public enum enum_DISASSEMBLY_STREAM_SCOPE {
    DSS_HUGE     = 0x10000000,
    DSS_FUNCTION = 0x0001,
    DSS_MODULE   = (DSS_HUGE) | 0x0002,
    DSS_ALL      = (DSS_HUGE) | 0x0003
};
```

## <a name="fields"></a>字段
`DSS_HUGE`\
指定拆解代码上下文产生的输出将超过客户端在单个调用中通常希望检索的输出数。

`DSS_FUNCTION`\
指定应拆解代码上下文中包含的函数。 指定拆解流表示函数，当由[GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)方法返回时。

`DSS_MODULE`\
当由`IDebugDisassemblyStream2::GetScope`方法返回时，指定拆解流表示模块。

`DSS_ALL`\
指定整个地址空间的拆解。

## <a name="remarks"></a>备注
作为参数传递给[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)方法，并由[GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)方法返回。

这些值可以稍微结合`OR`。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)
