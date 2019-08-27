---
title: STEPUNIT | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- STEPUNIT
helpviewer_keywords:
- STEPUNIT enumeration
ms.assetid: cb8441f2-f744-4e73-acfe-ae8542df9649
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 803aafb60d7ada5b3339735fc0a10c66bb4925e0
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329175"
---
# <a name="stepunit"></a>STEPUNIT
单步执行指定单步执行单元。

## <a name="syntax"></a>语法

```cpp
enum enum_STEPUNIT { 
   STEP_STATEMENT   = 0,
   STEP_LINE        = 1,
   STEP_INSTRUCTION = 2
};
typedef DWORD STEPUNIT;
```

```csharp
enum enum_STEPUNIT { 
   STEP_STATEMENT   = 0,
   STEP_LINE        = 1,
   STEP_INSTRUCTION = 2
};
```

## <a name="fields"></a>字段
 `STEP_STATEMENT`\
 若要执行的语句的步骤。

 `STEP_LINE`\
 若要执行的行的步骤。

 `STEP_INSTRUCTION`\
 若要执行的指令的步骤。

## <a name="remarks"></a>备注
 作为参数传递[步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)方法。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)