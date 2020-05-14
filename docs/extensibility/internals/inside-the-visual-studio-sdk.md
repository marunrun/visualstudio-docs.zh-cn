---
title: 在可视化工作室 SDK 中 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- roadmap, Visual Studio integration SDK
- Visual Studio integration SDK roadmap
- integration roadmap, Visual Studio SDK
ms.assetid: 9118eaa4-0453-4dc5-9e16-c7062d254869
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0e72020795bc3181e11f0f90eff580a2365d4000
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707574"
---
# <a name="inside-the-visual-studio-sdk"></a>深入探究 Visual Studio SDK

本节提供有关 Visual Studio 扩展的深入信息，包括 Visual Studio 体系结构、组件、服务、架构、实用程序等。

## <a name="extensibility-architecture"></a>可扩展性架构
 下图显示了可视化工作室扩展性体系结构。 VS包提供应用程序功能，这些功能在 IDE 之间作为服务共享。 标准 IDE 还提供广泛的服务，例如<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>，这些服务提供对 IDE 窗口功能的访问。

 ![环境体系结构图形](../../extensibility/internals/media/environment.gif "环境")可视化工作室架构的广义视图

## <a name="vspackages"></a>VSPackages
 VSPackage 是软件模块，它们通过 UI 元素、服务、项目、编辑器和设计器来组成并扩展 Visual Studio。 VS包是视觉工作室的中心建筑单元。 有关更多信息，请参见 [VSPackages](../../extensibility/internals/vspackages.md)。

## <a name="visual-studio-shell"></a>Visual Studio Shell
 Visual Studio 外壳提供基本功能，并支持其组件 VSPackages 和 MEF 扩展之间的交叉通信。 有关详细信息，请参阅[可视化工作室外壳](../../extensibility/internals/visual-studio-shell.md)。

## <a name="user-experience-guidelines"></a>用户体验指南
 如果您计划为 Visual Studio 设计新功能，您应该查看这些设计和可用性提示指南：[可视化工作室用户体验指南](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)。

## <a name="commands"></a>命令
 命令是完成任务（如打印文档、刷新视图或创建新文件）的函数。

 扩展可视化工作室时，您可以创建命令并将其注册到可视化工作室外壳。 您可以指定这些命令在 IDE 中的显示方式，例如，在菜单或工具栏上。 通常，"**工具**"菜单上会出现自定义命令，用于显示工具窗口的命令将显示在 **"视图"** 菜单**的其他 Windows**子菜单上。

 创建命令时，还必须为其创建事件处理程序。 事件处理程序确定命令何时可见或启用，允许您修改其文本，并保证命令在激活时做出适当的响应。 在大多数情况下，IDE 使用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口处理命令。 Visual Studio 中的命令从最里面的命令上下文开始处理，基于本地选择，并根据全局选择进入最外层上下文。 添加到主菜单的命令可立即用于脚本编写。

 有关详细信息，请参阅[命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)。

## <a name="menus-and-toolbars"></a>菜单和工具栏
 菜单和工具栏为用户提供调用命令的方法。 菜单是命令的行或列，通常显示为工具窗口顶部的单个文本项。 子菜单是辅助菜单，当用户单击包含小箭头的命令时显示。 当用户右键单击某些 UI 元素时，将显示上下文菜单。 一些常见的菜单名称是**文件**、**编辑**、**查看**和**窗口**。 有关详细信息，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。

 工具栏是按钮和其他控件的行或列，如组合框、列表框和文本框。 工具栏按钮通常具有图标图像，例如 **"打开文件"** 命令的文件夹图标或 **"打印"** 命令的打印机。 所有工具栏元素都与命令相关联。 单击工具栏按钮时，将运行其关联的命令。 对于下拉控件，下拉列表中的每个项都与不同的命令相关联。 某些工具栏控件（如拆分器控件）是混合控件。 控件的一侧是工具栏按钮，另一边是向下箭头，单击时显示多个命令。

## <a name="tool-windows"></a>工具窗口
 在 IDE 中使用工具窗口来显示信息。 **工具箱**、**解决方案资源管理器**、**属性**窗口和**Web 浏览器**是工具窗口的示例。

 工具窗口通常提供各种控件，用户可以与之交互。 例如，"**属性"** 窗口允许用户设置用于特定用途的对象的属性。 **属性**窗口在此意义上是专门化的，但也具有常规性，因为它可用于许多不同的情况。 同样，**输出**窗口是专门化的，因为它提供基于文本的输出，但一般，因为 Visual Studio 中的许多子系统可以使用它向 Visual Studio 用户提供输出。

 请考虑以下 Visual Studio 图片，其中包含多个工具窗口：

 ![屏幕截图](../../extensibility/internals/media/t1gui.png "T1gui")

 某些工具窗口停靠在一个窗格中，该窗格显示解决方案资源管理器工具窗口并隐藏其他工具窗口，但通过单击选项卡使其可用。 图片显示另外两个工具窗口，**错误列表**和**输出**窗口，停靠在单个窗格上。

 还显示的是主文档窗格，它显示了多个编辑器窗口。 尽管工具窗口通常只有一个实例（例如，您只能打开一个**解决方案资源管理器**），但编辑器窗口可以有多个实例，每个实例都用于编辑单独的文档，但所有这些实例都停靠在同一窗格中。 图片显示的文档窗格，该窗格具有两个编辑器窗口，一个窗体设计器窗口。 通过单击选项卡，文档窗格中的所有窗口都可用，但包含EditorPane.cs文件的编辑器窗口可见且处于活动状态。

 扩展 Visual Studio 时，您可以创建工具窗口，让 Visual Studio 用户与您的扩展进行交互。 您还可以创建自己的编辑器，让 Visual Studio 用户编辑文档。 由于工具窗口和编辑器将集成到 Visual Studio 中，因此您不必对其进行编程才能正确停靠或显示在选项卡上。 当它们在 Visual Studio 中正确注册时，它们将自动具有 Visual Studio 中工具窗口和文档窗口的典型功能。 有关详细信息，请参阅[扩展和自定义工具窗口](../../extensibility/extending-and-customizing-tool-windows.md)。

## <a name="document-windows"></a>文档窗口
 文档窗口是多文档接口 （MDI） 窗口的带框子窗口。 文档窗口通常用于承载文本编辑器、表单编辑器（也称为设计器）或编辑控件，但它们还可以承载其他功能类型。 "**新建文件**"对话框包括 Visual Studio 提供的文档窗口示例。

 大多数编辑器特定于编程语言或文件类型，如 HTML 页、框架集、C++文件或头文件。 通过在 **"新建文件"** 对话框中选择模板，用户会动态地为与模板关联的文件类型的编辑器创建文档窗口。 当用户打开现有文件时，也会创建文档窗口。

 文档窗口仅限于 MDI 工作区。 每个文档窗口的顶部都有一个选项卡，选项卡顺序链接到 MDI 区域中可能打开的其他窗口。 右键单击文档窗口的选项卡将显示一个快捷方式菜单，其中包含将 MDI 区域拆分为多个水平或垂直选项卡组的选项。 拆分 MDI 区域可同时查看多个文件。 有关详细信息，请参阅[文档窗口](../../extensibility/internals/document-windows.md)。

## <a name="editors"></a>编辑器
 Visual Studio 编辑器允许您自定义它，并通过托管扩展性框架 （MEF） 将其用于您自己的类型的内容。 在许多情况下，您不需要创建 VSPackage 来扩展编辑器，尽管如果要包括 shell 中的要素（例如，菜单命令或快捷键），则可以将 MEF 扩展与 VSPackage 合并。

 您还可以创建自定义编辑器，例如，如果要读取和写入数据库，或者希望使用设计器。 您还可以使用外部编辑器（如记事本或微软 WordPad）。 有关详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

## <a name="language-services"></a>语言服务
 如果希望 Visual Studio 编辑器支持新的编程关键字，甚至支持新的编程语言，则可以创建语言服务。 每个语言服务可以完全、部分或根本不实现某些编辑器功能。 根据配置方式，语言服务可以在编辑器中提供语法突出显示、大括号匹配、IntelliSense 支持和其他功能。

 语言服务的核心是解析器和扫描仪。 扫描程序（或 lexer）将源文件划分为称为令牌的元素，解析器在这些令牌之间建立关系。 创建语言服务时，必须实现解析器和扫描仪，以便 Visual Studio 能够理解该语言的令牌和语法。 您可以创建托管或非托管语言服务。 有关详细信息，请参阅[旧语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)。

## <a name="projects"></a>项目

在 Visual Studio 中，项目是开发人员用于组织和构建源代码和其他资源的容器。 项目允许您组织、构建、调试和部署源代码、对 Web 服务和数据库的引用以及其他资源。 VSPackages 可以通过提供项目类型、项目子类型和自定义工具来扩展 Visual Studio 项目系统。

项目也可以聚集在一个解决方案中，该*解决方案*是由一个或多个项目组成的分组，它们协同工作以创建应用程序。 与解决方案相关的项目和状态信息存储在两个解决方案文件中，即基于文本[的解决方案 （.sln） 文件和](solution-dot-sln-file.md)二进制[解决方案用户选项 （.suo） 文件](solution-user-options-dot-suo-file.md)。 这些文件类似于早期版本的 Visual Basic 中使用的组 （.vbg） 文件，以及用于早期版本的 C++的工作区 （.dsw） 和用户选项 （.opt） 文件。

有关详细信息，请参阅[项目和](../../extensibility/internals/projects.md)[解决方案](../../extensibility/internals/solutions-overview.md)。

## <a name="project-and-item-templates"></a>项目和项模板
 可视化工作室包括预定义的项目模板和项目项目模板。 您还可以制作自己的模板或从社区获取模板，然后将它们集成到 Visual Studio 中。 [MSDN 代码库](https://code.msdn.microsoft.com/site/search?query=visual%20studio)是获取模板和扩展的地方。

 模板包含生成特定类型的应用程序、控件、库或类所需的项目结构和基本文件。 当您要开发类似于其中一个模板的软件时，请创建基于模板的项目，然后修改该项目中的文件。

> [!NOTE]
> [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]项目不支持此模板体系结构。

 有关详细信息，请参阅[添加项目和项目项目模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。

## <a name="properties-and-options"></a>属性和选项
 属性**窗口**显示单个或多个选定项的属性：[扩展属性](../../extensibility/internals/extending-properties.md)选项页包含与特定组件相关的选项集，如编程语言或 VSPackage：[选项和选项页](../../extensibility/internals/options-and-options-pages.md)。 设置通常是可以导入和导出的与 UI 相关的功能：[支持用户设置](../../extensibility/internals/support-for-user-settings.md)。

## <a name="visual-studio-services"></a>视觉工作室服务
 服务为组件提供一组特定的接口。 Visual Studio 提供一组服务，这些服务可用于任何组件（包括扩展）。 例如，Visual Studio 服务允许动态显示或隐藏工具窗口，启用对帮助、状态栏或 UI 事件的访问。 Visual Studio 编辑器还提供可由编辑器扩展导入的服务。 有关详细信息，请参阅[使用和提供服务](../../extensibility/using-and-providing-services.md)。

## <a name="debugger"></a>调试程序
 调试器是特定于语言的调试组件的用户界面。 如果已创建新的语言服务，则需要创建特定的调试引擎以挂接到调试器。 有关详细信息，请参阅[可视化工作室调试器扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)。

## <a name="source-control"></a>源代码管理
 有关实现源代码管理插件或 VSPackage 的信息，请参阅[源代码管理](../../extensibility/internals/source-control.md)。

## <a name="wizards"></a>向导
 您可以结合新的项目类型创建向导，以便向导可帮助用户在创建该类型的新项目时做出正确的决策。 有关详细信息，请参阅[向导](../../extensibility/internals/wizards.md)。

## <a name="custom-tools"></a>自定义工具
 自定义工具允许您将工具与项目中的项目相关联，并在保存文件时运行该工具。 有关详细信息，请参阅[自定义工具](../../extensibility/internals/custom-tools.md)。

## <a name="vssdk-utilities"></a>VSSDK 实用工具
 VSSDK 包括一组实用程序，您可能需要这些实用程序才能处理 VSPackages 的不同方面。 有关详细信息，请参阅[VSSDK 实用程序](../../extensibility/internals/vssdk-utilities.md)。

## <a name="using-windows-installer"></a>使用 Windows 安装程序
 在某些情况下，您可能需要使用 Windows 安装程序而不是 VSIX 安装程序：例如，您可能需要写入注册表。 有关将 Windows 安装程序与扩展一起使用的信息，请参阅[使用 Windows 安装程序安装 VS 程序](../../extensibility/internals/installing-vspackages-with-windows-installer.md)。

## <a name="help-viewer"></a>帮助查看器
 您可以将自己的帮助和 F1 页面集成到帮助查看器中。 有关详细信息，请参阅[Microsoft 帮助查看器 SDK](../../extensibility/internals/microsoft-help-viewer-sdk.md)。
