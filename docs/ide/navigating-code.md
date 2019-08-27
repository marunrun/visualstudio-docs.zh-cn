---
title: 代码导航命令
ms.date: 08/14/2018
ms.topic: conceptual
helpviewer_keywords:
- code editor, navigation
- code editor, go to
- code editor, go to definition
- code editor, go to line
- code editor, peek definition
- code editor, navigation bar
- go to definition
- peek definition
- go to line
- go to
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1263b7a0ae65731eb618ffc925ff0f6310be0f4d
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68919517"
---
# <a name="navigate-code"></a>导航代码

Visual Studio 提供了许多用于在编辑器中导航代码的方法。 本主题汇总了导航代码的不同方法，并提供指向详细主题的链接。

## <a name="navigate-backward-and-navigate-forward-commands"></a>向后导航和向前导航命令

可使用工具栏上的“向后导航”(Ctrl+-) 和“向前导航”(Ctrl+Shift+-) 按钮，将插入点移到先前位置，或从先前位置返回到更新的位置        。 这些按钮保留插入点的最后 20 个位置。 这些命令还位于“视图”菜单中的“向后导航”和“向前导航”下    。

![向前和向后导航按钮](../ide/media/vs2017_nav_buttons.png)

## <a name="navigation-bar"></a>导航栏

可使用“导航栏”（代码窗口顶部的下拉框），在基本代码中导航代码  。 选择类型或成员即可直接转到。 在 Visual Basic、C# 或 C++ 代码库中编辑代码时，可以看到导航栏。 在分部类中，可能会禁用在当前代码文件之外定义的成员（灰显）。

![代码导航栏](../ide/media/vside_navigation_bar.png)

可围绕下拉框导航，如下所示：

- 若要导航到当前文件所属的另一个项目，请在左侧下拉列表中进行选择。

- 若要导航到类或类型，请在中间的下拉列表中进行选择。

- 若要直接导航到类中的过程或其他成员，请在右侧下拉列表中进行选择。

- 若要将焦点从代码窗口切换到导航栏，请按快捷组合键 Ctrl+F2   。

- 若要在导航栏上的框之间切换焦点，请按 Tab 键  。

- 若要选择具有焦点的导航栏项并返回到代码窗口，请按 Enter 键  。

- 若要在不选择任何项的情况下将焦点从导航栏返回到代码中，请按 Esc 键  。

若要隐藏导航栏，请在“文本编辑器”的“所有语言”设置中更改“导航栏”选项（依次选择“工具” > “选项” > “文本编辑器” > “所有语言”），也可以单独更改各语言的设置       。

## <a name="find-all-references"></a>查找所有引用

在解决方案中查找对选定元素的所有引用。 可以使用此操作检查大型重构可能的副作用，或者验证“死”代码。 按 **F8** 可在结果之间跳转。 有关详细信息，请参阅[在代码中查找引用](finding-references.md)。

输入 | 函数
------------ | ---
**键盘** | 将文本游标放置在类型名称内部的某个位置，然后按 Shift+F12  
**鼠标** | 选择右键单击菜单中的“查找所有引用” 

## <a name="reference-highlighting"></a>引用突出显示

单击源代码中的符号时，将在文档中突出显示该符号的所有实例。 突出显示的符号可能包括声明和引用，以及许多其他“查找所有引用”  将返回的符号。 其中包括类、对象、变量、方法和属性的名称。 在 Visual Basic 代码中，也将突出显示许多控件结构的关键字。 若要移至下一个或上一个突出显示的符号，请按 Ctrl+Shift+向下键或 Ctrl+Shift+向上键       。 可以在“工具” > “选项” > “环境” > “字体和颜色” > “突出显示的引用”中更改突出显示的颜色      。

## <a name="go-to-commands"></a>“转到”命令

“转到”包含以下位于“编辑”菜单中“转到”下的命令   ：

- “转到行”(Ctrl+G)    ：移到活动文档中的指定行号。

- “转到全部”（Ctrl+T 或 Ctrl+      ：移到指定的行、类型、文件、成员或符号。

- “转到文件”（Ctrl+1、Ctrl+F）      ：移到解决方案中的指定文件。

- “转到最近使用的文件”（Ctrl+1、Ctr+R）      ：转到解决方案中最近访问过的指定文件。

- “转到类型”（Ctrl+1、Ctrl+T）      ：移到解决方案中的指定类型。

- “转到成员”（Ctrl+1、Ctrl+M）      ：移到解决方案中的指定成员。

- “转到符号”（Ctrl+1、Ctrl+S）      ：移到解决方案中的指定符号。

在 Visual Studio 2017 版本 15.8 及更高版本中，还提供了以下“转到”导航命令  ：

- 转到文件中的下一个问题 (Alt+PgDn)和转到文件中的上一个问题 (Alt+PgUp)      

- 转到上次编辑位置 (Ctrl+Shift+Backspace)    

有关这些命令的详细信息，请参阅[使用“转到”命令查找代码](../ide/go-to.md)主题。

## <a name="go-to-definition"></a>转到定义

通过“转到定义”，可转到所选元素的定义。 有关详细信息，请参阅[转到定义和查看定义](../ide/go-to-and-peek-definition.md)。

输入 | 函数
------------ | ---
**键盘** | 将文本游标放置在类型名称内部的某个位置，然后按 **F12**
**鼠标** | 右键单击类型名称，然后选择“转到定义”，或者按“Ctrl”并单击类型名称  

## <a name="peek-definition"></a>查看定义

“查看定义”会在窗口中显示所选元素的定义，用户无需离开在代码编辑器中的当前位置。 有关详细信息，请参阅[如何：使用“查看定义”](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)和[“转到定义和查看定义”](../ide/go-to-and-peek-definition.md)查看和编辑代码。

输入 | 函数
------------ | ---
**键盘** | 将文本游标放置在类型名称内部的某个位置，然后按 Alt+F12  
**鼠标** | 右键单击类型名称，选择“查看定义”，或者按 Ctrl 并单击类型名称（如果已选中“在速览视图中打开定义”选项）   

## <a name="go-to-implementation"></a>转到实现

使用“转到实现”，可从一个基类或类型导航到其实现。 如果有多个实现，则可以看到它们在“查找符号结果”  窗口中列出：

输入 | 函数
------------ | ---
**键盘** | 将文本游标放置在类型名称内部的某个位置，然后按 Ctrl+F12  
**鼠标** | 右键单击类型名称，再选择“转到实现”  。

## <a name="call-hierarchy"></a>调用层次结构

可以在[“调用层次结构”窗口](../ide/reference/call-hierarchy.md)中查看方法的调用方和被调用方：

输入 | 函数
------------ | ---
**键盘** | 将文本游标放置在类型名称内部的某个位置，然后按 Ctrl+K、Ctrl+T    
**鼠标** | 右键单击成员名称并选择“查看调用层次结构” 

## <a name="next-method-and-previous-method-commands-visual-basic"></a>“下一个方法”和“上一个方法”命令 (Visual Basic)

在 Visual Basic 代码文件中，使用这些命令将插入点移动到不同的方法。 选择“编辑” > “下一个方法”或“编辑” > “上一个方法”     。

## <a name="structure-visualizer"></a>结构可视化工具

代码编辑器中的结构可视化工具功能可显示“结构参考线”，即指明代码库中成对大括号的垂直虚线  。 这样一来，你可以更加轻松地判断逻辑块的开始和结束位置。

![结构可视化工具](../ide/media/vside_structure_visualizer.png)

若要禁用结构参考线，请转到“工具” > “选项” > “文本编辑器” > “常规”，然后取消选中“显示结构参考线”框      。

## <a name="enhanced-scroll-bar"></a>增强型滚动条

可以在代码窗口中使用增强型滚动条获取代码的鸟瞰视图。 在映射模式下，当游标在滚动条中上下移动时可评审代码的预览。 有关详细信息，请参阅[如何：通过自定义滚动条来跟踪代码](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md)。

## <a name="codelens-information"></a>CodeLens 信息

在代码编辑器中使用 CodeLens 时，可以找到有关特定代码的信息，如更改和更改者、引用、Bug、工作项、代码评审和单元测试状态。 将 Visual Studio Enterprise 与 Team Foundation Server 一起使用时，CodeLens 的工作原理类似于警告显示。 请参阅[查找代码更改和其他历史记录](../ide/find-code-changes-and-other-history-with-codelens.md)。

## <a name="see-also"></a>请参阅

- [代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)
- [查看调用层次结构](../ide/reference/call-hierarchy.md)
