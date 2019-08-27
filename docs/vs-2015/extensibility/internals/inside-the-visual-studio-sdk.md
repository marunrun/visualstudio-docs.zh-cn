---
title: 在 Visual Studio SDK |Microsoft Docs
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
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687536"
---
# <a name="inside-the-visual-studio-sdk"></a>深入探究 Visual Studio SDK
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

本部分提供有关 Visual Studio 扩展，其中包括 Visual Studio 体系结构、 组件、 服务、 架构、 实用工具和类似的内容的详细信息。  
  
## <a name="extensibility-architecture"></a>可扩展性体系结构  
 下图显示了 Visual Studio 扩展性体系结构。 Vspackage 提供应用程序功能，作为服务在 IDE 间共享。 对标准 IDE 还提供了广泛的服务，如<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>，它提供的信息对 IDE 窗口化功能的访问。  
  
 ![环境体系结构图](../../extensibility/internals/media/environment.gif "环境")  
Visual Studio 体系结构的通用的视图  
  
## <a name="vspackages"></a>VSPackages  
 VSPackage 是软件模块，它们通过 UI 元素、服务、项目、编辑器和设计器来组成并扩展 Visual Studio。 Vspackage 是 Visual Studio 的中央体系结构单元。 有关更多信息，请参见 [VSPackages](../../extensibility/internals/vspackages.md)。  
  
## <a name="visual-studio-shell"></a>Visual Studio Shell  
 在 Visual Studio shell 提供基本功能和支持，其组件 Vspackage 和 MEF 扩展之间的跨通信。 有关详细信息，请参阅[Visual Studio Shell](../../extensibility/internals/visual-studio-shell.md)。  
  
## <a name="user-experience-guidelines"></a>用户体验指南  
 如果您打算设计的 Visual Studio 的新功能，您应该看看以下准则，以便设计和可用性的提示：[Visual Studio 用户体验指南](../../extensibility/ux-guidelines/visual-studio-user-experience-guidelines.md)。  
  
## <a name="commands"></a>命令  
 命令是完成任务（如打印文档、刷新视图或创建新文件）的函数。  
  
 扩展 Visual Studio 时，可以创建命令并将它们注册 Visual Studio shell。 您可以指定如何这些命令将显示在 IDE 中，例如，菜单或工具栏上。 自定义命令通常显示在**工具**菜单中和用于显示工具窗口的命令将显示**其他 Windows**的子菜单**视图**菜单。  
  
 在创建命令时，还必须为其创建事件处理程序。 事件处理程序确定命令何时可见或启用，可让你修改其文本，保证，该命令会做出适当响应激活时。 在大多数情况下，IDE 命令处理使用<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口。 Visual Studio 中的命令的处理从最内层命令上下文，基于本地选择和到最外层的上下文，基于全局选择继续操作。 添加到主菜单的命令可立即用于脚本编写。  
  
 有关详细信息，请参阅[命令、 菜单和工具栏](../../extensibility/internals/commands-menus-and-toolbars.md)。  
  
## <a name="menus-and-toolbars"></a>菜单和工具栏  
 菜单和工具栏提供的用户来调用命令的方法。 菜单的行或列的通常显示为单个文本项工具窗口顶部的命令。 子菜单是辅助显示在用户单击包含一个小箭头的命令时的菜单。 当用户右键单击某些 UI 元素时，会显示上下文菜单。 一些常见的菜单名包括**文件**，**编辑**，**视图**，以及**窗口**。 有关详细信息，请参阅[扩展菜单和命令](../../extensibility/extending-menus-and-commands.md)。  
  
 工具栏的行或列的按钮和其他控件，如组合框、 列表框和文本框。 工具栏按钮通常具有图标图像，如的文件夹图标**打开的文件**命令或为打印机**打印**命令。 工具栏上的所有元素都都与命令关联。 当您单击工具栏按钮时，其关联的命令运行。 对于下拉列表控件，下拉列表中的每个项都与不同命令关联。 某些工具栏控件，如拆分器控件，是混合模式。 控件的一端是工具栏按钮和另一端是在单击时显示多个命令的向下箭头。  
  
## <a name="tool-windows"></a>工具窗口  
 工具窗口用于在 IDE 中显示的信息。 **工具箱**，**解决方案资源管理器**，**属性**窗口中，和**Web 浏览器**是工具窗口的示例。  
  
 工具窗口通常会提供用户可与之交互的各种控件。 例如，**属性**窗口让用户设置具有特殊用途的对象的属性。 **属性**窗口是这个意义上说，专用的但还常规，因为在许多不同的情况下可以使用它。 同样，**输出**窗口专用化，因为它提供了基于文本的输出，但常规，因为在 Visual Studio 中的许多子系统可以使用它来向 Visual Studio 用户提供输出。  
  
 请考虑下图的 Visual Studio 中，其中包含多个工具窗口。  
  
 ![屏幕截图](../../extensibility/internals/media/t1gui.png "T1gui")  
  
 某些工具窗口一起停靠在单一的解决方案资源管理器工具窗口将显示和隐藏其他工具窗口，但使其可通过单击选项卡。 图中显示了两个其他工具窗口**错误列表**并**输出**窗口中上一个窗格, 停靠在一起。  
  
 此外显示的是主文档窗格中，其中显示了多个编辑器窗口。 尽管工具窗口通常有一个实例 (例如，可以打开一个**解决方案资源管理器**)，编辑器窗口可以具有多个实例，其中每个可用于编辑一个单独的文档，但所有这些都在停靠同一个窗格。 图显示了一个文档窗格具有两个编辑器窗口、 一个窗体设计器窗口中，以及一个显示启动页的浏览器窗口。 在文档窗格中的所有窗口都都可通过单击选项卡上，但包含 EditorPane.cs 文件的编辑器窗口是可见且处于活动状态。  
  
 扩展 Visual Studio 时，可以通过扩展来创建 windows，Visual Studio 用户可交互的工具。 此外可以创建自己的编辑器的让 Visual Studio 用户编辑文档。 工具窗口和编辑器将集成到 Visual Studio 中，因为没有它们以停靠或正确显示选项卡上进行编程。 时正确注册 Visual Studio 中，它们会自动具有工具窗口和文档窗口在 Visual Studio 中的典型功能。 有关详细信息，请参阅[扩展和自定义工具 Windows](../../extensibility/extending-and-customizing-tool-windows.md)。  
  
## <a name="document-windows"></a>文档窗口  
 文档窗口是带边框的子窗口的多文档界面 (MDI) 窗口。 文档窗口通常要用于宿主的文本编辑器、 窗体编辑器 （也称为设计器） 或编辑控件，但它们还可以托管其他功能的类型。 **新的文件**对话框包括 Visual Studio 提供的文档窗口的示例。  
  
 大多数编辑器是特定于编程语言或文件类型，如 HTML 页，框架集，C++文件或标头文件。 通过选择中的模板**新的文件**对话框中，用户动态创建一个文档窗口是与模板关联的文件类型的编辑器。 当用户打开现有文件，还会创建一个文档窗口。  
  
 文档窗口仅限于在 MDI 工作区。 每个文档窗口的顶部，有一个选项卡和 tab 键顺序链接至其他 MDI 区域中可以在打开的窗口。 右键单击文档窗口的选项卡显示包括用于将 MDI 区域拆分为多个水平或垂直选项卡组的选项的快捷菜单。 拆分 MDI 区可以同时查看多个文件。 有关详细信息，请参阅[文档 Windows](../../extensibility/internals/document-windows.md)。  
  
## <a name="editors"></a>编辑器  
 在 Visual Studio 编辑器允许您自定义它并将其用于自己的类型的内容通过 Managed Extensibility Framework (MEF)。 在许多情况下不需要创建 VSPackage 来扩展编辑器，但如果您想要包括从命令行程序 （例如，菜单命令或快捷键） 的功能，可以组合使用 VSPackage 的 MEF 扩展。  
  
 此外可以创建自定义编辑器，例如，如果你想要读取和写入到数据库，或者如果你想要使用设计器。 此外可以使用记事本或 Microsoft 写字板等外部编辑器。 有关详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。  
  
## <a name="language-services"></a>语言服务  
 如果你想在 Visual Studio 编辑器以支持新的编程关键字或甚至新编程语言，则创建语言服务。 每个语言服务完全、 部分，或根本不可能实现某些编辑器功能。 根据配置方式，该语言服务可以提供语法突出显示、 大括号匹配、 IntelliSense 支持和编辑器中的其他功能。  
  
 语言服务的核心是一个分析器和扫描程序。 扫描程序 （或词法分析器） 将源文件划分为称为标记的元素，并分析程序建立这些令牌之间的关系。 当创建语言服务时，必须实现分析器和扫描程序，以便 Visual Studio 可以理解的令牌和语言的语法。 可以创建托管或非托管语言服务。 有关详细信息，请参阅[旧版语言服务扩展性](../../extensibility/internals/legacy-language-service-extensibility.md)。  
  
## <a name="projects"></a>项目  
 在 Visual Studio 中，项目是开发人员用于组织和生成的源代码和其他资源的容器。 项目的让组织、 生成、 调试和部署的源代码，请对 Web 服务和数据库，以及其他资源的引用。 Vspackage 可以通过提供项目类型、 项目子类型和自定义工具来扩展 Visual Studio 项目系统。  
  
 项目还可能收集到一个解决方案，其中是协同工作以创建应用程序的一个或多个项目的分组。 适用于解决方案的项目和状态信息存储在两个解决方案文件、 基于文本的解决方案 (.sln) 文件和二进制解决方案用户选项 (.suo) 文件。 这些文件是与组 (文件.vbg) 文件的早期版本中使用的类似[!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]，以及在工作区 (.dsw) 和用户选项 (.opt) 文件的早期版本中使用[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]。  
  
 有关详细信息，请参阅[项目](../../extensibility/internals/projects.md)并[解决方案](../../extensibility/internals/solutions-overview.md)。  
  
## <a name="project-and-item-templates"></a>项目和项模板  
 Visual Studio 包含预定义的项目模板和项目项模板。 可以还使您自己的模板或获取社区中的模板，然后将其集成到 Visual Studio。 [MSDN 代码库](https://code.msdn.microsoft.com/site/search?query=visual%20studio)是为模板和扩展的位置。  
  
 模板包含的项目结构和所需构建特定类型的应用程序、 控件、 库或类的基本文件。 当你想要开发软件，类似于一个模板时，创建基于模板的项目，然后修改该项目中的文件。  
  
> [!NOTE]
> 此模板体系结构不支持为[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]项目。 有关如何创建[!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]项目模板，请参阅[设计向导](https://msdn.microsoft.com/library/a7c0be7e-9297-4fed-83e3-5645c896d56b)。  
  
 有关详细信息，请参阅[添加项目和项目项模板](../../extensibility/internals/adding-project-and-project-item-templates.md)。  
  
## <a name="properties-and-options"></a>属性和选项  
 **属性**窗口显示单个或多个选定的项的属性：[将属性扩展](../../extensibility/internals/extending-properties.md)选项页包含一系列的适用于特定组件，例如，一种编程语言或 VSPackage 的选项：[选项和选项页](../../extensibility/internals/options-and-options-pages.md)。 设置为通常与 UI 相关的功能，可以导入和导出：[支持用户设置](../../extensibility/internals/support-for-user-settings.md)。  
  
## <a name="visual-studio-services"></a>Visual Studio Services  
 服务提供了一组特定的组件使用的接口。 Visual Studio 提供了一组可由任何组件，包括扩展的服务。 例如，Visual Studio 服务，工具窗口，以显示或隐藏动态，启用对帮助、 状态栏或 UI 事件的访问。 在 Visual Studio 编辑器还提供可由编辑器扩展导入的服务。 有关详细信息，请参阅[使用和提供服务](../../extensibility/using-and-providing-services.md)。  
  
## <a name="debugger"></a>调试器  
 调试器是特定于语言的调试组件的用户界面。 如果创建新的语言服务后，您需要创建特定的调试引擎将在挂接到调试器。 有关详细信息，请参阅[Visual Studio 调试器可扩展性](../../extensibility/debugger/visual-studio-debugger-extensibility.md)。  
  
## <a name="source-control"></a>源代码管理  
 有关实现 VSPackage 或源代码管理插件的信息，请参阅[源代码管理](../../extensibility/internals/source-control.md)。  
  
## <a name="wizards"></a>向导  
 可以使用新的项目类型创建向导结合使用，在创建该类型的新项目时，你的用户，以便向导可以帮助做出正确的决策。 有关详细信息，请参阅[向导](../../extensibility/internals/wizards.md)。  
  
## <a name="custom-tools"></a>自定义工具  
 自定义工具可以在项目中的项相关联的工具和运行该工具，每次保存该文件。 有关详细信息，请参阅[自定义工具](../../extensibility/internals/custom-tools.md)。  
  
## <a name="vssdk-utilities"></a>VSSDK 实用工具  
 VSSDK 包括一组可能需要才能使用 Vspackage 的不同方面的实用程序。 有关详细信息，请参阅[VSSDK 实用工具](../../extensibility/internals/vssdk-utilities.md)。  
  
## <a name="using-windows-installer"></a>使用 Windows 安装程序  
 在某些情况下，您可能需要使用 Windows 安装程序而不是 VSIX 安装程序： 例如，您可能需要写入注册表。 有关使用 Windows 安装程序通过你的扩展的信息，请参阅[使用 Windows Installer 安装 Vspackage](../../extensibility/internals/installing-vspackages-with-windows-installer.md)。  
  
## <a name="help-viewer"></a>帮助查看器  
 可以将你自己的帮助和 F1 页面集成到帮助查看器。 有关详细信息，请参阅[Microsoft 帮助查看器 SDK](../../extensibility/internals/microsoft-help-viewer-sdk.md)。
