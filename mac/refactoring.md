---
title: 重构代码
description: 使用 Visual Studio for Mac 和快速操作优化代码。
author: cobey
ms.author: cobey
ms.date: 03/29/2019
ms.assetid: C7782BF3-016F-4B41-8A81-85FC540A1A8F
ms.custom: video
ms.openlocfilehash: 5a87b87f3a14462daec1e069fe222164818d2a19
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "67691287"
---
# <a name="refactoring"></a>Refactoring

重构代码方法可重新排列、重构和阐明现有代码，同时确保代码总体行为保持不变。

重构生成高质量的基本代码，使代码更易于使用、读取和管理，方便你或任何其他开发者或用户参考。

Visual Studio for Mac 与 Roslyn（Microsoft 的开源 .NET 编译器平台）集成之后支持更多重构操作。

## <a name="renaming"></a>重命名

任何代码标识符（例如，类名、属性名等）都可使用“重命名”重构命令来查找该标识符所有的出现次数并更改它们  。 若要重命名某个符号，请右键单击该符号，并选择“重命名...”，或使用“Cmd (⌘) + R”键绑定   ：

![重命名菜单项](media/refactoring-renaming1.png)

将突出显示符号和对该符号的任何引用。 开始键入新名称时，它会自动更改代码中的所有引用，按 Enter 可提交所做的更改  ：

![重命名和标识符](media/refactoring-renaming2.png)

## <a name="quick-actions"></a>快速操作

通过快速操作，只凭单个操作便可轻松重构、生成或修改代码。

可使用“快速操作”功能：

* 对代码分析器规则冲突应用代码修复
* 阻止代码分析器规则冲突
* 应用重构（例如，内联临时变量）
* 生成代码（例如，引入局部变量）

可使用灯泡![灯泡图标](media/quick-actions-light-bulb-icon.png)或螺丝刀![螺丝刀图标](media/quick-actions-screwdriver-icon.png)图标，或当光标位于操作就绪的代码行上时按 Option (⌥)+Enter 来应用快速操作。 如果出现指示错误的红色波形曲线，且 Visual Studio 有针对该错误的可用修复方法，会显示一个错误灯泡![错误灯泡图标](media/quick-actions-error-light-bulb-icon.png)。

第三方可针对任何语言提供自定义诊断和建议，例如随附 SDK 提供，同时根据这些规则，Visual Studio 电灯泡可能亮起。

### <a name="quick-action-icons"></a>快速操作图标
当存在可用的快速操作时，会出现一个图标，指示可用的修复方法或重构的类型。 螺丝刀  ![ 螺丝刀图标](media/quick-actions-screwdriver-icon.png)图标仅指示存在可用于更改代码的操作，但不一定要使用它们。 黄色灯泡  ![灯泡图标](media/quick-actions-light-bulb-icon.png)图标指示存在应  执行的、用于改进代码的可用操作。 错误灯泡  ![错误灯泡图标](media/quick-actions-error-light-bulb-icon.png)图标指示存在可用于修复代码中的错误的操作。

### <a name="to-see-a-light-bulb-or-screwdriver"></a>查看灯泡或螺丝刀

- 如果有可用的修复方法，将鼠标悬停在存在错误的位置时，会同时显示灯泡。

   ![带鼠标悬停的灯泡](media/refactoring-lightbulb-hover.png)

- 将脱字号移动到可使用快速操作的代码行时，编辑器左边距中会显示灯泡和螺丝刀。

- 在行的任意位置按 Option (⌥)+Enter，可查看可用快速操作和重构的列表。

![显示上下文项](media/refactoring-context-action.png)

将鼠标悬停在任意上下文操作上可预览添加到代码或从代码中删除的内容。

![“选项 + Enter”上下文项](media/refactoring-image2a.png)

要启用这些选项，必须在选项“Visual Studio for Mac”>“首选项”>“文本编辑器”>“源分析”中选择“启用所有已打开文件的源分析”：  

![启用源分析](media/refactoring-options.png)

可能的建议操作具有 100 多个，可通过浏览到“Visual Studio for Mac”>“首选项”>“源分析”>“C#”>“代码操作”，并选中或取消选中操作旁的框，启用或禁用它们  。

![C# 源分析操作](media/refactoring-image3a.png)

### <a name="common-quick-actions"></a>常见快速操作

可在[常见快速操作](/visualstudio/ide/common-quick-actions)一文中了解有关常见快速操作的详细信息。

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