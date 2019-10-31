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
ms.openlocfilehash: f7670eacc875bf7c5437d9bb92cc1932753093bd
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186639"
---
# <a name="guids-and-ids-of-visual-studio-commands"></a>Visual Studio 命令的 Guid 和 Id
Visual Studio 集成开发环境（IDE）中包含的命令的 GUID 和 ID 值是在作为 Visual Studio SDK 的一部分安装的 .vsct 文件中定义的。 有关详细信息，请参阅[IDE 定义的命令、菜单和组](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)。

 有关如何使用 *.vsct*文件中定义的 IDE 对象的详细信息，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

## <a name="find-a-command-definition"></a>查找命令定义
 由于 Visual Studio 定义的命令超过1000，因此在此处列出它们都不切实际。 相反，请按照以下步骤查找命令的定义。

### <a name="to-locate-a-command-definition"></a>查找命令定义

1. 在 Visual Studio 中，打开 *< Visual STUDIO SDK 安装路径\>\VisualStudioIntegration\Common\Inc\\* 文件夹中的以下文件： *.vsct*、 *ShellCmdDef*、.vsct *、VsDbgCmdUsed、* *Venusmenu. .vsct*。

    大多数 Visual Studio 命令是在*SharedCmdDef. .vsct*和*ShellCmdDef*中定义的。 *VsDbgCmdUsed*定义了与调试器相关的命令，而*Venusmenu*定义了特定于 Web 开发的命令。

2. 如果命令为菜单项，请注意菜单项的确切文本。 如果命令是工具栏上的按钮，请注意在它上暂停时显示的工具提示文本。

3. 按**Ctrl**+**F**打开 "**查找**" 对话框。

4. 在 "**查找内容**" 框中，键入你在步骤2中记下的文本。

5. 验证**所有打开的文档**是否都显示在 "**查找范围**" 框中。

6. 单击 "**查找下一个**" 按钮，直到在[button 元素](../../extensibility/button-element.md)的 "`<Strings>`" 部分中选择了文本。

    命令出现在其中的 `<Button>` 元素是命令定义。

   找到命令定义后，可以通过创建与命令具有相同 `guid` 和 `id` 值的[CommandPlacement 元素](../../extensibility/commandplacement-element.md)，将命令的副本放在另一个菜单或工具栏上。 有关详细信息，请参阅[创建可重用的按钮组](../../extensibility/creating-reusable-groups-of-buttons.md)。

### <a name="special-cases"></a>特殊情况
 在以下情况下，菜单文本或工具提示文本可能与命令定义中的内容不完全匹配。

- 包含带下划线字符的菜单项，如 "**文件**" 菜单上的 "**打印**" 命令，其中*P*带有下划线。

     菜单项名称中前面带有 "and" 符（&）字符的字符以下划线显示。 但是， *.vsct*文件以 XML 编写，后者使用 "and" 符（&）字符指示特殊字符，并要求要显示的 "符号" 必须以 *&amp;amp*形式出现。 因此，在 *.vsct*文件中， **Print**命令显示为 *&amp;amp;打印*。

- 具有动态文本的命令（如**Save** \<当前文件名\>和动态生成的菜单项，如 "**最近的文件**" 列表中的项）。

     没有可靠的方法可对动态文本进行搜索。 相反，请通过咨询[Visual studio 菜单的 guid 和 id](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)和[visual Studio 工具栏的 guid 和](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)id，并搜索该组的 id 来查找托管所需命令的组。 如果命令定义没有组作为其[父元素](../../extensibility/parent-element.md)，则在设置父级的 `<CommandPlacement>` 元素的 *.vsct*和 *.vsct* *（或 VsDbgCmdPlace for 调试程序命令*）中搜索command. *.Vsct*、 *ShellCmdPlace* *\<Visual Studio SDK 安装路径\>VsDbgCmdPlace\\* "文件夹*中。*

## <a name="see-also"></a>请参阅

- [Visual Studio 命令表（.vsct）文件](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [.VSCT XML 架构引用](../../extensibility/vsct-xml-schema-reference.md)
