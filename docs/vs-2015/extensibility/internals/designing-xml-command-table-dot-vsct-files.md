---
title: 设计 XML 命令表 (。Vsct) 文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, designing
ms.assetid: bb87a322-bac4-4258-92bc-9a876f05d653
caps.latest.revision: 28
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 987536af051de4a66b3eccadb105fd98455ddf06
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196851"
---
# <a name="designing-xml-command-table-vsct-files"></a>设计 XML 命令表 (。Vsct) 文件
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

XML 命令表格 (.vsct) 文件描述的布局和外观的命令项对为 VSPackage。 命令项包括按钮、 组合框、 菜单、 工具栏和命令项的组。 本主题介绍 XML 命令表文件、 它们如何影响命令项和菜单，以及如何创建它们。  
  
## <a name="commands-menus-groups-and-the-vsct-file"></a>命令、 菜单、 组和.vsct 文件  
 .vsct 文件组织周围命令、 菜单和命令组中。 .Vsct 文件中的 XML 标记表示每个这些项，以及其他相关联的项，如命令按钮、 命令放置和位图。  
  
 通过运行时创建新的 VSPackage[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]包模板，模板生成所需的元素具有菜单命令、 工具窗口中，或自定义编辑器中的，具体取决于你选择的.vsct 文件。 然后可以修改此.vsct 文件以满足特定的 VSPackage 的要求。 有关如何修改.vsct 文件的示例，请参阅中的示例[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。  
  
 若要创建新的、 空白.vsct 文件，请参阅[如何：创建。Vsct 文件](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)。 创建后，您将添加 XML 元素、 属性和值到描述命令项布局的文件。 有关详细的 XML 架构，请参阅[VSCT XML Schema Reference](../../extensibility/vsct-xml-schema-reference.md)。  
  
## <a name="differences-between-ctc-and-vsct-files"></a>.Ctc 和.vsct 文件之间的差异  
 虽然.vsct 文件中的 XML 标记背后的含义是相同的为中现已弃用.ctc 文件格式，其实现是稍有不同。  
  
- 新 **\<extern >** 标记是，引用其他.h 文件进行编译，例如针对[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]工具栏。  
  
- 而.vsct 文件的支持 **/include**语句，.ctc 文件执行操作，它还具有一个新\<**导入 >** 元素。 其差异是， **/include**引入了**所有**的信息，但\<**导入 >** 将仅在名称中。  
  
- 虽然.ctc 文件需要在其中定义预处理器指令的标头文件，其中一个不需要的.vsct 文件。 相反，将在指令放置在符号表中，位于 **\<符号 >** 元素，位于.vsct 文件的底部。  
  
- .vsct 文件功能 **\<批注 >** 标记，它使您可以嵌入您喜欢，如说明或甚至图片的任何信息。  
  
- 值存储为项的特性。  
  
- 可以单独存储或堆积图命令标志。  Intellisense，但是，不适用于堆积的命令标志。 有关命令标志的详细信息，请参阅[Command Flag 元素](../../extensibility/command-flag-element.md)。  
  
- 可以指定多个类型，例如拆分下拉列表、 combos，等等。  
  
- Guid 不验证。  
  
- 每个 UI 元素有一个字符串，表示与它一起显示的文本。  
  
- 父是可选的。 如果省略，使用"组未知"的值。  
  
- 图标参数是可选的。  
  
- 将文件位图部分-.ctc 相同，只不过现在可以指定文件名称，通过将由 vsct.exe 编译器抽取在编译时的 href。  
  
- ResID-旧的位图资源 ID 可以用于，如下所示.ctc 文件仍在工作方式相同。  
  
- HRef-一个新的方法，允许您指定的位图资源文件的名称。 它假定，将使用所有，因此可以省略使用的部分。 首先，编译器将搜索该文件，然后在任何网络共享上的本地资源和 /I 开关所定义的所有资源。  
  
- 键绑定-不再需要指定一个仿真程序。 如果指定一个，则编译器将假定在编辑器和仿真程序是相同的。  
  
- Keychord-已删除。 新的格式为 Key1、 Mod1、 Key2、 Mod2。  您可以指定字符、 十六进制、 或 VK 常量。  
  
  新的编译器、 vsct.exe，编译.ctc 和.vsct 文件。 旧 ctc.exe 编译器，但是，将不识别也不编译.vsct 文件。  
  
  Vsct.exe 编译器可用于将现有.cto 文件转换成一个.vsct 文件。 有关详细信息，请参阅[如何：创建。从现有的 Vsct 文件。首席技术官文件](../../misc/how-to-create-a-dot-vsct-file-from-an-existing-dot-cto-file.md)。  
  
## <a name="the-vsct-file-elements"></a>.Vsct 文件元素  
 命令表具有以下层次结构和元素：  
  
 [CommandTable 元素](../../extensibility/commandtable-element.md)— 表示的所有命令、 菜单组和 VSPackage 与关联的菜单。  
  
 [Extern 元素](../../extensibility/extern-element.md)— 引用你想要使用.vsct 文件合并任何外部.h 文件。  
  
 [包含元素](../../extensibility/include-element.md)— 引用你想要编译 your.vsct 文件以及任何其他标头 (.h) 文件。 .Vsct 文件可以包括包含常数，用于定义在 IDE 或另一个 VSPackage 提供的命令、 菜单组和菜单的.h 文件。  
  
 [命令元素](../../extensibility/commands-element.md)— 表示所有可执行的单个命令。 每个命令具有以下四个子元素：  
  
 [Menus 元素](../../extensibility/menus-element.md)— 表示所有菜单和工具栏在 VSPackage 中的。 菜单是组的命令的容器。  
  
 [Groups 元素](../../extensibility/groups-element.md)— 表示所有在 VSPackage 中的组。 组是单个命令的集合。  
  
 [按钮元素](../../extensibility/buttons-element.md)— 表示的所有命令按钮和菜单项在 VSPackage 中的。 按钮是可以与命令相关联的可视控件。  
  
 [Bitmaps 元素](../../extensibility/bitmaps-element.md)— 表示所有按钮在 VSPackage 中的所有位图。 位图为显示下一步或上的命令按钮，具体取决于上下文的图片。  
  
 [CommandPlacements 元素](../../extensibility/commandplacements-element.md)— 指示单个命令，应被放置在你的 VSPackage 的菜单中的其他位置。  
  
 [VisibilityConstraints 元素](../../extensibility/visibilityconstraints-element.md)-指定是否命令将显示在所有时间，或仅在某些上下文中，例如何时显示特定对话框或窗口中。 仅当指定的上下文处于活动状态时，将显示菜单和命令，并提供此元素的值。 默认行为是可在任何时候显示命令。  
  
 [KeyBindings 元素](../../extensibility/keybindings-element.md)— 指定命令的任何键绑定。 也就是说，一个或多个键组合必须按下执行命令，如**CTRL + S**。  
  
 [UsedCommands 元素](../../extensibility/usedcommands-element.md)— 通知[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]环境当前 VSPackage 处于活动状态时，将由其他代码，实现指定的命令，尽管它提供了命令实现。  
  
 `Symbols Element` -包含的符号名称和所有包中命令的 GUID Id。  
  
## <a name="vsct-file-design-guidelines"></a>.Vsct 文件设计指南  
 若要成功设计一个.vsct 文件，请遵循以下准则。  
  
- 可以仅为组中置于命令、 组可放置仅在菜单和菜单可以放置仅在组中。 仅菜单实际显示在 IDE 中，组和命令不。  
  
- 子菜单不能直接分配给一个菜单，但必须将分配给一个组，该组又分配给一个菜单。  
  
- 命令、 子菜单和组可以分配给一个父级组或使用其定义的指令的父字段的菜单。  
  
- 组织仅通过的指令中的父字段的命令表有一个明显的限制。 定义对象的指令可能只有一个父参数。  
  
- 重复使用的命令、 组或子菜单需要新的指令以创建对象的新实例有其自身使用`GUID:ID`对。  
  
- 每个`GUID:ID`对都必须唯一。 重复使用，例如，已放在菜单上，工具栏上，或上下文菜单上的命令由处理<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口。  
  
- 命令和子菜单还可以分配给多个组和组可以分配给使用多个菜单[Commands 元素](../../extensibility/commands-element.md)。  
  
## <a name="vsct-file-notes"></a>.Vsct 文件说明  
 如果您同时对其进行编译，并将其放在本机附属 DLL 后，可以对.vsct 文件进行任何更改，则应运行**devenv.exe /setup /nosetupvstemplates**。 执行此操作将强制在实验性注册表以重新读取和描述的内部数据库中所指定的 VSPackage 资源[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]重新生成。  
  
 在开发期间，就可以对多个 VSPackage 项目来创建并注册可能会导致令人困惑的混乱，在 IDE 中的实验性注册表配置单元。 若要解决此问题，可以重新设置为默认设置以删除所有已注册的 Vspackage 和可能会对 IDE 进行的任何更改实验性配置单元。 若要重置实验性配置单元，请使用 Visual Studio SDK 随附的 CreateExpInstance.exe 工具。 你可以找到它在  
  
 **%PROGRAMFILES(x86)%\Visual Studio \<version> SDK\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe**  
  
 使用命令行运行该工具**CreateExpInstance /Reset**。 请记住，此工具从中删除实验性配置单元通常不随一起安装的所有已注册的 Vspackage [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。  
  
## <a name="see-also"></a>请参阅  
 [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)
