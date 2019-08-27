---
title: BP_FLAGS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_FLAGS
helpviewer_keywords:
- BP_FLAGS enumeration
ms.assetid: c45dfc74-5e7f-4f1e-a147-ab2a55dccbd0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 31f5153c3a2d0b55829a7743840fe8a791f023d0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66319227"
---
# <a name="bpflags"></a>BP_FLAGS
提供了可用于设置一个断点时指定的附加信息的可选标志。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_FLAGS {
    BP_FLAG_NONE            = 0x0000,
    BP_FLAG_MAP_DOCPOSITION = 0x0001,
    BP_FLAG_DONT_STOP       = 0x0002
};
typedef DWORD BP_FLAGS;
```

```csharp
public enum enum_BP_FLAGS {
    BP_FLAG_NONE            = 0x0000,
    BP_FLAG_MAP_DOCPOSITION = 0x0001,
    BP_FLAG_DONT_STOP       = 0x0002
};
```

## <a name="fields"></a>字段
`BP_FLAG_NONE`\
不指定任何断点标志。

`BP_FLAG_MAP_DOCPOSITION`\
指定调试引擎 (DE) 应映射使用的文档位置断点。 这是仅适用于面向脚本的源代码文件，如 Active Server Pages (ASP) 中设置断点。

`BP_FLAG_DONT_STOP`\
指定调试引擎中，应处理断点，但是，调试引擎最终应接着往下看 (即[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)事件对象不应在发送)。 此标志用于主要与跟踪点一起使用。

## <a name="remarks"></a>备注
用于`dwFlags`的成员[BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)并[BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)结构。

可能的按位组合这些值`OR`。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
