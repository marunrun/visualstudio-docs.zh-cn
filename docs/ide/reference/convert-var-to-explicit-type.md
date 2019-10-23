---
title: 重构代码以将 var 替换为显式类型
ms.date: 05/15/2018
ms.topic: reference
author: jillre
ms.author: jillfra
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 566d064ac0ac1b9c48ee8e75697cef39b2ec4ee1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661691"
---
# <a name="refactoring-to-replace-var-with-an-explicit-type"></a>重构以将 var 替换为显式类型

使用此重构将本地变量声明中的 [var](/dotnet/csharp/language-reference/keywords/var) 替换为显式类型。

此重构适用于：

- C#

## <a name="why-to-use-an-explicit-type"></a>为何要使用显式类型

以下是使用显式类型声明变量的一些原因：

- 提高代码的可读性。

- 不想在声明中初始化变量。

但是，在使用匿名类型初始化变量并需要在稍后访问对象的属性时，则必须使用 [var](/dotnet/csharp/language-reference/keywords/var)。 有关详细信息，请参阅[隐式类型本地变量 (C#)](/dotnet/csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables)。

## <a name="how-to-use-it"></a>使用方法

1. 将插入点置于 `var` 关键字中。

1. 按“Ctrl”  + **。** 或单击代码文件边距中的螺丝刀![螺丝刀图标](../media/screwdriver-icon.png)图标。

   ![使用显式类型快速操作菜单](media/use-explicit-type.png)

1. 选择“使用显式类型”  。 或者，选择“预览更改”  以打开[“预览更改”](../../ide/preview-changes.md)对话框，然后选择“应用”  。

## <a name="see-also"></a>请参阅

- [隐式类型化变量 (C#)](/dotnet/csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables)
- [重构](../refactoring-in-visual-studio.md)
- [预览更改](../../ide/preview-changes.md)