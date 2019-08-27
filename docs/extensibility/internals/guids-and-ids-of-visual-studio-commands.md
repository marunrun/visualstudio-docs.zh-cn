---
title: Visual Studio 命令的 Guid 和 Id |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands
- id
- command placement
- visual studio command
- guid
ms.assetid: 2ea4bee2-0259-4675-8e65-2023b312b516
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 89274600d05b787182ac447902555f7d703851c2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66329189"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>Guid 和 Id 的 Visual Studio 命令
Visual Studio SDK 的一部分安装的.vsct 文件中定义的 Visual Studio 集成的开发环境 (IDE) 中包含的命令的 GUID 和 ID 值。 有关详细信息，请参阅[IDE 定义的命令、 菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)。

 有关如何使用 IDE 对象中定义的详细信息 *.vsct*文件，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

## <a name="find-a-command-definition"></a>查找命令定义
 由于 Visual Studio 定义 1000 多个命令，是不切合实际它们全部列出。 相反，请执行以下步骤来查找命令的定义。

### <a name="to-locate-a-command-definition"></a>若要查找命令定义

1. 在 Visual Studio 中打开以下文件中的 *< Visual Studio SDK 安装路径\>\VisualStudioIntegration\Common\Inc\\* 文件夹：*SharedCmdDef.vsct*， *ShellCmdDef.vsct*， *VsDbgCmdUsed.vsct*， *Venusmenu.vsct*。

    Visual Studio 的大多数命令中定义*SharedCmdDef.vsct*并*ShellCmdDef.vsct*。 *VsDbgCmdUsed.vsct*定义与调试器相关的命令和*Venusmenu.vsct*定义特定于 Web 开发的命令。

2. 如果该命令的菜单项，记下的菜单项的确切文本。 如果该命令是按钮在工具栏上的，请注意将显示在其上悬停时的工具提示文本。

3. 按**Ctrl**+**F**以打开**查找**对话框。

4. 在中**查找内容**框中，键入在步骤 2 中记下的文本。

5. 确认**所有打开的文档**中显示**查找**框。

6. 单击**查找下一步**按钮，直至在中选择文本`<Strings>`一部分[Button 元素](../../extensibility/button-element.md)。

    `<Button>`命令也显示在的元素是命令定义。

   在您找到命令定义，您可以将副本放命令的另一个菜单或工具栏上通过创建[CommandPlacement 元素](../../extensibility/commandplacement-element.md)具有相同`guid`和`id`与命令的值。 有关详细信息，请参阅[创建可重用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)。

### <a name="special-cases"></a>特殊情况
 在以下情况下，菜单文本或工具提示文本可能不完全匹配中的命令定义。

- 包括带下划线的字符，如下所述的菜单项**打印**命令**文件**菜单中的，在其中*P*带下划线。

     与符号前面的字符 (&) 菜单项名称中的字符将显示为带下划线。 但是， *.vsct*文件写入在 XML 中，它使用与号 (&) 字符以指示特殊字符，并要求必须在作为拼写与号以显示 *&amp;a m p;* 。 因此，在 *.vsct*文件中，**打印**命令将显示为 *&amp;a m p;打印*。

- 命令，具有动态文本，如 **保存** \<当前文件名\>，动态生成菜单项，例如各项 **最近使用的文件** 列表。

     没有可靠的方法来搜索动态文本。 相反，查找所需的命令在承载的咨询的组[Guid 和 Id 的 Visual Studio 菜单](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)或[Guid 和 Id 的 Visual Studio 工具栏](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)，并搜索该组的 ID。 如果命令定义不具备组作为其[父元素](../../extensibility/parent-element.md)，搜索*SharedCmdPlace.vsct*并*ShellCmdPlace.vsct* (或*VsDbgCmdPlace.vsct*调试器命令) 为`<CommandPlacement>`设置命令的父级的元素。 *SharedCmdPlace.vsct*， *ShellCmdPlace.vsct*，和*VsDbgCmdPlace.vsct*位于 *\<Visual Studio SDK 安装路径\>\VisualStudioIntegration\Common\Inc\\* 文件夹。

## <a name="see-also"></a>请参阅
- [MenuCommands 与OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md)
- [Visual Studio 命令表格 (.vsct) 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)
