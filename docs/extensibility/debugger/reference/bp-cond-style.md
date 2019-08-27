---
title: BP_COND_STYLE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- BP_COND_STYLE
helpviewer_keywords:
- BP_COND_STYLE enumeration
ms.assetid: a93b1412-f447-48a1-af9d-38f3dbb3092f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ded3d31f9be2d0a02a238ead4bc989cc21b4922a
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351817"
---
# <a name="bpcondstyle"></a>BP_COND_STYLE
指定断点条件的样式的挂起和绑定断点。

## <a name="syntax"></a>语法

```cpp
enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
typedef DWORD BP_COND_STYLE;
```

```csharp
public enum enum_BP_COND_STYLE {
    BP_COND_NONE         = 0x0000,
    BP_COND_WHEN_TRUE    = 0x0001,
    BP_COND_WHEN_CHANGED = 0x0002
};
```

## <a name="fields"></a>字段
`BP_COND_NONE`\
到达断点的位置时，会触发断点。 没有指定断点条件。

`BP_COND_WHEN_TRUE`\
仅在条件表达式时与断点关联的计算结果为触发断点`true`。

`BP_COND_WHEN_CHANGED`\
触发断点仅在与断点关联的条件表达式的值时已从其以前的评估。

## <a name="remarks"></a>备注
用于`styleCondition`的成员[BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)结构。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)
