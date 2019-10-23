---
title: 快速操作、灯泡和螺丝刀
ms.date: 03/28/2018
ms.topic: conceptual
author: jillre
ms.author: jillfra
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 18df1378218d2188ee78d1b1b2a991e35f5ed689
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72666759"
---
# <a name="quick-actions"></a>快速操作

通过快速操作，只凭单个操作便可轻松重构、生成或修改代码。 快速操作可用于 C#、[C++](/cpp/ide/writing-and-refactoring-code-cpp) 和 Visual Basic 代码文件。 某些操作特定于一种语言，而其他操作适用于所有语言。

可使用“快速操作”功能：

- 通过代码修复[代码分析器](../code-quality/roslyn-analyzers-overview.md)规则冲突

::: moniker range=">=vs-2019"

- [阻止](../code-quality/use-roslyn-analyzers.md#suppress-violations)代码分析器规则冲突或[配置](../code-quality/use-roslyn-analyzers.md#automatically-configure-rule-severity)其严重性

::: moniker-end

::: moniker range="vs-2017"

- [阻止](../code-quality/use-roslyn-analyzers.md#suppress-violations)代码分析器规则冲突

::: moniker-end

- 应用重构（例如，[内联临时变量](../ide/reference/inline-temporary-variable.md)）

- 生成代码（例如，[引入局部变量](../ide/reference/introduce-local-variable.md)）

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[重构 (Visual Studio for Mac)](/visualstudio/mac/refactoring)。

可使用灯泡![灯泡图标](media/light-bulb-icon.png)或螺丝刀![螺丝刀图标](media/screwdriver-icon.png)图标，或按“Ctrl”  应用快速操作。+  当光标位于可操作的代码行上时， 如果出现指示错误的红色波形曲线，且 Visual Studio 有针对该错误的可用修复方法，会显示一个错误灯泡 ![错误灯泡图标](media/error-light-bulb-icon.png)。

第三方可针对任何语言提供自定义诊断和建议，例如在 SDK 中提供；同时根据这些规则，Visual Studio 电灯泡可能会显示。

## <a name="icons"></a>图标

当存在可用的快速操作时，会出现一个图标，指示可用的修复方法或重构的类型。 螺丝刀  ![螺丝刀图标](media/screwdriver-icon.png)图标仅指示存在可用于更改代码的操作，但不一定要使用它们。 黄色灯泡  ![灯泡图标](media/light-bulb-icon.png)图标指示存在应  执行的、用于改进代码的可用操作。 错误灯泡  ![错误灯泡图标](media/error-light-bulb-icon.png)图标指示存在可用于修复代码中的错误的操作。

## <a name="to-see-a-light-bulb-or-screwdriver"></a>查看灯泡或螺丝刀

如果有可用的修补程序，在以下情况下会显示灯泡：

- 当鼠标悬停在错误位置时

   ![带鼠标悬停的灯泡](../ide/media/vs2015_lightbulb_hover.png)

- 将插入点（光标）移到相应的代码行时，显示在编辑器的左边距中

还可按 Ctrl+   。 可在行的任意位置查看可用快速操作和重构的列表。

若要查看可能的修补程序，请选择灯泡旁边的下箭头或“显示可能的修补程序”  链接。 此时会显示可用的“快速操作”列表。

![灯泡已展开](../ide/media/vs2015_lightbulb_hover_expanded.png)

## <a name="see-also"></a>请参阅

- [Visual Studio 中的代码生成](../ide/code-generation-in-visual-studio.md)
- [常见快速操作](../ide/common-quick-actions.md)
- [代码样式和快速操作](../ide/code-styles-and-code-cleanup.md)
- [编写和重构代码 (C++)](/cpp/ide/writing-and-refactoring-code-cpp)
- [重构 (Visual Studio for Mac)](/visualstudio/mac/refactoring)