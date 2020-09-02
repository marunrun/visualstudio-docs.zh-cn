---
title: 在 Visual Studio SDK 内 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- roadmap, Visual Studio integration SDK
- Visual Studio integration SDK roadmap
- integration roadmap, Visual Studio SDK
ms.assetid: 9118eaa4-0453-4dc5-9e16-c7062d254869
caps.latest.revision: 31
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3bdc65a145b64071087d72fce9967c67cc2f8426
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687536"
---
# <a name="inside-the-visual-studio-sdk"></a>深入探究 Visual Studio SDK
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本部分提供了有关 Visual Studio 扩展的详细信息，包括 Visual Studio 体系结构、组件、服务、架构、实用程序，等等。  
  
## <a name="extensibility-architecture"></a>扩展性体系结构  
 下图显示了 Visual Studio 扩展性体系结构。 Vspackage 提供应用程序功能，该功能在 IDE 中作为服务共享。 标准 IDE 还提供了各种服务，例如 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> ，提供对 IDE 窗口功能的访问。  
  
 ![环境体系结构图](../../extensibility/internals/media/environment.gif "environment")  
Visual Studio 体系结构的通用视图  
  
## <a name="vspackages"></a>VSPackages  
 VSPackage 是软件模块，它们通过 UI 元素、服务、项目、编辑器和设计器来组成并扩展 Visual Studio。 Vspackage 是 Visual Studio 的中央体系结构单元。 有关更多信息，请参见 [VSPackages](../../extensibility/internals/vspackages.md)。  
  
## <a name="visual-studio-shell"></a>Visual Studio Shell  
 Visual Studio shell 提供基本功能，并支持其组件 Vspackage 和 MEF 扩展之间的跨通信。 有关详细信息，请参阅 [Visual Studio Shell](../../extensibility/internals/visual-studio-shell.md)。  
  
## <a name="user-experience-guidelines"></a>用户体验指南  
 如果计划设计 Visual Studio 的新功能，则应该查看以下有关设计和可用性提示的准则： [Visual Studio 用户体验指南](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)。  
  
## <a name="commands"></a>命令  
 命令是完成任务（如打印文档、刷新视图或创建新文件）的函数。  
  
 扩展 Visual Studio 时，可以创建命令并将其注册到 Visual Studio shell。 您可以指定这些命令在 IDE 中的显示方式，例如，在菜单或工具栏上。 通常，自定义命令显示在 "**工具**" 菜单中，而用于显示工具窗口的命令将显示在 "**视图**" 菜单的 "**其他窗口**" 子菜单中。  
  
 创建命令时，还必须为它创建事件处理程序。 事件处理程序确定命令何时可见或启用，使你可以修改其文本，并确保命令在激活时正确响应。 在大多数情况下，IDE 使用接口处理命令 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 。 Visual Studio 中的命令从最内层命令上下文开始处理，并基于本地选择，并根据全局选择继续到最外层上下文。 添加到主菜单的命令可立即用于脚本编写。  
  
 有关详细信息，请参阅 [命令、菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)。  
  
## <a name="menus-and-toolbars"></a>菜单和工具栏  
 菜单和工具栏提供了一种方法，使用户可以调用命令。 菜单是通常在工具窗口顶部显示为单个文本项的命令行或列。 子菜单是当用户单击包括小箭头的命令时显示的辅助菜单。 当用户右键单击某些 UI 元素时，将显示上下文菜单。 一些常见的菜单名包括 **文件**、 **编辑**、 **视图**和 **窗口**。 有关详细信息，请参阅 [扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。  
  
 工具栏是按钮和其他控件（如组合框、列表框和文本框）的行或列。 工具栏按钮通常具有图标图像，例如 " **打开文件** " 命令的文件夹图标或用于 **打印** 命令的打印机。 所有工具栏元素都与命令关联。 单击工具栏按钮时，其关联的命令将运行。 对于下拉控件，下拉列表中的每一项都与不同的命令相关联。 某些工具栏控件（如拆分控件）是混合的。 控件的一端是工具栏按钮，另一端是在单击时显示多个命令的向下箭头。  
  
## <a name="tool-windows"></a>工具窗口  
 工具窗口用于在 IDE 中显示信息。 **工具箱**、 **解决方案资源管理器**、" **属性** " 窗口和 **Web 浏览器** 都是工具窗口的示例。  
  
 工具窗口通常提供用户可与之交互的各种控件。 例如，" **属性** " 窗口允许用户设置用于特定用途的对象的属性。 " **属性** " 窗口是专用化的，但也是常规的，因为它可在许多不同的情况下使用。 同样， **输出** 窗口是专用的，因为它提供基于文本的输出，但通常是因为 Visual studio 中的许多子系统都可以使用它向 Visual Studio 用户提供输出。  
  
 请考虑 Visual Studio 的下图，其中包含多个工具窗口。  
  
 ![屏幕截图](../../extensibility/internals/media/t1gui.png "T1gui")  
  
 某些工具窗口停靠在单个窗格上，该窗格显示 "解决方案资源管理器工具" 窗口并隐藏其他工具窗口，但通过单击 "选项卡" 使其可用。 该图显示了两个其他工具窗口，即 " **错误列表** " 和 " **输出** " 窗口，它们停靠在一个窗格中。  
  
 还显示了主文档窗格，其中显示了多个编辑器窗口。 尽管工具窗口通常只包含一个实例 (例如，您只能打开一个 **解决方案资源管理器**) ，编辑器窗口可以有多个实例，每个实例用于编辑单独的文档，但所有这些实例都停靠在同一窗格中。 图片显示一个文档窗格，其中包含两个编辑器窗口，一个窗体设计器窗口，一个显示起始页的浏览器窗口。 可以通过单击 "选项卡" 来使用文档窗格中的所有窗口，但包含 EditorPane.cs 文件的编辑器窗口是可见和活动的。  
  
 扩展 Visual Studio 时，你可以创建工具窗口，使 Visual Studio 用户能够与你的扩展交互。 还可以创建自己的编辑器，使 Visual Studio 用户可以编辑文档。 由于你的工具窗口和编辑器将集成到 Visual Studio 中，因此你不必对其进行编程以使其正确停靠或显示在选项卡上。 在 Visual Studio 中正确注册后，它们将在 Visual Studio 中自动具有工具窗口和文档窗口的典型功能。 有关详细信息，请参阅 [扩展和自定义工具窗口](../../extensibility/extending-and-customizing-tool-windows.md)。  
  
## <a name="document-windows"></a>文档窗口  
 文档窗口是多文档界面 (MDI) 窗口的一个带框子窗口。 文档窗口通常用于宿主文本编辑器、窗体编辑器 (也称为设计器) 或编辑控件，但它们也可以承载其他功能类型。 " **新建文件** " 对话框包括 Visual Studio 提供的文档窗口的示例。  
  
 大多数编辑器都是特定于编程语言或文件类型的，如 HTML 页面、框架集、c + + 文件或头文件。 在 " **新建文件** " 对话框中选择模板后，用户会动态地为与模板关联的文件类型创建一个文档窗口。 当用户打开现有文件时，也会创建文档窗口。  
  
 文档窗口限制为 MDI 工作区。 每个文档窗口的顶部都有一个选项卡，并且 tab 键顺序链接到可能在 MDI 区域中打开的其他窗口。 右键单击文档窗口的选项卡将显示一个快捷菜单，其中包含用于将 MDI 区域拆分为多个水平或垂直选项卡组的选项。 拆分 MDI 区域可以同时查看多个文件。 有关详细信息，请参阅 [文档窗口](../../extensibility/internals/document-windows.md)。  
  
## <a name="editors"></a>编辑器  
 Visual Studio 编辑器允许你对其进行自定义，并通过 Managed Extensibility Framework (MEF) ，将其用于自己的内容类型。 在许多情况下，你不需要创建 VSPackage 来扩展编辑器，不过，如果你想要在 shell 中包含功能 (例如，菜单命令或快捷键) ，则可以将 MEF 扩展与 VSPackage 结合使用。  
  
 你还可以创建自定义编辑器，例如，如果你想要对数据库进行读取和写入，或者想要使用设计器。 你还可以使用 "记事本" 或 "Microsoft 写字板" 等外部编辑器。 有关详细信息，请参阅 [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。  
  
## <a name="language-services"></a>语言服务  
 如果希望 Visual Studio 编辑器支持新的编程关键字，甚至还支持新的编程语言，请创建语言服务。 每个语言服务都可以完全、部分或根本不实现某些编辑器功能。 根据配置方式的不同，语言服务可以提供语法突出显示、大括号匹配、IntelliSense 支持和编辑器中的其他功能。  
  
 语言服务核心是一个分析器和一个扫描程序。 扫描器 (或词法分析器) 将源文件分为称为标记的元素，而分析器在这些标记之间建立关系。 创建语言服务时，必须实现分析器和扫描程序，使 Visual Studio 能够理解语言的标记和语法。 你可以创建托管或非托管的语言服务。 有关详细信息，请参阅 [旧版语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)。  
  
## <a name="projects"></a>项目  
 在 Visual Studio 中，项目是开发人员用来组织和生成源代码和其他资源的容器。 项目使你可以组织、构建、调试和部署源代码，引用 Web 服务和数据库以及其他资源。 Vspackage 可以通过提供项目类型、项目子类型和自定义工具来扩展 Visual Studio 项目系统。  
  
 还可以将项目收集到解决方案中，这是一个或多个项目的分组，可协同工作以创建应用程序。 与解决方案有关的项目和状态信息存储在两个解决方案文件中，基于文本的解决方案 ( .sln) 文件，而二进制解决方案用户选项 ( .suo) 文件中。 这些文件类似于早期版本中使用的组 ( vbg) 文件 [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ，以及工作区 () 和用户选项 () 中使用的文件。 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]  
  
 有关详细信息，请参阅 [项目](../../extensibility/internals/projects.md) 和 [解决方案](../../extensibility/internals/solutions-overview.md)。  
  
## <a name="project-and-item-templates"></a>项目和项模板  
 Visual Studio 包括预定义的项目模板和项目项模板。 还可以创建自己的模板或从社区获取模板，然后将其集成到 Visual Studio 中。 [MSDN 代码库](https://code.msdn.microsoft.com/site/search?query=visual%20studio)是用于浏览模板和扩展的位置。  
  
 模板包含生成特定类型的应用程序、控件、库或类所需的项目结构和基本文件。 如果要开发类似于其中一个模板的软件，请创建一个基于该模板的项目，然后修改该项目中的文件。  
  
> [!NOTE]
> 项目不支持此模板体系结构 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 。 有关如何创建 [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)] 项目模板的信息，请参阅 [设计向导](https://msdn.microsoft.com/library/a7c0be7e-9297-4fed-83e3-5645c896d56b)。  
  
 有关详细信息，请参阅 [添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。  
  
## <a name="properties-and-options"></a>属性和选项  
 " **属性** " 窗口显示单个或多个选定项的属性： " [扩展属性](../../extensibility/internals/extending-properties.md) " 选项页包含与特定组件相关的选项集，如编程语言或 VSPackage： [选项和选项页](../../extensibility/internals/options-and-options-pages.md)。 设置通常是 UI 相关的功能，可以导入和导出： [对用户设置的支持](../../extensibility/internals/support-for-user-settings.md)。  
  
## <a name="visual-studio-services"></a>Visual Studio 服务  
 服务提供一组特定的接口供组件使用。 Visual Studio 提供了一组可供任何组件使用的服务，包括扩展。 例如，Visual Studio 服务使工具窗口可以动态显示或隐藏，启用对帮助、状态栏或 UI 事件的访问。 Visual Studio 编辑器还提供可由编辑器扩展导入的服务。 有关详细信息，请参阅 [使用和提供服务](../../extensibility/using-and-providing-services.md)。  
  
## <a name="debugger"></a>调试器  
 调试器是特定于语言的调试组件的用户界面。 如果已创建新的语言服务，则需要创建一个特定的调试引擎，以挂钩到调试器。 有关详细信息，请参阅 [Visual Studio 调试器扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)。  
  
## <a name="source-control"></a>源代码管理  
 有关实现源代码管理插件或 VSPackage 的信息，请参阅 [源代码管理](../../extensibility/internals/source-control.md)。  
  
## <a name="wizards"></a>向导  
 您可以与新的项目类型一起创建一个向导，以便向导可以帮助您的用户在创建该类型的新项目时做出正确的决策。 有关详细信息，请参阅 [向导](../../extensibility/internals/wizards.md)。  
  
## <a name="custom-tools"></a>自定义工具  
 自定义工具使你可以将工具与项目中的项相关联，并在每次保存文件时运行该工具。 有关详细信息，请参阅 [自定义工具](../../extensibility/internals/custom-tools.md)。  
  
## <a name="vssdk-utilities"></a>VSSDK 实用工具  
 VSSDK 包含一组可用于 Vspackage 的不同方面的实用程序。 有关详细信息，请参阅 [VSSDK 实用程序](../../extensibility/internals/vssdk-utilities.md)。  
  
## <a name="using-windows-installer"></a>使用 Windows Installer  
 在某些情况下，你可能需要使用 Windows Installer 而不是 VSIX 安装程序：例如，你可能需要写入注册表。 有关将 Windows Installer 与扩展结合使用的信息，请参阅使用 [Windows Installer 安装 vspackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)。  
  
## <a name="help-viewer"></a>帮助查看器  
 你可以将自己的帮助和 F1 页面集成到帮助查看器中。 有关详细信息，请参阅 [MICROSOFT HELP VIEWER SDK](../../extensibility/internals/microsoft-help-viewer-sdk.md)。
