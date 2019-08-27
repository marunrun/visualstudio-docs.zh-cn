---
title: 设计 XML 命令表 (。Vsct) 文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, designing
ms.assetid: bb87a322-bac4-4258-92bc-9a876f05d653
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bc088ac5c534e77de2aae919019396ccf2c344e2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66312103"
---
# <a name="design-xml-command-table-vsct-files"></a>设计 XML 命令表格 (.vsct) 文件
XML 命令表 ( *.vsct*) 文件描述的布局和外观的命令项对为 VSPackage。 命令项包括按钮、 组合框、 菜单、 工具栏和命令项的组。 本文介绍 XML 命令表文件、 它们如何影响命令项和菜单，以及如何创建它们。

## <a name="commands-menus-groups-and-the-vsct-file"></a>命令、 菜单、 组和.vsct 文件
 *.Vsct*围绕命令、 菜单和命令组组织文件。 中的 XML 标记 *.vsct*文件的表示每个项，以及其他相关联的项，如命令按钮、 命令放置和位图。

 通过运行时创建新的 VSPackage[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]包模板，该模板会生成 *.vsct*所需的元素的菜单命令、 工具窗口中或自定义编辑器中的，具体取决于你选择的文件。 这 *.vsct*文件然后进行修改以满足特定的 VSPackage 的要求。 有关如何修改的示例 *.vsct*文件，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

 若要创建新的空白 *.vsct*文件，请参阅[如何：创建 *.vsct*文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)。 创建后，您将添加 XML 元素、 属性和值到描述命令项布局的文件。 有关详细的 XML 架构，请参阅[VSCT XML 架构参考](../../extensibility/vsct-xml-schema-reference.md)。

## <a name="differences-between-ctc-and-vsct-files"></a>.Ctc 和.vsct 文件之间的差异
 虽然标记中的 XML 背后的含义 *.vsct*文件将与这些标记中现已弃用相同 *.ctc*文件格式，其实现是稍有不同：

- 新 **\<extern >** 标记是其中引用其他 *.h*文件以进行编译，这些文件以查找如[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]工具栏。

- 虽然 *.vsct*文件支持 **/include**语句，为 *.ctc*文件，它还具有一个新 **\<导入 >** 元素。 其差异是， **/include**引入了*所有*的信息，而 **\<导入 >** 将仅在名称中。

- 虽然 *.ctc*文件需要在其中定义预处理器指令的标头文件，不需要 *.vsct*文件。 相反，将在指令放置在符号表中，位于 **\<符号 >** 元素，位于底部 *.vsct*文件。

- *.vsct*文件功能 **\<批注 >** 标记，它使您可以嵌入您喜欢，如说明或甚至图片的任何信息。

- 值存储为项的特性。

- 可以单独存储或堆积图命令标志。  IntelliSense，但是，不适用于堆积的命令标志。 有关命令标志的详细信息，请参阅[CommandFlag 元素](../../extensibility/command-flag-element.md)。

- 可以指定多个类型，例如拆分下拉列表、 combos，等等。

- Guid 不验证。

- 每个 UI 元素有一个字符串，表示与它一起显示的文本。

- 父级是可选的。 如果省略，则这*未知组*使用。

- *图标*参数是可选的。

- 位图部分：本部分是中的相同 *.ctc*文件，只不过现在可以指定将由请求中的 Href 通过文件名*vsct.exe*编译器在编译时。

- ResID:旧位图的资源 ID 可以是使用和仍处于工作中的相同 *.ctc*文件。

- HRef:一个新方法，允许您指定的位图资源文件的名称。 它假定，将使用所有，因此可以省略使用的部分。 编译器将首先搜索文件，然后在任何网络共享上的本地资源，并且任何资源由 **/I**切换。

- 键绑定：不再需要指定一个仿真程序。 如果指定一个，则编译器将假定在编辑器和仿真程序是相同的。

- Keychord:已删除 Keychord。 新的格式是*Key1、 Mod1、 Key2、 Mod2*。  您可以指定字符、 十六进制、 或 VK 常量。

新的编译器*vsct.exe*，将同时编译 *.ctc*并 *.vsct*文件。 旧*ctc.exe*编译器，但是，将不识别或编译 *.vsct*文件。

可以使用*vsct.exe*编译器要转换的现有 *.cto*文件到 *.vsct*文件。 有关详细信息，请参阅[如何：从现有.cto 文件创建.vsct 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file)。

## <a name="the-vsct-file-elements"></a>.Vsct 文件元素
 命令表具有以下层次结构和元素：

- [CommandTable 元素](../../extensibility/commandtable-element.md):表示的所有命令、 菜单组和 VSPackage 与关联的菜单。

- [Extern 元素](../../extensibility/extern-element.md):引用你想要合并的任何外部.h 文件 *.vsct*文件。

- [包含元素](../../extensibility/include-element.md):引用要进行编译以及任何其他标头 (.h) 文件您 *.vsct*文件。 一个 *.vsct*文件可以包含 *.h*包含常数，用于定义命令、 菜单组和菜单在 IDE 或另一个 VSPackage 提供的文件。

- [Commands 元素](../../extensibility/commands-element.md):表示所有可执行的单个命令。 每个命令具有以下四个子元素：

- [Menus 元素](../../extensibility/menus-element.md):表示所有菜单和工具栏在 VSPackage 中。 菜单是组的命令的容器。

- [Groups 元素](../../extensibility/groups-element.md):表示所有在 VSPackage 中的组。 组是单个命令的集合。

- [Buttons 元素](../../extensibility/buttons-element.md):表示所有的命令按钮和菜单项在 VSPackage 中。 按钮是可以与命令相关联的可视控件。

- [Bitmaps 元素](../../extensibility/bitmaps-element.md):表示所有按钮在 VSPackage 中的所有位图。 位图为显示下一步或上的命令按钮，具体取决于上下文的图片。

- [CommandPlacements 元素](../../extensibility/commandplacements-element.md):指示其中的单个命令应放置在你的 VSPackage 的菜单中的其他位置。

- [VisibilityConstraints 元素](../../extensibility/visibilityconstraints-element.md):指定命令将显示在所有时间，或仅在某些上下文中，例如何时显示特定对话框或窗口中。 仅当指定的上下文处于活动状态时，将显示菜单和命令，并提供此元素的值。 默认行为是可在任何时候显示命令。

- [KeyBindings 元素](../../extensibility/keybindings-element.md):指定命令的任何键绑定。 也就是说，一个或多个键组合必须按下执行命令，如**Ctrl**+**S**。

- [UsedCommands 元素](../../extensibility/usedcommands-element.md):通知[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]环境当前 VSPackage 处于活动状态时，将由其他代码，实现指定的命令，尽管它提供了命令实现。

- [Symbols 元素](../../extensibility/symbols-element.md):包含的符号名称和 GUID 的所有包中命令的 Id。

## <a name="vsct-file-design-guidelines"></a>.vsct 文件设计指导原则
 已成功设计 *.vsct*文件中，请遵循以下准则。

- 可以仅为组中置于命令、 组可放置仅在菜单和菜单可以放置仅在组中。 仅菜单实际显示在 IDE 中，组和命令不。

- 子菜单不能直接分配给一个菜单，但必须将分配给一个组，该组又分配给一个菜单。

- 命令、 子菜单和组可以分配给一个父级组或使用其定义的指令的父字段的菜单。

- 组织仅通过的指令中的父字段的命令表有一个明显的限制。 定义对象的指令可能只有一个父参数。

- 重复使用的命令、 组或子菜单需要新的指令以创建对象的新实例有其自身使用`GUID:ID`对。

- 每个`GUID:ID`对都必须唯一。 重复使用，例如，已放在菜单上，工具栏上，或上下文菜单上的命令由处理<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口。

- 命令和子菜单还可以分配给多个组和组可以分配给使用多个菜单[Commands 元素](../../extensibility/commands-element.md)。

## <a name="vsct-file-notes"></a>.vsct 文件说明
 如果进行的任何更改 *.vsct*文件在同时对其进行编译，并将其放在本机附属 DLL 后，应运行**devenv.exe /setup /nosetupvstemplates**。 实验性注册表以重新读取和描述的内部数据库中指定的 VSPackage 资源执行操作，强制[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]重新生成。

 在开发期间，就可以对多个 VSPackage 项目来创建并注册可能会导致令人困惑的混乱，在 IDE 中的实验性注册表配置单元。 若要解决此问题，可以重新设置为默认设置以删除所有已注册的 Vspackage 和可能会对 IDE 进行的任何更改实验性配置单元。 若要重置实验性配置单元，请使用 Visual Studio SDK 随附的 CreateExpInstance.exe 工具。 您可以找到在：

 *%PROGRAMFILES(x86)%\Visual Studio\\\<version> SDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe*

 使用命令来运行该工具**CreateExpInstance /Reset**。 请记住，此工具从中删除实验性配置单元通常不随一起安装的所有已注册的 Vspackage [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)