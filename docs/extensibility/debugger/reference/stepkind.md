---
title: STEPKIND | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- STEPKIND
helpviewer_keywords:
- STEPKIND enumeration
ms.assetid: d3d8cf76-24bf-455e-803e-0e3e28f0b262
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7adf835cd3809eeb3d4db664cf5febcfa2a0597b
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329160"
---
# <a name="stepkind"></a>STEPKIND
指定用于单步执行步骤种类。

## <a name="syntax"></a>语法

```cpp
enum enum_STEPKIND { 
   STEP_INTO      = 0,
   STEP_OVER      = 1,
   STEP_OUT       = 2,
   STEP_BACKWARDS = 3
};
typedef DWORD STEPKIND;
```

```csharp
public enum enum_STEPKIND { 
   STEP_INTO      = 0,
   STEP_OVER      = 1,
   STEP_OUT       = 2,
   STEP_BACKWARDS = 3
};
```

## <a name="fields"></a>字段
 `STEP_INTO`\
 单步执行函数。

 `STEP_OVER`\
 过程执行函数的步骤。

 `STEP_OUT`\
 跳出函数。

 `STEP_BACKWARDS`\
 执行某一函数向后的步骤。

## <a name="remarks"></a>备注
 作为参数传递[步骤](../../../extensibility/debugger/reference/idebugprocess3-step.md)方法。

## <a name="requirements"></a>要求
 标头： msdbg.h

 命名空间:Microsoft.VisualStudio.Debugger.Interop

 程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)