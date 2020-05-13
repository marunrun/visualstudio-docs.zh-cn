---
title: 重构代码
description: 使用源分析，可轻松重新组织 Visual Studio for Mac 中的代码。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 05/06/2018
ms.assetid: C7782BF3-016F-4B41-8A81-85FC540A1A8F
ms.custom: video
ms.openlocfilehash: 7b11f09d8fb70612d4496987f69583b2ac691275
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "74985237"
---
# <a name="refactoring"></a>Refactoring

重构代码方法可重新排列、重构和阐明现有代码，同时确保代码总体行为保持不变。

重构生成高质量的基本代码，使代码更易于使用、读取和管理，方便你或任何其他开发者或用户参考。

Visual Studio for Mac 与 Roslyn（Microsoft 的开源 .NET 编译器平台）集成之后支持更多重构操作。

## <a name="renaming"></a>重命名

任何代码标识符（例如，类名、属性名等）都可使用“重命名”重构命令来查找该标识符所有的出现次数并更改它们  。 若要重命名某个符号，请右键单击该符号，并选择“重构”>“重命名”，或“Cmd + R”键绑定：  

![重命名菜单项](media/refactoring-renaming1.png)

将突出显示符号和对该符号的任何引用。 开始键入新名称时，它会自动更改代码中的所有引用。可通过按 Enter 示意重命名完成  ：

![重命名和标识符](media/refactoring-renaming2.png)

## <a name="context-actions"></a>上下文操作

可使用上下文操作检查任何 C# 代码，查看所有可能的重构选项。

“解析”和“重构”上下文项已合并为单一的“快速修复...”项，用于提供所有可用的上下文操作：   

![显示上下文项](media/refactoring-context-action.png)

将鼠标悬停在任意上下文操作上可预览添加到代码或从代码中删除的内容。

也可在代码任何位置按“选项 + Enter”： 

![“选项 + Enter”上下文项](media/refactoring-image2a.png)

要启用这些选项，必须在选项“Visual Studio for Mac”>“首选项”>“文本编辑器”>“源分析”中选择“启用所有已打开文件的源分析”：  

![启用源分析](media/refactoring-options.png)

可能的建议操作具有 100 多个，可通过浏览到“Visual Studio for Mac”>“首选项”>“源分析”>“C#”>“代码操作”，并选中或取消选中操作旁的框，启用或禁用它们  。

![C# 源分析操作](media/refactoring-image3a.png)

### <a name="common-context-actions"></a>常见上下文操作

下面介绍一些最常用的上下文操作。

#### <a name="extract-method"></a>提取方法

提取方法重构操作可以通过提取现有成员的代码选择创建新方法。 此操作将完成两件事情：

* 创建包含所选代码的新方法
* 在所选代码所在的位置调用新方法。

##### <a name="example"></a>示例

1. 添加以下代码：

```csharp
    class MainClass
    {

        double CalculatePyramidVolume(double baseArea, double height)
        {

            double volume = (baseArea * height) / 3;

            return volume;
        }
    }
```

2. 突出显示 `double volume = (baseArea * height) / 3;` 行，右键单击该行，并选择“重构”>“提取方法”  。

3. 使用箭头键选择在代码中放置新方法的位置。

#### <a name="encapsulate-field"></a>封装字段

封装字段操作可以从现有的字段创建属性，并更新代码以引用新创建的属性。 通过创建封装字段的属性，可禁止对公共字段的直接访问，这表示其他对象无法修改它。

该操作将完成以下功能：

* 将访问修饰符改为专用。
* 为该字段生成 Getter 和 Setter（除非字段为只读，此时将只创建 Getter）。

## <a name="source-analysis"></a>源分析

源分析通过对潜在错误和样式冲突添加下划线并提供自动修复作为上下文操作对代码进行即时分析。

通过查看文本编辑器右侧的滚动条，可在任何时间查看任何文件源分析的所有结果：

![源分析边栏](media/refactoring-image4a.png)

单击顶部的圆圈可循环访问每条建议，严重性最高的问题将最先显示。 将鼠标悬停在单个结果或行上时将显示该问题，可通过上下文操作对问题进行修复：

![源分析项](media/refactoring-image5.png)

## <a name="related-video"></a>相关视频

> [!Video https://channel9.msdn.com/Shows/Visual-Studio-Toolbox/Visual-Studio-for-Mac-Refactoring-Code/player]

## <a name="see-also"></a>另请参阅

- [快速操作（Windows 上的 Visual Studio）](/visualstudio/ide/quick-actions)
- [重构代码（Windows 上的 Visual Studio）](/visualstudio/ide/refactoring-in-visual-studio)