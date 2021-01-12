---
title: 自动换行、缩进和对齐重构
description: 了解如何自动换行并对齐方法调用链。
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: d8a98ebd1fa1e8a9ec937cf4e0965d804a8a9387
ms.sourcegitcommit: 3c571f44bfd6402efea5187af43df287bac5b6ac
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "97761220"
---
# <a name="wrap-indent-and-align-refactorings"></a>自动换行、缩进和对齐重构

## <a name="wrap-and-align-call-chains"></a>自动换行并对齐调用链

此重构适用于：

- C#

- Visual Basic

**功能：** 允许自动换行和对齐方法调用链。

**使用时机：** 有一个长链，由一个语句中的多个方法调用组成。

操作原因：  根据用户首选项进行自动换行或缩进时，长列表会更易于阅读。

### <a name="how-to"></a>操作说明

1. 将光标置于任何调用链中。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
3. 选择“对调用链进行自动换行”或“自动换行并对齐调用链”以接受重构   。

   ![Visual Studio 中“快速操作和重构”菜单的屏幕截图，其中选中了“对调用链进行自动换行”，并显示了 C# 代码更改。](media/wrap-call-chain.png)

## <a name="wrap-indent-and-align-parameters-or-arguments"></a>换行、缩进和对齐参数

此重构适用于：

- C#

- Visual Basic

**功能：** 允许你换行、缩进或对齐参数。

**使用时机：** 有具有多个参数的方法声明或调用。

操作原因：  根据用户偏好换行或缩进时，读取一长串参数会更容易。

### <a name="how-to"></a>操作说明

1. 请将光标放置在参数列表中。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。

   ![自动换行、缩进和对齐参数](media/wrap-parameters.png)

3. 选择“包装每个参数”以接受重构  。

## <a name="wrap-binary-expressions"></a>包装二进制表达式

此重构适用于：

- C#

- Visual Basic

**功能：** 包装二进制表达式。

**使用时机：** 在你拥有二进制表达式时。

操作原因：  将二进制表达式包装到用户首选项后，读取二进制表达式会更容易。

### <a name="how-to"></a>操作说明

1. 将光标置于二进制表达式中。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
3. 选择“包装表达式”以接受重构  。

   ![Visual Studio 中“快速操作和重构”菜单的屏幕截图，其中选中了“对表达式进行自动换行”，并显示了 C# 代码更改。](media/wrap-binary-expression.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
