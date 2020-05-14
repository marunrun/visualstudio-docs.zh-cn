---
title: 设计 XML 命令表 （.Vsct） 文件 |微软文档
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
ms.openlocfilehash: fcd29aee98139bb151c87590b256df6b8370abff
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708741"
---
# <a name="design-xml-command-table-vsct-files"></a>设计 XML 命令表 （.vsct） 文件
XML 命令表 *（.vsct*） 文件描述 VSPackage 的命令项的布局和外观。 命令项包括按钮、组合框、菜单、工具栏和命令项组。 本文介绍了 XML 命令表文件、它们如何影响命令项和菜单以及如何创建它们。

## <a name="commands-menus-groups-and-the-vsct-file"></a>命令、菜单、组和 .vsct 文件
 *.vsct*文件围绕命令、菜单和命令组进行组织。 *.vsct*文件中的 XML 标记表示每个项，以及其他关联的项，如命令按钮、命令放置和位图。

 通过运行[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]包模板创建新的 VSPackage 时，模板会生成一个 *.vsct*文件，该文件包含菜单命令、工具窗口或自定义编辑器的必要元素，具体取决于您的选择。 然后可以修改此 *.vsct*文件以满足特定 VSPackage 的要求。 有关如何修改 *.vsct*文件的示例，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

 要创建新的空白 *.vsct*文件，请参阅[如何：创建 *.vsct*文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)。 创建后，向文件添加 XML 元素、属性和值以描述命令项布局。 有关详细的 XML 架构，请参阅[VSCT XML 架构引用](../../extensibility/vsct-xml-schema-reference.md)。

## <a name="differences-between-ctc-and-vsct-files"></a>.ctc 和 .vsct 文件之间的差异
 虽然 *.vsct*文件中的 XML 标记背后的含义与现在弃用*的 .ctc*文件格式中的这些标记相同，但它们的实现却略有不同：

- 新的**\<extern>** 标记是引用要编译的其他 *.h*文件的位置，例如工具栏的文件[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]。

- 虽然 *.vsct*文件支持 **/include**语句，就像 *.ctc*文件一样，但它也具有新的**\<导入>** 元素。 区别在于 **/包括**带来了*所有*信息，而**\<导入>** 只带来名称。

- 虽然 *.ctc*文件需要一个头文件，您可以在其中定义预处理器指令，*但 .vsct*文件不需要一个。 相反，将指令放在符号表中，该表位于位于 *.vsct*文件底部的**\<符号>** 元素中。

- *.vsct*文件具有**\<注释>** 标记，允许您嵌入任何你喜欢的信息，如笔记，甚至图片。

- 值存储为项上的属性。

- 命令标志可以单独存储或堆叠。  但是，IntelliSense 不适用于堆叠的命令标志。 有关命令标志的详细信息，请参阅[命令Flag元素](../../extensibility/command-flag-element.md)。

- 您可以指定多种类型，如拆分下拉、组合等。

- GUID 不验证。

- 每个 UI 元素都有一个字符串，表示与它一起显示的文本。

- 父级是可选的。 如果省略，则使用值*组"未知*"。

- *图标*参数是可选的。

- Bitmap 部分：此部分与 *.ctc*文件中相同，只不过您现在可以通过 href指定文件名，该文件名将在编译时由*vsct.exe*编译器拉取。

- ResID：可以使用旧的位图资源 ID，并且仍然与 *.ctc*文件中的工作方式相同。

- HRef：一种新方法，允许您为位图资源指定文件名。 它假定所有都已使用，因此您可以省略"已使用"部分。 编译器将首先搜索文件的本地资源，然后在任何网络共享上搜索 **/I**开关定义的任何资源。

- 密钥绑定：您不再需要指定仿真器。 如果指定了一个，编译器将假定编辑器和仿真器相同。

- 基乔德：基乔德已经掉了下来。 新格式为*Key1、Mod1、Key2、Mod2*。  您可以指定字符、十六进制或 VK 常量。

新的编译器 *，vsct.exe，* 编译 *.ctc*和 *.vsct*文件。 但是，旧的*ctc.exe*编译器不会识别或编译 *.vsct*文件。

您可以使用*vsct.exe*编译器将现有的 *.cto*文件转换为 *.vsct*文件。 有关详细信息，请参阅[如何：从现有的 .cto 文件创建 .vsct 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md#how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file)。

## <a name="the-vsct-file-elements"></a>.vsct 文件元素
 命令表具有以下层次结构和元素：

- [命令表元素](../../extensibility/commandtable-element.md)：表示与 VSPackage 关联的所有命令、菜单组和菜单。

- [Extern 元素](../../extensibility/extern-element.md)：引用要与 *.vsct*文件合并的任何外部 .h 文件。

- [包括元素](../../extensibility/include-element.md)：引用要与 *.vsct*文件一起编译的任何其他标头 （.h） 文件。 *.vsct*文件可以包含包含定义 IDE 或其他 VSPackage 提供的命令、菜单组和菜单的常量的 *.h*文件。

- [命令元素](../../extensibility/commands-element.md)：表示可以执行的所有单个命令。 每个命令具有以下四个子元素：

- [菜单元素](../../extensibility/menus-element.md)：表示 VSPackage 中的所有菜单和工具栏。 菜单是命令组的容器。

- [组元素](../../extensibility/groups-element.md)：表示 VS 包中的所有组。 组是单个命令的集合。

- [按钮元素](../../extensibility/buttons-element.md)：表示 VSPackage 中的所有命令按钮和菜单项。 按钮是可与命令关联的可视控件。

- [位图元素](../../extensibility/bitmaps-element.md)：表示 VSPackage 中所有按钮的所有位图。 位贴图是显示在命令按钮旁边或上阵的图片，具体取决于上下文。

- [命令放置元素](../../extensibility/commandplacements-element.md)：指示应在 VSPackage 菜单中放置各个命令的其他位置。

- [可见性约束元素](../../extensibility/visibilityconstraints-element.md)：指定命令是否在所有时间显示，或仅在某些上下文中（例如显示特定对话框或窗口时）显示。 只有指定上下文处于活动状态时，才显示具有此元素值的菜单和命令。 默认行为是随时显示该命令。

- [键绑定元素](../../extensibility/keybindings-element.md)：指定命令的任何键绑定。 也就是说，必须按下一个或多个键组合才能执行命令，如**Ctrl**+**S**。

- [已用命令元素](../../extensibility/usedcommands-element.md)：通知[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]环境，尽管指定的命令由其他代码实现，但当当前 VSPackage 处于活动状态时，它提供命令实现。

- [符号元素](../../extensibility/symbols-element.md)：包含包中所有命令的符号名称和 GUID ID。

## <a name="vsct-file-design-guidelines"></a>.vsct 文件设计指南
 要成功设计 *.vsct*文件，请遵循以下准则。

- 命令只能放在组中，组只能放置在菜单中，菜单只能放在组中。 实际上只有菜单显示在 IDE 中，组和命令不显示。

- 子菜单不能直接分配给菜单，但必须分配给组，而组又分配给菜单。

- 可以使用命令、子菜单和组的定义指令的父字段将命令、子菜单和组分配给一个育儿组或菜单。

- 仅通过指令中的父字段组织命令表存在很大限制。 定义对象的指令只能采用一个父参数。

- 重用命令、组或子菜单需要使用新指令创建具有其自身`GUID:ID`对的对象的新实例。

- 每`GUID:ID`对必须是唯一的。 重复使用一个命令，例如，已放置在菜单，工具栏，或上下文菜单，由<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口处理。

- 命令和子菜单也可以分配给多个组，并且可以使用[命令元素](../../extensibility/commands-element.md)将组分配给多个菜单。

## <a name="vsct-file-notes"></a>.vsct 文件注释
 如果在编译 *.vsct*文件并将其放在本机卫星 DLL 中后对其进行任何更改，则应运行**devenv.exe /setup /nosetupvstemplates**。 这样做将强制重新读取实验注册表中指定的 VSPackage 资源以及描述[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]要重建的内部数据库。

 在开发过程中，可以在实验注册表配置单元中创建和注册多个 VSPackage 项目，这可能导致 IDE 中的混乱混乱。 要解决此问题，您可以将实验配置单元重置为默认设置，以删除所有已注册的 VS 包以及它们可能对 IDE 所做的任何更改。 要重置实验配置单元，请使用 Visual Studio SDK 附带的 CreateExpInstance.exe 工具。 您可以在：

 *%PROGRAMFILES（x86）%\视觉工作室\\\<版本> SDK_VisualStudio 集成\工具\Bin_createExpInstance.exe*

 使用命令**CreateExp实例 /重置**运行该工具。 请记住，此工具从实验配置单元中删除通常不安装[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的所有已注册的 VS 包。

## <a name="see-also"></a>请参阅
- [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)
