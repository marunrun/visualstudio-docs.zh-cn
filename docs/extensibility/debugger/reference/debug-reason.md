---
title: DEBUG_REASON |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DEBUG_REASON
helpviewer_keywords:
- DEBUG_REASON enumeration
ms.assetid: ad2ee898-8648-4671-9078-d32873862346
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 59954ea7e89390a5e35dbe0bfb0412da1aabc80f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737421"
---
# <a name="debug_reason"></a>DEBUG_REASON
指定启动进程以进行调试的原因。

## <a name="syntax"></a>语法

```cpp
enum enum_DEBUG_REASON {
    DEBUG_REASON_ERROR         = 0,
    DEBUG_REASON_USER_LAUNCHED = 1,
    DEBUG_REASON_USER_ATTACHED = 2,
    DEBUG_REASON_AUTO_ATTACHED = 3,
    DEBUG_REASON_CAUSALITY     = 4
};
typedef DWORD DEBUG_REASON;
```

```csharp
public enum enum_DEBUG_REASON {
    DEBUG_REASON_ERROR         = 0,
    DEBUG_REASON_USER_LAUNCHED = 1,
    DEBUG_REASON_USER_ATTACHED = 2,
    DEBUG_REASON_AUTO_ATTACHED = 3,
    DEBUG_REASON_CAUSALITY     = 4
};
```

## <a name="fields"></a>字段
`DEBUG_REASON_ERROR`\
发生非特定错误（当其他原因均不合适时，这用作默认条件）。

`DEBUG_REASON_USER_LAUNCHED`\
该过程是应用户请求启动的。

`DEBUG_REASON_USER_ATTACHED`\
已运行的进程由用户附加到。

`DEBUG_REASON_AUTO_ATTACHED`\
该过程在启动时自动附加到。

`DEBUG_REASON_CAUSALITY`\
该过程是由于实时 （JIT） 调试事件而启动*的*。

## <a name="remarks"></a>备注
从[GetDebugAthe 方法](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)返回。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)
