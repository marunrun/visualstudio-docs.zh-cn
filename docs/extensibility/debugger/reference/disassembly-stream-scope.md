---
title: DISASSEMBLY_STREAM_SCOPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DISASSEMBLY_STREAM_SCOPE
helpviewer_keywords:
- DISASSEMBLY_STREAM_SCOPE enumeration
ms.assetid: 43e2b364-cbbe-4755-a7e6-a03f3054c965
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 724e32f83cfec31c2bacdab661407983af87efe6
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66318247"
---
# <a name="disassemblystreamscope"></a>DISASSEMBLY_STREAM_SCOPE
指定反汇编流的作用域。

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
指定拆装代码上下文会生成不是客户端通常想要在单个调用中检索详细输出。

`DSS_FUNCTION`\
指定应拆装所包含的代码上下文的函数。 指定的反汇编流表示一个函数时返回的[GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)方法。

`DSS_MODULE`\
当返回`IDebugDisassemblyStream2::GetScope`方法中，指定反汇编流表示一个模块。

`DSS_ALL`\
指定整个地址空间的反汇编。

## <a name="remarks"></a>备注
作为参数传递[GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)方法并返回由[GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)方法。

可能的按位组合这些值`OR`。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [GetScope](../../../extensibility/debugger/reference/idebugdisassemblystream2-getscope.md)
