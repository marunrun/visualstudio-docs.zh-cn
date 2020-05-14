---
title: Visual Studio 命令的 GUID 和 IT |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands
- id
- command placement
- visual studio command
- guid
ms.assetid: 2ea4bee2-0259-4675-8e65-2023b312b516
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8932f23d301eabc97414bf76453d70336e0dabae
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708256"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>Visual Studio 命令的 GUID 和 IT
Visual Studio 集成开发环境 （IDE） 中包含的命令的 GUID 和 ID 值在作为 Visual Studio SDK 的一部分安装的 .vsct 文件中定义。 有关详细信息，请参阅[IDE 定义的命令、菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)。

 有关如何处理*在 .vsct*文件中定义的 IDE 对象的详细信息，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

## <a name="find-a-command-definition"></a>查找命令定义
 由于 Visual Studio 定义了 1000 多个命令，因此在此处列出所有这些命令是不切实际的。 相反，请按照以下步骤查找命令的定义。

### <a name="to-locate-a-command-definition"></a>查找命令定义

1. 在 Visual Studio 中，在 *<Visual Studio\>SDK 安装路径 [VisualStudio\\集成]公共_Inc*文件夹中打开以下文件：SharedCmdDef.vsct、ShellCmdDef.vsct、VsDbgCmdUsed.vsct、Venusmenu.vsct 。 *SharedCmdDef.vsct* *ShellCmdDef.vsct* *VsDbgCmdUsed.vsct* *Venusmenu.vsct*

    大多数可视化工作室命令在*SharedCmdDef.vsct*和*ShellCmdDef.vsct 中*定义。 *VsDbgCmdUsed.vsct*定义与调试器相关的命令 *，Venusmenu.vsct*定义特定于 Web 开发的命令。

2. 如果命令是菜单项，请注意菜单项的确切文本。 如果该命令是工具栏上的按钮，请注意暂停时显示的工具提示文本。

3. 按**Ctrl**+**F**打开"**查找"** 对话框。

4. 在"**查找内容"** 框中，键入您在步骤 2 中注意到的文本。

5. 验证**所有打开的文档**是否显示在"**查看"** 框中。

6. 单击"**查找下一步**"按钮，直到在`<Strings>`[按钮元素](../../extensibility/button-element.md)部分中选择文本。

    该`<Button>`命令中显示的元素是命令定义。

   找到命令定义后，可以通过创建与命令具有相同`guid`和`id`值的 Command[放置元素](../../extensibility/commandplacement-element.md)将命令的副本放在另一个菜单或工具栏上。 有关详细信息，请参阅[创建可重用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)。

### <a name="special-cases"></a>特殊情况
 在以下情况下，菜单文本或工具提示文本可能不完全匹配命令定义中的内容。

- 包含带下划线字符的菜单项，如 **"文件**"菜单上的 **"打印"** 命令，其中*P*加下下划线。

     菜单项名称中由 & 字符开头的字符显示为下划线。 但是 *，.vsct*文件用 XML 编写，它使用安培 （&） 字符来指示特殊字符，并且要求必须显示要显示的放大器必须拼写为*&amp;amp;* 因此，在 *.vsct*文件中，"**打印"** 命令显示为*&amp;amp;打印*。

- 具有动态文本的命令，如 **"保存**\<当前文件名\>"和动态生成的菜单项，如 **"最近文件**"列表中的项目。

     没有可靠的方法来搜索动态文本。 相反，通过查阅 Visual Studio 菜单的[GUID 和 ID](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)或 Visual Studio[工具栏的 GUID 和 ID，](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)并搜索该组的 ID，找到承载所需命令的组。 如果命令定义没有将组作为其[父元素](../../extensibility/parent-element.md)，则搜索*SharedCmdPlace.vsct*和*ShellCmdPlace.vsct（* 或用于调试器命令的*VsDbgCmdPlace.vsct）* 的元素`<CommandPlacement>`，以设置命令的父元素。 *SharedCmdPlace.vsct* *、ShellCmdPlace.vsct*和*VsDbgCmdPlace.vsct*位于*\<可视化工作室 SDK\>安装路径 [VisualStudio\\集成]通用_Inc*文件夹中。

## <a name="see-also"></a>请参阅

- [可视化工作室命令表 （.vsct） 文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSCT XML 架构引用](../../extensibility/vsct-xml-schema-reference.md)
