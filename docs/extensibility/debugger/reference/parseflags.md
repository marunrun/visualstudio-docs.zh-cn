---
title: PARSEFLAGS |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- PARSEFLAGS
helpviewer_keywords:
- PARSEFLAGS enumeration
ms.assetid: 47943f0a-54cb-4493-a62e-5dba97bd4c35
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0cc70fdd9fe1279e4d419a422b970eb3d3b07c65
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80714121"
---
# <a name="parseflags"></a>PARSEFLAGS
指定如何解析表达式。

## <a name="syntax"></a>语法

```cpp
enum enum_PARSEFLAGS { 
   PARSE_EXPRESSION            = 0x0001,
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000
};
typedef DWORD PARSEFLAGS;
```

```csharp
public enum enum_PARSEFLAGS { 
   PARSE_EXPRESSION            = 0x0001,
   PARSE_FUNCTION_AS_ADDRESS   = 0x0002,
   PARSE_DESIGN_TIME_EXPR_EVAL = 0x1000
};
```

## <a name="fields"></a>字段
 `PARSE_EXPRESSION`\
 指示表达式不是语句。

 `PARSE_FUNCTION_AS_ADDRESS`\
 指示表达式将作为地址进行解析（和以后计算）。

 `PARSE_DESIGN_TIME_EXPR_EVAL`\
 指示在设计期间（即设计器打开时）正在分析表达式。

## <a name="remarks"></a>备注
 作为参数传递给[ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)和[Parse 方法](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)。

## <a name="requirements"></a>要求
 标题： msdbg.h

 命名空间：微软.VisualStudio.调试器.互通

 程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [ParseText](../../../extensibility/debugger/reference/idebugexpressioncontext2-parsetext.md)
- [解析](../../../extensibility/debugger/reference/idebugexpressionevaluator-parse.md)
