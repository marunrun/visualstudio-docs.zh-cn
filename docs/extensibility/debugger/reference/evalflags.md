---
title: 埃瓦尔格兹 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EVALFLAGS
helpviewer_keywords:
- EVALFLAGS enumeration
ms.assetid: 7b2cb14a-511a-4fef-9e4f-308139719fba
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4136726e5c8b798121dbd38975d8f2bb935ed04a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737110"
---
# <a name="evalflags"></a>EVALFLAGS
指定控制表达式计算的标志。

## <a name="syntax"></a>语法

```cpp
enum enum_EVALFLAGS {
    EVAL_RETURNVALUE = 0x0002,
    EVAL_NOSIDEEFFECTS = 0x0004,
    EVAL_ALLOWBPS = 0x0008,
    EVAL_ALLOWERRORREPORT = 0x0010,
    EVAL_FUNCTION_AS_ADDRESS = 0x0040,
    EVAL_NOFUNCEVAL = 0x0080,
    EVAL_NOEVENTS = 0x1000
};
typedef DWORD EVALFLAGS;
```

```csharp
public enum enum_EVALFLAGS {
    EVAL_RETURNVALUE = 0x0002,
    EVAL_NOSIDEEFFECTS = 0x0004,
    EVAL_ALLOWBPS = 0x0008,
    EVAL_ALLOWERRORREPORT = 0x0010,
    EVAL_FUNCTION_AS_ADDRESS = 0x0040,
    EVAL_NOFUNCEVAL = 0x0080,
    EVAL_NOEVENTS = 0x1000
}
```

## <a name="fields"></a>字段
`EVAL_RETURNVALUE`\
指定计算返回值（如果有）。

`EVAL_NOSIDEEFFECTS`\
指定不允许副作用。

`EVAL_ALLOWBPS`\
指定在断点停止。

`EVAL_ALLOWERRORREPORT`\
指定允许向主机报告错误。 主要用于在 Internet 资源管理器中脚本中的表达式计算。

`EVAL_FUNCTION_AS_ADDRESS`\
强制函数作为地址计算，而不是调用函数。

`EVAL_NOFUNCEVAL`\
防止计算函数。 例如，`int`考虑表达式`myExpression(int) + 10`中的标记。 此功能可以正确计算为地址，但不能作为值。

`EVAL_NOEVENTS`\
标记以指示不应将表达式计算期间发生的事件发送到会话调试管理器 （SDM） 或 IDE。

## <a name="remarks"></a>备注
这些标志作为参数传递给[评估Async](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)和[评估同步](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)方法。

这些标志可以与位或组合。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
