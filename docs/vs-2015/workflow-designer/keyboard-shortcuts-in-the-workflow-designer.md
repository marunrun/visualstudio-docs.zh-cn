---
title: 键盘快捷方式在工作流设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- WFDKeyboardShortcuts.UI
ms.assetid: 9be75438-a4a3-4781-94e5-45b7ec082358
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b1a03463d292fa1d4d980c62daa74b291d6a8cb1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62951952"
---
# <a name="keyboard-shortcuts-in-the-workflow-designer"></a>工作流设计器中的键盘快捷键
可通过键盘访问 [!INCLUDE[wfd1](../includes/wfd1-md.md)] 的所有核心功能。  
  
## <a name="navigating-the-workflow-designer-using-the-keyboard"></a>使用键盘导航工作流设计器  
 在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中，全局快捷键和调试快捷键适用于 [!INCLUDE[wfd2](../includes/wfd2-md.md)]。 此外，还创建了很多 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 特定的键盘快捷键。 在 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中，可以重新映射所有键盘快捷键。 但是，在重新承载的应用程序中，对这些键盘快捷键进行了硬编码。  
  
### <a name="workflow-designer-keyboard-shortcuts"></a>工作流设计器键盘快捷键  
 下表汇总了分配给 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 命令的默认键盘快捷键。  
  
|快捷键|用途|  
|--------------|-------------|  
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
 下表列出了通过键盘构造流程图所使用的笔势。 与在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 的其他内容中一样，会使用 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 提供的全局工具箱快捷键将活动添加到设计器图面。  
  
- 若要移动某个活动，请选择该活动并使用箭头键重新定位该活动。  
  
- 若要调整流程图的大小，请使用箭头键移动某个活动经过该流程图的当前边框。 将自动调整流程图的大小。  
  
- 若要将某个活动设置为开始节点，请使用**设置为 StartNode**命令的上下文菜单中。  
  
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
 默认情况下，用于 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 文本编辑的默认键盘快捷键适用于 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 中的表达式编辑器，但具有以下限制：  
  
- 重新映射以下命令的键盘快捷键无效。 编辑表达式时，只能使用默认的键盘快捷键访问这些命令。  
  
    1. 剪切  
  
    2. 复制  
  
    3. 粘贴  
  
    4. 全选  
  
    5. 撤消  
  
    6. 重做  
  
- 若要重新映射 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 的 [!INCLUDE[vs2010](../includes/vs2010-md.md)] 中表达式编辑命令的键盘快捷键，请在 [!INCLUDE[wfd2](../includes/wfd2-md.md)] 作用域中编辑这些快捷键。 在文本编辑器作用域所进行的更改不会自动应用于 [!INCLUDE[wfd2](../includes/wfd2-md.md)]。 如果您希望在这两个位置都重新映射快捷键，则必须应用两次更改（每个作用域应用一次）。