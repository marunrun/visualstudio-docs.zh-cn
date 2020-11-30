---
title: 设计 XML 命令表 (。.Vsct) 文件 |Microsoft Docs
description: 了解如何设计 XML 命令表 ( .vsct) 文件，该文件描述命令项的布局和外观，包括按钮、组合框、菜单和工具栏。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, designing
ms.assetid: bb87a322-bac4-4258-92bc-9a876f05d653
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a1ccab1eddf38e2f93cb00f1f5fdea6ce09f2f05
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "96328426"
---
# <a name="design-xml-command-table-vsct-files"></a>设计 XML 命令表 ( .vsct) 文件
XML 命令表 (*.vsct*) 文件描述 VSPackage 的命令项的布局和外观。 命令项包括按钮、组合框、菜单、工具栏和命令项组。 本文介绍 XML 命令表文件、它们如何影响命令项和菜单，以及如何创建它们。

## <a name="commands-menus-groups-and-the-vsct-file"></a>命令、菜单、组和 .vsct 文件
 *.Vsct* 文件是围绕命令、菜单和命令组进行组织的。 *.Vsct* 文件中的 XML 标记表示每个项，以及其他关联项，如命令按钮、命令位置和位图。

 通过运行包模板来创建新的 VSPackage 时 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ，模板会生成一个 *.vsct* 文件，其中包含菜单命令、工具窗口或自定义编辑器的必要元素，具体取决于所做的选择。 然后，可以修改此 *.vsct* 文件以满足特定 VSPackage 的要求。 有关如何修改 *.vsct* 文件的示例，请参阅 [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

 若要创建新的空白 *.vsct* 文件，请参阅 how [to： create a *.vsct* file](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)。 创建后，将 XML 元素、特性和值添加到文件中，以描述命令项布局。 有关详细的 XML 架构，请参阅 [.VSCT xml 架构参考](../../extensibility/vsct-xml-schema-reference.md)。

## <a name="differences-between-ctc-and-vsct-files"></a>.Ctc 和 .vsct 文件之间的差异
 尽管 *.vsct* 文件中 XML 标记后面的含义与 *.ctc* 文件格式中的标记相同，但其实现有点不同：

- 新 **\<extern>** 标记是引用其他 *.h* 文件（如工具栏文件）的位置。 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]

- 尽管 *.vsct* 文件支持 **/include** 语句，但 *.ctc* 文件也是 **\<import>** 如此。 差别在于， **/include** 会引入 *所有* 信息，而 **\<import>** 只会引入名称。

- 尽管 *.ctc* 文件需要一个在其中定义预处理器指令的标头文件，但 *.vsct* 文件不需要一个头文件。 相反，请将指令放在位于 **\<Symbol>** *.vsct* 文件底部的元素中的符号表中。

- *.vsct* files 具有标记功能 **\<Annotation>** ，可用于嵌入所需的任何信息，例如便笺甚至图片。

- 值以属性的形式存储在项上。

- 可单独存储或堆叠命令标志。  但是，IntelliSense 不能用于堆栈命令标志。 有关命令标志的详细信息，请参阅 [CommandFlag 元素](../../extensibility/command-flag-element.md)。

- 可以指定多个类型，如 split dropdown、combos 等。

- 不验证 Guid。

- 每个 UI 元素都有一个字符串，该字符串表示与之一起显示的文本。

- 父节点是可选的。 如果省略，则使用值 *组 Unknown* 。

- *Icon* 参数是可选的。

- Bitmap 节：此部分与 *.ctc* 文件中的相同，不同之处在于，你现在可以通过 Href 指定一个文件名，该文件名将在编译时由 *vsct.exe* 编译器提取。

- Resid 标识：可以使用旧的位图资源 ID，但其工作方式与在 *.ctc* 文件中的工作方式相同。

- HRef：允许您为位图资源指定文件名的新方法。 它假定所有内容都已使用，因此可以省略已使用部分。 编译器首先会搜索该文件的本地资源，然后在任何网络共享上搜索该 **/i** 开关定义的任何资源。

- 键绑定：不再需要指定模拟器。 如果指定了一个，编译器将假定编辑器和模拟器相同。

- Keychord： Keychord 已删除。 新格式为 *Key1、Mod1、Key2、Mod2*。  可以指定字符、十六进制或 VK 常量。

新编译器 *vsct.exe* 会编译 *.ctc* 和 *.vsct* 文件。 但是，旧的 *ctc.exe* 编译器将无法识别或 *.vsct* 文件。

可以使用 *vsct.exe* 编译器将现有 *的 cto* 文件转换为 *.vsct* 文件。 有关详细信息，请参阅 [如何：从现有的 cto 文件创建 .vsct 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file)。

## <a name="the-vsct-file-elements"></a>.Vsct 文件元素
 命令表具有以下层次结构和元素：

- [CommandTable 元素](../../extensibility/commandtable-element.md)：表示与 VSPackage 关联的所有命令、菜单组和菜单。

- [Extern 元素](../../extensibility/extern-element.md)：引用要与 *.vsct* 文件合并的所有外部 .h 文件。

- [Include 元素](../../extensibility/include-element.md)：引用要编译的任何附加标头 () 文件以及 *.vsct* 文件。 *.Vsct* 文件可以包含 *.h* 文件，其中包含的常量用于定义 IDE 或其他 VSPackage 提供的命令、菜单组和菜单。

- [命令元素](../../extensibility/commands-element.md)：表示所有可执行的单个命令。 每个命令都具有以下四个子元素：

- [菜单元素](../../extensibility/menus-element.md)：表示 VSPackage 中的所有菜单和工具栏。 菜单是用于命令组的容器。

- [Groups 元素](../../extensibility/groups-element.md)：表示 VSPackage 中的所有组。 组是各个命令的集合。

- [钮扣元素](../../extensibility/buttons-element.md)：表示 VSPackage 中的所有命令按钮和菜单项。 按钮是可与命令相关联的视觉对象。

- [位图元素](../../extensibility/bitmaps-element.md)：表示 VSPackage 中所有按钮的所有位图。 位图是在命令按钮旁显示的图片，具体取决于上下文。

- [CommandPlacements 元素](../../extensibility/commandplacements-element.md)：指示各个命令应放置在 VSPackage 的菜单中的其他位置。

- [VisibilityConstraints 元素](../../extensibility/visibilityconstraints-element.md)：指定是在任何时候还是仅在某些上下文（如显示特定的对话框或窗口）中显示命令。 只有指定的上下文处于活动状态时，才会显示具有此元素的值的菜单和命令。 默认行为是始终显示该命令。

- [键绑定元素](../../extensibility/keybindings-element.md)：指定命令的任何键绑定。 这是一个或多个必须按下以执行命令的组合键，如 **Ctrl** + **S**。

- [UsedCommands 元素](../../extensibility/usedcommands-element.md)：通知 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 环境：尽管指定的命令由其他代码实现，但当当前 VSPackage 处于活动状态时，它会提供命令实现。

- Symbol[元素](../../extensibility/symbols-element.md)：包含包中所有命令的符号名称和 GUID id。

## <a name="vsct-file-design-guidelines"></a>.vsct 文件设计准则
 若要成功设计 *.vsct* 文件，请遵循以下准则。

- 命令只能放在组中，组只能放置在菜单中，而菜单只能放在组中。 IDE 中只显示菜单，而不是组和命令。

- 子菜单不能直接分配给菜单，但必须分配给某个组，而该组又被分配给某个菜单。

- 可以使用其定义指令的父字段将命令、子菜单和组分配给一个父组或菜单。

- 仅通过指令中的父字段组织命令表有一个很大的限制。 定义对象的指令只能采用一个父参数。

- 重复使用命令、组或子菜单要求使用新指令来创建对象的新实例，该实例具有其自己的 `GUID:ID` 对。

- 每个 `GUID:ID` 对必须是唯一的。 例如，重复使用已放置在菜单、工具栏或上下文菜单上的命令由 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口处理。

- 命令和子菜单还可以分配给多个组，可以使用 [命令元素](../../extensibility/commands-element.md)将组分配给多个菜单。

## <a name="vsct-file-notes"></a>.vsct 文件说明
 如果在对 *.vsct* 文件进行编译并将其放入本机附属 DLL 之后对该文件进行任何更改，则应运行 **devenv.exe/setup/nosetupvstemplates**。 这样做会强制重新读取实验注册表中指定的 VSPackage 资源，并强制重新读取要重新生成的内部数据库 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

 在开发过程中，可能会在实验注册表配置单元中创建和注册多个 VSPackage 项目，从而导致在 IDE 中出现混乱。 若要解决此问题，可以将实验性 hive 重置为默认设置，以删除所有已注册的 Vspackage 和他们可能对 IDE 所做的任何更改。 若要重置实验性 hive，请使用 Visual Studio SDK 附带的 CreateExpInstance.exe 工具。 可在以下位置找到：

 *% PROGRAMFILES (x86) % \ Visual Studio \\ \<version> SDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe*

 使用命令 **CreateExpInstance/Reset** 运行该工具。 请记住，此工具从实验性 hive 中删除通常不随一起安装的所有已注册的 Vspackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)
