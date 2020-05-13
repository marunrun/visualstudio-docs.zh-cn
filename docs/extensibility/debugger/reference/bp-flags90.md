---
title: BP_FLAGS90 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- BP_FLAGS90 enumeration
ms.assetid: 3e5a06c5-fb30-4b8a-b2d5-4a0570fc80bd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5628af4a6e5c4deae3de02340e882bd2605e22d3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738046"
---
# <a name="bp_flags90"></a>BP_FLAGS90
枚举可选标志的有效值。 设置断点时，可选标志可用于指定其他信息。 此枚举扩展了[BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md)枚举。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_FLAGS90
{
    // VS 8.0 values
    BP90_FLAG_NONE               = 0x0000,
    BP90_FLAG_MAP_DOCPOSITION    = 0x0001,
    BP90_FLAG_DONT_STOP          = 0x0002,

    // Values added in VS 9.0
    BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,
};
typedef DWORD BP_FLAGS90;
```

```csharp
public enum enum_BP_FLAGS90
{
    // VS 8.0 values
    BP90_FLAG_NONE                = 0x0000,
    BP90_FLAG_MAP_DOCPOSITION     = 0x0001,
    BP90_FLAG_DONT_STOP           = 0x0002,

    // Values added in VS 9.0
    BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,
};
```

## <a name="fields"></a>字段
`BP90_FLAG_NONE`\
指定无断点标志。

`BP90_FLAG_MAP_DOCPOSITION`\
指定调试引擎 （DE） 应使用文档位置映射断点。 这仅适用于在面向脚本的源文件中设置的断点，如活动服务器页 （ASP）。

`BP90_FLAG_DONT_STOP`\
指定断点应由调试引擎处理，但调试引擎最终不应停止;也就是说，不应发送[IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md)事件对象。 此标志设计主要用于跟踪点。

`BP90_FLAG_TRACEPOINT_CONTINUE`\
本机调试引擎用于确定是否应清除步进状态。 它与BP90_FLAG_DONT_STOP不同，因为如果跟踪点执行宏，则不设置BP90_FLAG_DONT_STOP。

## <a name="requirements"></a>要求
标题： Msdbg90.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
