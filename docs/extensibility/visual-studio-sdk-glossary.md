---
title: Visual Studio SDK 词汇表 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- glossary [Visual Studio SDK]
ms.assetid: b64d432b-c39b-4904-ad18-3c3218b6e3aa
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c5aa8398f3a102031c3a40074f76557ef311d4d7
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66322410"
---
# <a name="visual-studio-sdk-glossary"></a>Visual Studio SDK 词汇表
此术语表中使用的术语提供定义[!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)]文档。

## <a name="terms"></a>术语
 外接程序的实用程序应用程序、 驱动程序或添加到主应用程序的其他软件。 在 Visual Studio 集成的开发环境 (IDE) 中外, 接程序是扩展的功能的 IDE 的自动化基于应用程序。

 自动化模型自动化模型中，在以前版本的 Visual Studio 扩展性模型，已知是为您提供了一个编程接口访问的基础例程该驱动器的 IDE。 外接程序、 向导和宏使用自动化模型来控制中的对象或扩展 IDE 的功能。

 命令 UI 上下文关联的 GUID 与 UI 命令或工具栏等元素的可见性。 命令 UI 上下文是与选定内容上下文不同，而不附加到窗口。

 命令 UI 上下文可用于：

- 将 GUID 分配给特定窗口被激活时，将显示一个工具栏。

- 将 GUID 分配给命令的可用性，而无需加载或运行 VSPackage。

- 将分配一个 GUID 以影响活动的键绑定。

- 将分配一个 GUID 以开启宏录制。

- 将分配一个 GUID 以激活调试模式或设计和在编辑器中的运行的模式之间进行切换。

  组件可以不具有任何预先存在相关信息的软件实现该应用程序建立应用程序的功能的一部分的软件。 组件和应用程序之间的通信是仅通过 OLE 风格的接口。

  组件管理器的服务， `SOleComponentManager`，它提供非用户界面协调服务顶级组件。 `SOleComponentManager`服务实现`IOleComponentManager`接口。

  组件 UI 管理器的服务， `SOleComponentUIManager`，提供用户界面协调服务。 `SOleComponentUIManager`服务实现`IOleComponentUIManager`和`IOleInPlaceComponentUIManager`接口。

  上下文包`IVsUserContext`对象 （COM 对象） 附加到环境组件。 此对象保存查找关键字**F1**关键字和与组件相关的属性。 上下文包此外指向链接到其任何子上下文包。

  具有与之关联的上下文包在 IDE 中的上下文提供程序的组件。 此类组件包括工具窗口、 编辑器或项目层次结构。

  设计器允许用户操作 UI （窗体、 按钮和其他控件） 的元素的编程接口。

  封装一个世界中的文档的基础数据的 DocData 的 COM 对象没有文档/视图分离 （例如，在文本编辑器的情况下，这会基础文本编辑器的所有视图的文本缓冲区）。 如果 EditorFactory 不提供此对象，IDE 将生成一个代表其。 此对象的责任是管理数据暂留和多个共享的语义视图通过此相同`DocData`。 如果`DocData`对象支持`IOleCommandTarget`接口，它已包含在 UIShell 命令路由。

  DocObject 技术用来承载在宿主所提供的范围内的用户界面。 具体而言，此术语指支持任何嵌入`IOleDocument`和相关的接口。 此技术有许多潜在应用程序，例如 COM 文档的实现细节，在 Visual Basic 5.0 中的工具窗口、 ActiveX 设计器在 Visual Basic 6.0 中，依次类推。

  文档用来泛指文档作为一个整体，同时`DocData`和`DocView`。 例如，包含 DocumentFrame `DocView`，，但它还会保留对引用`DocData`处理持久性。

  DocView DocObject/嵌入/窗口窗格在用户查看和操作基础交互`DocData`。 用户没有利用一部分的文档/视图分离`DocObject`接口设计。 用户使用整个 DocObject 充当一个视图，而不是使用更抽象 （和不太正式化） 的这一概念的基础数据称为`DocData`。 `DocView` 始终与文档框架对象 （MDI 子窗口） 的 IDE 嵌入对象。

  DTE `DTE` （开发工具扩展性） 对象是在 Visual Studio 自动化模型中，允许您以编程方式自动执行和扩展 IDE 的最顶层的访问点。

  动态帮助窗口工具窗口，通过 IDE 实现，并显示一系列查找关键字或**F1**帮助主题。

  编辑器实现的代码 （类，CLSID） `DocView`。 它还实现`DocData`如果受支持的视图和数据分离。

  修改的扩展的功能自定义，或将添加到 IDE。 创建使用自动化模型或 Vspackage 扩展。

  外部编辑器并不特定于 IDE 中，如 Microsoft Word 的编辑器。 它通过其自己的机制已注册，并可以在 IDE 外部使用。 如果可以嵌入此编辑器，它将显示在 IDE 中窗口。 如果它不能嵌入，将创建一个单独的顶级窗口。

  层次结构树的节点，与一组属性相关联的每个节点。

  使用无模式的顶级窗口和作为独立应用程序窗口中，可以有效地运行，但实现为进程内对象的独立顶级组件的组件。 因此，独立的顶级组件必须协调模式和消息循环与 IDE 的服务。 进程内对象不具有其自己的消息循环。

  信息提供程序的信息提供程序是一个模块，可以查找关键字，并返回的窗体中的主题，列表`IVsUserContextItem`对象。 若要提供**F1**并查找关键字的项有关的信息提供程序、 要注册已编译的帮助文件 ( *。HxS*) 与系统。 这些文件中的帮助主题提供的动态帮助窗口中显示，并显示是否在用户按下的主题列表**F1**。

  就地组件实现的 VSPackage 对象`IOleInPlaceComponent`接口来管理以可视方式包含在归 IDE 的文档窗口的窗口。 就地组件不参与标准 OLE 菜单合并;而是他们将其用户界面元素集成到 IDE。

  有两种类型的就地组件： 硬编码的就地组件和组件控件。

  硬编码的就地组件有菜单、 工具栏和紧密集成到 IDE 中，显示为如果它们已直接内置于 IDE 的用户界面的命令。

  组件控件没有任何集成到 IDE; 其自身用户界面元素相反，它们使用 IDE 的菜单、 命令和工具栏。 例如，粗体命令无法用于在窗体中嵌入的富文本控件中的选定的文字设置为粗体。 但是，组件控件可以请求显示动态安装特定于组件的 UI 元素。

  语言服务一组对象，它允许代码编辑器，例如，文本将标记和着色的 VSPackage 开发人员实现计算机语言的功能。

  杂项文件项目用于映射到不在任何项目中的房子打开文件的项目。 此项目中的项列表不永久保存。

  项目的项目组成层次结构对象或 COM 对象实现`IVsHierarchy`接口。

  特定于项目的设计器或编辑器的设计器不能使用独立于项目类型。 所有特定于项目的设计器必须在注册表中输入其编辑器工厂的信息。 IDE 然后可以实例化设计器时，只要在特定项目中打开特定文件类型。

  项目类型窗口的窗口，它会持续跟踪当前处于活动状态的项目层次结构和项从全局选定内容上下文。 项目类型 windows 使用`SVsTrackSelectionEx`服务发出警报的更改的 IDE，并能够将反馈显示给用户。 解决方案资源管理器是一个项目类型窗口的示例。

  属性窗口以前称为属性浏览器。

  基于引用的项目不需要为位于相同的目录中的项目文件的项目。 相反，对文件来自其他不相关的目录的引用存储和维护项目本身。

  运行文档表内部结构依据 IDE 维护的所有当前打开的文档列表。 该列表包含所有打开的文档在内存中而不考虑是否当前正在编辑的文档。 文档是包括在编辑器中，项目中的文件或主项目文件 （例如，*.vcproj 文件） 中打开的存储的过程的保存的任何项。

  选定内容上下文是在 IDE 中的每个窗口的详细信息的一部分，用于跟踪活动选择的数据。 选定内容上下文包括：

- 指向`IVsHierarchy`项目层次结构的接口

- 项目项的项标识符。

- 指向`ISelectionContainer`用于访问属性的活动对象的接口。

- 元素值的数组。

  服务驻留在单个的 COM 对象的一组 COM 接口的协定。 时创建一个服务，它由 GUID 标识，定义执行该服务的 COM 接口集。 COM 对象使用服务相互通信。

  解决方案的用户的工作的相关项目进行分组。

  标准设计器设计器，可独立于项目类型。 所有标准的设计器必须在注册表中输入其编辑器工厂的信息。 IDE 然后可以实例化设计器每次打开具有特定扩展名的文件。 数据必须保存到文件。

  标准编辑器可以使用独立于任何特定项目类型的编辑器。 此类编辑器都有 EditorFactories 在注册表中注册。 这使 IDE，可查找并调用编辑器。

  嵌入的标准 OS 编辑器并不是特定于 Visual Studio。 注册使用已知的 Win32 键 （例如，Win32 资源管理器知道如何调用）。 如果可以嵌入此类编辑器，在编辑器仍会显示在 IDE 中其原位置。 否则，为此类编辑器创建一个单独的顶级窗口。

  子上下文包`IVsUserContext`对象链接到上下文包。 该对象包含查找关键字**F1**关键字和选择的 IDE 组件中的属性。 子上下文的示例包括一个命令中的工具窗口中或在编辑器中的关键字。

  任务列表工具窗口，通过 IDE 实现，并显示活动任务的列表。

  文本缓冲区对象的公用名`VSTextBuffer`。

  文本视图对象的公用名`VSTextView`。

  作为无模式弹出窗口中，与在 IDE 的用户界面紧密协作的工具顶级组件的组件。 独立的顶级组件一样工具顶级组件还必须协调模式和消息循环与 IDE 的服务。

  顶级组件 VSPackage 对象，用于管理无模式的顶层窗口，而不是一个 IDE 窗口的工作区。 顶级组件实现`IOleComponent`接口以利用空闲时间的消息循环服务，例如访问。

  UI 活动 VSPackage 对象是可见且当前具有焦点。

  实现 UI 层次结构 COM 对象`IVsUIHierarchy`接口以允许显示的层次结构。 UI 层次结构窗口实现`ISelectionContainer`接口更新属性窗口; 其他项目类型窗口可以使用此实现中，如果所需的。

  VSCT Visual Studio 命令表。 .Vsct 文件包含有关布局和菜单、 工具栏和 XML 格式中的命令的行为的信息。

  VSPackage 通过参与一个或多个以下项来扩展 Visual Studio IDE 的软件可安装部分： 用户界面、 服务、 项目类型或编辑器/设计器。 VSPackage 包含实现的 COM 对象`IVsPackage`接口和一个或多个其他 COM 对象实现其他接口以支持所选内容和其他功能。 此外，VSPackage 还具有特定的注册要求。