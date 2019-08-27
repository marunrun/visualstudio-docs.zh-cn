---
title: 工作流设计器：键盘快捷键
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- WFDKeyboardShortcuts.UI
ms.assetid: 9be75438-a4a3-4781-94e5-45b7ec082358
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b2026c61d05425f0f0d48a9fb722c62f760fcba2
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67825514"
---
# <a name="keyboard-shortcuts-in-the-workflow-designer"></a>工作流设计器中的键盘快捷键

可以通过键盘访问所有工作流设计器的核心功能。

## <a name="navigating-the-workflow-designer-using-the-keyboard"></a>使用键盘导航工作流设计器

在 Visual Studio 中，全局快捷键和调试快捷键适用于工作流设计器。 此外，已创建了大量工作流设计器特定的键盘快捷方式。 在 Visual Studio 中，所有键盘快捷方式可被重新映射。 但是，在重新承载的应用程序中，对这些键盘快捷键进行了硬编码。

### <a name="workflow-designer-keyboard-shortcuts"></a>工作流设计器键盘快捷键

下表总结了分配给工作流设计器命令的默认键盘快捷键。

|快捷键|用途|
|-|-------------|
|Ctrl+E，A|显示或隐藏自变量设计器。|
|Ctrl+E，C|就地折叠所选择的活动。|
|Ctrl+E，E|就地展开所选择的活动。|
|Ctrl+E，F|连接流程图中所选择的活动。|
|Ctrl+E，I|显示或隐藏导入项设计器。|
|Ctrl+E，M|将键盘焦点按 Tab 键顺序移到下一项。|
|Ctrl+E，N|在所选（或最近）活动的作用域内创建新变量。|
|Ctrl+E，O|显示或隐藏摘要图。|
|Ctrl+E，P|导航到所选活动的父活动。 这将进入痕迹导航中的上一级并更改设计器图面上的根活动。|
|Ctrl+E，S|将具有键盘焦点的项添加到当前选择中。|
|Ctrl+E，V|显示或隐藏变量设计器。|
|Ctrl+E，X|展开工作流中的所有活动。|
|Ctrl+Alt+F6|将键盘焦点从当前 UI 区域按顺序移到下一区域。 该顺序如下所示：<br /><br /> 1.痕迹导航栏。<br />2.设计器图面<br />3.自变量/变量/导入设计器（如果打开）<br />4.shell|

### <a name="flowchart"></a>流程图

下表列出了通过键盘构造流程图所使用的笔势。 如下所示余下的工作流设计器中，将活动添加到使用随 Visual Studio 一起提供的全局工具箱快捷键在设计器图面。

- 若要移动某个活动，请选择该活动并使用箭头键重新定位该活动。

- 若要调整流程图的大小，请使用箭头键移动某个活动经过该流程图的当前边框。 将自动调整流程图的大小。

- 若要将某个活动设置为开始节点，请使用**设置为 StartNode**中右键单击菜单命令。

- 连接活动：

    1. 通过按 Tab 键定位到活动来选择源活动。

    2. 根据需要按 Ctrl+E，M 多次将键盘焦点移至目标活动。

    3. 按 Ctrl+E，S 将目标活动添加到选择范围。

    4. 按 Ctrl+E，F 添加从源到目标的连接器。

有关通过键盘连接活动的说明：

- 通过在按 Ctrl+E，F 之前将多个活动添加到所选作用域可同时进行多个连接。按照向所选作用域添加活动的顺序进行连接。

- 如果某对活动无法连接（例如，源活动已具有一个传出连接），则仍会尽可能进行所选作用域内活动之间的其他连接。

- 当**FlowDecision**选定内容中包含和**FlowDecision**有没有传出连接器，连接器放置在**True**分支。

### <a name="expression-editing"></a>表达式编辑

默认情况下，Visual Basic 文本编辑的默认键盘快捷方式应用内部的表达式编辑器中工作流设计器中，有以下限制：

- 重新映射以下命令的键盘快捷键无效。 编辑表达式时，只能使用默认的键盘快捷键访问这些命令。

  - 剪切
  - 复制
  - 粘贴
  - 全选
  - 撤消
  - 重做

- 若要重新映射在 Visual Studio 中的工作流设计器内的表达式编辑命令的键盘快捷键，编辑工作流设计器作用域中的快捷方式。 工作流设计器自动不适用于在文本编辑器作用域中所做的更改。 如果您希望在这两个位置都重新映射快捷键，则必须应用两次更改（每个作用域应用一次）。
