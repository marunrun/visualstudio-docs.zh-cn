---
title: 命令 Guid 和 Id |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands
- id
- command placement
- visual studio command
- guid
ms.assetid: 2ea4bee2-0259-4675-8e65-2023b312b516
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2feef3cbe72b7eb8db96052236fe483733e22273
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62538133"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>Visual Studio 命令中的 GUID 和 ID
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio SDK 的一部分安装的.vsct 文件中定义的 Visual Studio 集成的开发环境 (IDE) 中包含的命令的 GUID 和 ID 值。 有关详细信息，请参阅[IDE-Defined 命令、 菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)。

 有关如何使用.vsct 文件中定义的 IDE 对象的详细信息，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

## <a name="finding-a-command-definition"></a>查找命令定义
 由于 Visual Studio 定义多个一千命令，是不切合实际它们全部列出。 相反，请执行以下步骤来查找命令的定义。

#### <a name="to-locate-a-command-definition"></a>若要查找命令定义

1. 在 Visual Studio 中打开以下文件中的*Visual Studio SDK 安装路径*\VisualStudioIntegration\Common\Inc\ 文件夹：SharedCmdDef.vsct，ShellCmdDef.vsct，VsDbgCmdUsed.vsct，Venusmenu.vsct。

    Visual Studio 的大多数命令 SharedCmdDef.vsct 和 ShellCmdDef.vsct 中定义。 VsDbgCmdUsed.vsct 定义与调试器相关的命令和 Venusmenu.vsct 定义特定于 Web 开发的命令。

2. 如果该命令的菜单项，记下的菜单项的确切文本。 如果该命令是按钮在工具栏上的，请注意将显示在其上悬停时的工具提示文本。

3. 按 CTRL + F 打开**查找**对话框。

4. 在中**查找内容**框中，键入在步骤 2 中记下的文本。

5. 确认**所有打开的文档**中显示**查找**框。

6. 单击**查找下一步**按钮，直至在中选择文本`<Strings>`一部分[Button 元素](../../extensibility/button-element.md)。

    `<Button>`命令也显示在的元素是命令定义。

   在您找到命令定义，您可以将副本放命令的另一个菜单或工具栏上通过创建[CommandPlacement 元素](../../extensibility/commandplacement-element.md)具有相同`guid`和`id`与命令的值。 有关详细信息，请参阅[按钮创建可重用组](../../extensibility/creating-reusable-groups-of-buttons.md)。

### <a name="special-cases"></a>特殊情况
 在以下情况下，菜单文本或工具提示文本可能不完全匹配中的命令定义。

- 包括带下划线的字符，如下所述的菜单项**打印**命令**文件**菜单中，P 是否带下划线。

     在菜单项名称中的 & 字符前面的字符显示为带下划线。 不过，在 XML 中，它使用 & 字符以指示特殊字符，并需要显示 & 符必须拼写出来写入.vsct 文件为&amp;。 因此，在.vsct 文件中，**打印**命令将显示为&amp;打印。

- 命令，具有动态文本，如**保存***当前文件名*，动态生成菜单项，例如各项**最近使用的文件**列表。

     没有可靠的方法来搜索动态文本。 相反，查找所需的命令在承载的咨询的组[Guid 和 Id 的 Visual Studio 菜单](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)或[Guid 和 Id 的 Visual Studio 工具栏](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)，并搜索该组的 ID。 如果命令定义不具备组作为其[父元素](../../extensibility/parent-element.md)，搜索 SharedCmdPlace.vsct 和 ShellCmdPlace.vsct （或调试器命令 VsDbgCmdPlace.vsct）`<CommandPlacement>`设置的父级的元素命令。 SharedCmdPlace.vsct，ShellCmdPlace.vsct，andVsDbgCmdPlace.vsct 处于*Visual Studio SDK 安装路径*\VisualStudioIntegration\Common\Inc\ 文件夹。

## <a name="see-also"></a>请参阅
 [MenuCommands 与OleMenuCommands](../../misc/menucommands-vs-olemenucommands.md) [Visual Studio 命令表 (。Vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md) [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)
