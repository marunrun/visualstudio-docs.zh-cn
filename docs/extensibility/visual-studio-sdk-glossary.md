---
title: Visual Studio SDK 术语表 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- glossary [Visual Studio SDK]
ms.assetid: b64d432b-c39b-4904-ad18-3c3218b6e3aa
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 332e606e689e9394f2fcdc8cbc902e2d4a6e5ab5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80698160"
---
# <a name="visual-studio-sdk-glossary"></a>Visual Studio SDK 术语表
此术语表提供文档中使用的术语的定义 [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] 。

## <a name="terms"></a>术语
 外接程序应用程序、驱动程序或添加到主应用程序的其他软件。 在 Visual Studio 集成开发环境中 (IDE) ，外接程序是一种基于自动化的应用程序，用于扩展 IDE 的功能。

 自动化模型在 Visual Studio 的早期版本中称为扩展性模型，它是一个编程接口，可让你访问驱动 IDE 的基础例程。 外接程序、向导和宏使用自动化模型中的对象来控制或扩展 IDE 的功能。

 GUID 与 UI 命令或元素（如工具栏）的可见性的命令 UI 上下文关联。 命令用户界面上下文与选择上下文不同，因为它不会附加到窗口中。

 命令用户界面上下文可用于：

- 将 GUID 分配给激活特定窗口时显示的工具栏。

- 将 GUID 分配给命令的可用性，而无需加载或运行 VSPackage。

- 分配一个 GUID 来影响活动键绑定。

- 分配一个 GUID 来打开宏记录。

- 分配一个 GUID 来激活调试模式，或在编辑器中的设计模式和运行模式之间切换。

  软件的组件部分，它可以成为应用程序功能的一部分，而无需在应用程序中包含有关软件实现的任何预先存在的信息。 组件和应用程序之间的通信仅通过 OLE 样式接口进行。

  组件管理器是一种服务， `SOleComponentManager` 它为顶级组件提供非用户界面协调服务。 `SOleComponentManager`服务实现 `IOleComponentManager` 接口。

  组件 UI 管理器服务， `SOleComponentUIManager` 提供用户界面协调服务。 `SOleComponentUIManager`服务实现 `IOleComponentUIManager` 和 `IOleInPlaceComponentUIManager` 接口。

  上下文包 `IVsUserContext` 附加到环境组件)  (COM 对象的对象。 此对象保存与组件相关的查找关键字、 **F1** 关键字和属性。 上下文包还会指向链接到它们的所有子上下文包。

  上下文提供程序中具有与之关联的上下文包的组件。 此类组件包含工具窗口、编辑器或项目层次结构。

  设计器一个编程接口，该接口允许用户使用) 的 UI (窗体、按钮和其他控件的元素。

  DocData 将一个 COM 对象封装在世界上的文档的基础数据，其中存在文档/视图分隔 (例如，在文本编辑器的情况下，这将是所有文本编辑器视图) 基础的文本缓冲区。 如果 EditorFactory 未提供此对象，IDE 将代表其提供一个对象。 此对象的责任是为多个视图管理数据持久性和共享语义 `DocData` 。 如果 `DocData` 对象支持 `IOleCommandTarget` 接口，则它包含在 UIShell 的命令路由中。

  用于在主机提供的框架内托管 UI 的 DocObject 技术。 更具体地说，此术语是指支持 `IOleDocument` 和相关接口的任何嵌入。 此技术有许多潜在的应用程序，如 COM 文档的实现细节、Visual Basic 5.0 中的工具窗口、Visual Basic 6.0 中的 ActiveX 设计器等。

  用于整体引用文档的文档- `DocData` 和和 `DocView` 。 例如，DocumentFrame 包含 `DocView` ，但它还保留对的引用 `DocData` 以处理持久性。

  DocView 用户交互以查看和操作基础的 DocObject/嵌入/Windowpane> `DocData` 。 用户不会利用作为界面设计一部分的文档/视图分隔 `DocObject` 。 用户使用整个 DocObject 作为视图，而不是使用更抽象的 (，而不是使用称为的基础数据的规范化) 概念 `DocData` 。 `DocView` 对象始终嵌入在 IDE (MDI 子窗口) 中的文档框架对象。

  DTE `DTE` (开发工具扩展性) 对象是 Visual Studio 自动化模型中最顶层的访问点，可用于以编程方式自动执行和扩展 IDE。

  IDE 实现的动态帮助窗口工具窗口，并显示查找关键字或 **F1** 帮助主题的列表。

  编辑器代码 (类、用于实现的 CLSID) `DocView` 。 `DocData`如果支持视图和数据分离，还会实现。

  扩展一项功能，该功能可修改、自定义或添加到 IDE。 您可以使用自动化模型或 Vspackage 创建扩展。

  外部编辑器不特定于 IDE 的编辑器，如 Microsoft Word。 它已通过其自身的机制注册，可以在 IDE 外部使用。 如果可以嵌入该编辑器，它将显示在 IDE 中的窗口内。 如果无法嵌入，则会创建一个单独的顶级窗口。

  节点的层次结构树，每个与一组属性相关联的节点。

  独立顶级组件是使用无模式顶级窗口的组件，它可以作为独立的应用程序窗口有效运行，但作为进程内对象实现。 因此，独立顶级组件必须与 IDE 协调模态和消息循环服务。 进程内对象没有自己的消息循环。

  信息提供程序信息提供程序是一个模块，它可以查找关键字并以对象的形式返回主题列表 `IVsUserContextItem` 。 若要为信息提供程序提供 **F1** 和查找关键字项，请将编译的帮助文件 (*。* 与系统) 的 HxS。 这些文件中的帮助主题提供 "动态帮助" 窗口中显示的主题列表，并显示用户是否按 **F1**。

  就地组件一个 VSPackage 对象，该对象实现 `IOleInPlaceComponent` 接口以管理可视化包含在 IDE 所拥有的文档窗口中的窗口。 就地组件不参与标准 OLE 菜单合并;而是将其用户界面元素集成到 IDE 中。

  存在两种类型的就地组件：硬编码的就地组件和组件控件。

  硬编码的就地组件具有紧密集成到 IDE 用户界面的菜单、工具栏和命令，就好像它们是直接内置到 IDE 中一样。

  组件控件没有任何自己的用户界面元素集成到 IDE 中;而是使用 IDE 的菜单、命令和工具栏。 例如，Bold 命令可用于在嵌入在窗体中的多格式文本控件中以粗体显示选定的单词。 不过，组件控件可以请求显示动态安装的特定于组件的 UI 元素。

  语言服务一组对象，这些对象允许 VSPackage 开发人员实现计算机语言代码编辑器的功能，如文本标记和着色。

  用于承载不在任何项目中的打开文件的杂项文件项目项目。 此项目中的项列表不会持久保存。

  项目项目由层次结构对象或实现接口的 COM 对象组成 `IVsHierarchy` 。

  项目特定设计器或编辑器不能独立于项目类型使用的设计器。 所有特定于项目的设计器都必须在注册表中输入其编辑器工厂信息。 每当在特定项目中打开某一文件类型时，IDE 就可以实例化设计器。

  项目类型窗口一个持续跟踪全局选择上下文中当前活动的项目层次结构和项目的窗口。 项目类型 windows 使用该 `SVsTrackSelectionEx` 服务对 IDE 发出更改并向用户显示反馈。 解决方案资源管理器是项目类型窗口的一个示例。

  属性窗口以前的属性浏览器。

  基于引用的项目项目，不需要项目文件位于同一目录中。 相反，由项目本身存储和维护来自其他不相关目录的文件的引用。

  运行文档表内部结构，IDE 将通过该结构维护所有当前打开的文档的列表。 此列表包括内存中所有打开的文档，无论当前是否正在编辑这些文档。 文档是保存的任何项，包括在编辑器中打开的存储过程、项目中的文件或主项目文件 (例如，* vcproj 文件) 。

  选择上下文数据，它是 IDE 中每个窗口的详细信息的一部分，用于跟踪活动选项。 选择上下文包含：

- 指向 `IVsHierarchy` 项目层次结构的接口的指针

- 项目项的项标识符。

- 指向接口的指针，该 `ISelectionContainer` 接口提供对活动对象的属性的访问。

- 元素值的数组。

  为驻留在单个 COM 对象中的一组 COM 接口为协定提供服务。 创建由 GUID 标识的服务时，可以定义执行该服务的 COM 接口集。 COM 对象使用服务相互通信。

  用户工作的相关项目的解决方案组。

  标准设计器：可独立于项目类型使用的设计器。 所有标准设计器都必须在注册表中输入其编辑器工厂信息。 只要打开具有特定扩展名的文件，IDE 就可以实例化设计器。 数据必须保存到文件。

  可独立于任何特定项目类型使用的标准编辑器编辑器。 此类编辑器在注册表中注册了 EditorFactories。 这允许 IDE 定位并调用编辑器。

  标准操作系统编辑器不特定于 Visual Studio 的嵌入。 它使用众所周知的 Win32 密钥注册 (例如，Win32 资源管理器知道如何调用) 。 如果此类编辑器可以嵌入，则编辑器仍会显示在 IDE 中的位置。 否则，将为此类编辑器创建一个单独的顶级窗口。

  子上下文包 `IVsUserContext` 链接到上下文包的对象。 对象保存 IDE 组件中所选内容的查找关键字、 **F1** 关键字和属性。 子上下文的示例包括工具窗口中的命令或编辑器中的关键字。

  由 IDE 实现并显示活动任务的列表的任务列表工具窗口。

  对象的文本缓冲区公用名 `VSTextBuffer` 。

  对象的文本视图公用名 `VSTextView` 。

  刀具顶级组件作为无模式弹出窗口运行的组件，与 IDE 的用户界面紧密协作。 与独立的顶级组件一样，工具顶级组件还必须在 IDE 中协调模态和消息循环服务。

  顶级组件 VSPackage 对象，它管理无模式顶级窗口，而不是 IDE 窗口的工作区。 顶级组件实现 `IOleComponent` 接口以利用消息循环服务，例如访问空闲时间。

  UI 活动 VSPackage 对象，该对象可见且当前具有焦点。

  UI 层次结构一个 COM 对象，该对象实现 `IVsUIHierarchy` 接口以允许显示层次结构。 "UI 层次结构" 窗口实现了 `ISelectionContainer` 用于更新属性窗口的接口; 其他项目类型 windows 可以根据需要使用此实现。

  .VSCT Visual Studio 命令表。 .Vsct 文件包含有关菜单、工具栏和 XML 格式命令的位置和行为的信息。

  VSPackage 一款可安装的软件，它通过参与以下一项或多项来扩展 Visual Studio IDE：用户界面、服务、项目类型或编辑器/设计器。 VSPackage 由实现接口的 COM 对象 `IVsPackage` 和一个或多个实现其他接口以支持选择和其他功能的 com 对象组成。 此外，VSPackage 具有特定的注册要求。
