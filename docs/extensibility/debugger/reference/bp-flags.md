---
title: BP_FLAGS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_FLAGS
helpviewer_keywords:
- BP_FLAGS enumeration
ms.assetid: c45dfc74-5e7f-4f1e-a147-ab2a55dccbd0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 62626ff75a4545d89835d3136649191004291f8f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738057"
---
# <a name="bp_flags"></a>BP_FLAGS
提供可用于在设置断点时指定附加信息的可选标志。

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
指定无断点标志。

`BP_FLAG_MAP_DOCPOSITION`\
指定调试引擎 (DE) 应使用文档位置映射断点。 这仅适用于在面向脚本的源文件中设置的断点，例如 (ASP) 的 Active Server Pages。

`BP_FLAG_DONT_STOP`\
指定应由调试引擎处理断点，但调试引擎最终不应 (停止，也就是说，不应) 发送 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) 事件对象。 此标志设计为主要与跟踪点一起使用。

## <a name="remarks"></a>备注
用于 `dwFlags` [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) 和 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md) 结构的成员。

这些值可以与按位组合 `OR` 。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
- [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)
