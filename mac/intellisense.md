---
title: IntelliSense
description: 有关使用 Visual Studio for Mac 中的 IntelliSense 的信息
author: cobey
ms.author: cobey
ms.date: 08/16/2019
ms.openlocfilehash: 07ef1d6292e4ac88ca616d0f35e3fd831cacc649
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "75405811"
---
# <a name="intellisense"></a>IntelliSense

IntelliSense 提供了多种功能，有助于增强编写和编辑代码的体验。 例如，除代码完成之外，IntelliSense 引擎还提供成员列表、参数信息和快速信息。

在 Visual Studio for Mac 中，IntelliSense 由核心编辑器服务提供，并且支持多种语言，例如 C#、XAML、F#、JavaScript 等。 Visual Studio for Mac 还具有高级 IntelliSense 功能，例如能显示尚未导入项目的库的完成。

## <a name="code-completion"></a>代码完成

在支持的文件（例如 C# 代码文件）中键入内容时，当前键入的字符串的有效完成将显示在完成列表中，并在键入时更新。 此外，如果删除文本，列表将再次自动更新，以包含完成给定字符串的更多可能性。 

完成窗口还支持按类型筛选包含的完成。 例如，可以将列表成员限制为仅表示类或委托等类型。 可以通过单击表示将筛选的类型的特定图标，或通过与给定类型对应的键盘快捷方式来启用此筛选过程。 位于完成窗口底部的图标如下：

| 图标                         | 名称          | 关键字    | 热键 |
| -----------------------------|---------------| -----------|--------|
| ![类图标](media/classes-icon.png)  | class         | `class`    |  ⌥C
| ![“常量”图标](media/constant-icon.png) | 常量      | `const`    |  ⌥O
| ![委托图标](media/delegate-icon.png) | 委托      | `delegate` |  ⌥D
| ![枚举图标](media/enums-icon.png)    | 枚举          | `enum`     |  ⌥E
| ![事件图标](media/event-icon.png)    | event         |            |  ⌥V
| ![“字段”图标](media/fields-icon.png)   | 字段         |            |  ⌥F
| ![接口图标](media/interface-icon.png)| 接口     | `interface`|  ⌥I
| ![关键字图标](media/keyword-icon.png)  | 关键字 (keyword)       |            |  ⌥K
| ![方法图标](media/method-icon.png)   | method        |            |  ⌥M
| ![命名空间图标](media/namespace-icon.png)| 命名空间     | `namespace`|  ⌥N
| ![属性图标](media/props-icon.png)    | 属性      |            |  ⌥P
| ![代码片段图标](media/snippet-icon.png)  | 片段       | `class`    |  ⌥S
| ![结构图标](media/struct-icon.png)   | structure     | `struct`   |  ⌥S

通过单击任何图标，或者按下相应的热键，完成列表将仅限于由筛选集定义的类型。  

![IntelliSense 类型筛选](media/intellisense-typefiltering.gif)

## <a name="parameter-window"></a>参数窗口

IntelliSense 的另一个功能是能够在适当的位置提供参数列表。 参数列表提供所调用代码的方法签名的详细信息。 通过单击签名中的向上/向下箭头，可以循环浏览每个可用的参数签名，以确定最适合你需求的参数。 除允许的数据类型的细节之外，还可以通过 XML 注释在目标方法中定义描述。

![参数列表](media/intellisense-parameter.png)

在填写参数时，当前正在编辑的参数将以粗体显示，而非活动参数将具有标准权重。 


## <a name="triggering-completion-window-and-parameter-window"></a>触发完成窗口和参数窗口

在源文件中键入时，将自动触发完成窗口。 但也可以使用快捷方式 `control-space` 触发完成窗口。 此组合键将使完成列表显示在插入符号的当前位置。 

也可通过键入 `control-shift-space` 手动触发参数窗口的外观。 插入符号位于对参数列表有效的位置时，参数列表将出现在插入符号位置附近。

## <a name="see-also"></a>另请参阅

- [快速操作（Windows 上的 Visual Studio）](/visualstudio/ide/quick-actions)
- [重构代码（Windows 上的 Visual Studio）](/visualstudio/ide/refactoring-in-visual-studio)
