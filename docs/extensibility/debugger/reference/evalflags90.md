---
title: EVALFLAGS90 |微软文档
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- EVALFLAGS90 enumeration
ms.assetid: 64fb0139-8b04-4726-b52c-db2e04d65498
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 01951885541ba4acce33f3e4f06f7106116ccc62
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737101"
---
# <a name="evalflags90"></a>EVALFLAGS90
枚举控制表达式计算的标志的有效值。 此枚举扩展了[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)枚举。

## <a name="syntax"></a>语法

```cpp
enum enum_EVALFLAGS90
{
    // VS 8.0 values
    EVAL90_RETURNVALUE                 = 0x0002,
    EVAL90_NOSIDEEFFECTS               = 0x0004,
    EVAL90_ALLOWBPS                    = 0x0008,
    EVAL90_ALLOWERRORREPORT            = 0x0010,
    EVAL90_FUNCTION_AS_ADDRESS         = 0x0040,
    EVAL90_NOFUNCEVAL                  = 0x0080,
    EVAL90_NOEVENTS                    = 0x1000,
    EVAL90_DESIGN_TIME_EXPR_EVAL       = 0x2000,
    EVAL90_ALLOW_IMPLICIT_VARS         = 0x4000,

    // Values added in VS 9.0
    EVAL90_FORCE_EVALUATION_NOW        = 0x8000
};
typedef DWORD EVALFLAGS90;
```

```csharp
public enum enum_EVALFLAGS90
{
    // VS 8.0 values
    EVAL90_RETURNVALUE                 = 0x0002,
    EVAL90_NOSIDEEFFECTS               = 0x0004,
    EVAL90_ALLOWBPS                    = 0x0008,
    EVAL90_ALLOWERRORREPORT            = 0x0010,
    EVAL90_FUNCTION_AS_ADDRESS         = 0x0040,
    EVAL90_NOFUNCEVAL                  = 0x0080,
    EVAL90_NOEVENTS                    = 0x1000,
    EVAL90_DESIGN_TIME_EXPR_EVAL       = 0x2000,
    EVAL90_ALLOW_IMPLICIT_VARS         = 0x4000,

    // Values added in VS 9.0
    EVAL90_FORCE_EVALUATION_NOW        = 0x8000
};
```

## <a name="fields"></a>字段
`EVAL90_RETURNVALUE`\
指定计算返回值（如果有）。

`EVAL90_NOSIDEEFFECTS`\
指定不允许副作用。

`EVAL90_ALLOWBPS`\
指定在断点停止。

`EVAL90_ALLOWERRORREPORT`\
指定允许向主机报告的错误。 主要用于在 Internet 资源管理器中脚本中的表达式计算。

`EVAL90_FUNCTION_AS_ADDRESS`\
强制函数作为地址计算，而不是调用函数。

`EVAL90_NOFUNCEVAL`\
防止计算函数。 例如，`int`考虑表达式`myExpression(int) + 10`中的标记。 此功能可以正确计算为地址，但不能作为值。

`EVAL90_NOEVENTS`\
标记以指示不应将表达式计算期间发生的事件发送到会话调试管理器 （SDM） 或 IDE。

`EVAL90_DESIGN_TIME_EXPR_EVAL`\
启用设计时表达式计算。

`EVAL90_ALLOW_IMPLICIT_VARS`\
允许隐式变量创建。

`EVAL90_FORCE_EVALUATION_NOW`\
强制立即进行评估。 这在服务请求（如用户请求）时非常有用。

## <a name="requirements"></a>要求
标题： Msdbg90.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
