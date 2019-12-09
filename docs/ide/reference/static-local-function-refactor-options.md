---
title: 静态本地函数重构
ms.date: 09/28/2019
ms.topic: reference
author: governesss
ms.author: midumont
manager: jillfra
f1_keywords:
- vs.csharp.refactoring.make.local.function.static
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: adbf84b9ae7566cd5e58a7c757ce09a37252b754
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74782317"
---
# <a name="static-local-function-refactorings-and-quick-actions"></a>静态本地重构和快速操作

本文概述了与静态本地函数相关的两个工作效率功能。 一种是将本地函数设置为静态的重构，另一种是快速动作，可生成将变量传递到静态本地函数中的代码。

## <a name="make-local-function-static"></a>将本地函数设置为静态

此重构适用于：

- C#

**功能：** 可以将本地函数设置为静态，并将在函数外部定义的变量传入到该函数的声明和调用。

**使用时机：** 你希望本地函数是静态的，并且在函数的作用域中定义所有变量。

操作原因：  静态本地函数可提高可读性：已知特定代码是隔离的，使其更易于理解、重新读取和重用。 静态本地函数还提供作用域，以防止使用仅在单个方法中调用的静态函数污染类。

### <a name="how-to"></a>操作说明

1. 将插入点置于本地函数名称上。

2. 按“Ctrl”  + **。** （句点）触发“快速操作和重构”  菜单。

   ![将本地函数设置为静态](media/make-local-function-static.png)

3. 选择“将本地函数设置为静态”。 

## <a name="pass-variable-explicitly-in-a-static-local-function"></a>将变量显式传入静态本地函数

此快速操作适用于：

- C#

**功能：** 现在可以将变量显式传入本地静态函数。

**使用时机：** 你希望本地函数是静态的，但仍使用在该函数之外初始化的变量。

操作原因：  使用静态本地函数向读者进行澄清，因为他们知道只能在程序的特定上下文中声明和调用该函数。 它可以灵活地在此上下文外定义变量，但仍能将它们作为参数传递给静态本地函数。

### <a name="how-to"></a>操作说明

1. 将插入点置于静态本地函数中使用的变量上。

2. 按“Ctrl”  + **。** （句点）触发“快速操作和重构”  菜单。

   ![将变量显式传入静态本地函数](media/pass-variable-explicitly-static-local-function.png)

3. 选择“将变量显式传入局部静态函数”。 

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)