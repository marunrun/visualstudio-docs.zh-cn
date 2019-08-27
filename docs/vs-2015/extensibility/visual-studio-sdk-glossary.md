---
title: Visual Studio SDK 词汇表 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- glossary [Visual Studio SDK]
ms.assetid: b64d432b-c39b-4904-ad18-3c3218b6e3aa
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8c189c4c9e06d224d7cef296a2c39e732cbc29f6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62538702"
---
# <a name="visual-studio-sdk-glossary"></a>Visual Studio SDK 词汇表
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此术语表中使用的术语提供定义[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]文档。  
  
## <a name="terms"></a>术语  
 Add-in — 外接程序  
 实用程序应用程序、 驱动程序或添加到主应用程序的其他软件。 在 Visual Studio 集成的开发环境 (IDE) 中外, 接程序是扩展的功能的 IDE 的自动化基于应用程序。  
  
 自动化模型  
 自动化模型，在以前版本的 Visual Studio 扩展性模型，已知是为您提供了一个编程接口访问的基础例程该驱动器的 IDE。 外接程序、 向导和宏使用自动化模型来控制中的对象或扩展 IDE 的功能。  
  
 命令 UI 上下文  
 与 UI 命令或工具栏等元素的可见性的一个 GUID 关联。 命令 UI 上下文是与选定内容上下文不同，因为它未附加到窗口。  
  
 命令 UI 上下文可用于：  
  
- 将 GUID 分配给特定窗口被激活时，将显示一个工具栏。  
  
- 将 GUID 分配给命令的可用性，而无需加载或运行 VSPackage。  
  
- 将分配一个 GUID 以影响活动的键绑定。  
  
- 将分配一个 GUID 以开启宏录制。  
  
- 将分配一个 GUID 以激活调试模式或设计和在编辑器中的运行的模式之间进行切换。  
  
  组件  
  一种软件，可以不具有任何预先存在相关信息的软件实现该应用程序建立应用程序的功能的一部分。 组件和应用程序之间的通信是仅通过 OLE 风格的接口。  
  
  组件管理器  
  一个服务， `SOleComponentManager`，它提供非用户界面协调服务顶级组件。 `SOleComponentManager`服务实现`IOleComponentManager`接口。  
  
  组件 UI 管理器  
  一个服务， `SOleComponentUIManager`，提供用户界面协调服务。 `SOleComponentUIManager`服务实现`IOleComponentUIManager`和`IOleInPlaceComponentUIManager`接口。  
  
  上下文包  
  `IVsUserContext`对象 （COM 对象） 附加到环境组件。 此对象包含查找关键字、 F1 关键字和相关组件的属性。 上下文包此外指向链接到其任何子上下文包。  
  
  上下文提供程序  
  具有与之关联的上下文包在 IDE 中的组件。 此类组件包括工具窗口、 编辑器或项目层次结构。  
  
  设计器  
  一个编程接口，允许用户操作 UI （窗体、 按钮和其他控件） 的元素。  
  
  DocData  
  封装一个世界中的文档的基础数据的 COM 对象没有文档/视图分离 （例如，在文本编辑器的情况下，这会基础文本编辑器的所有视图的文本缓冲区）。 如果 EditorFactory 不提供此对象，IDE 将制造一个代表其自身。 此对象的责任是管理数据暂留和多个共享的语义视图通过此相同`DocData`。 如果`DocData`对象支持`IOleCommandTarget`接口，它将包含在 UIShell 命令路由。  
  
  DocObject  
  用来承载在宿主所提供的范围内的用户界面技术。 具体而言，此术语指支持任何嵌入`IOleDocument`和相关的接口。 此技术有许多潜在应用程序，例如 COM 文档的实现细节，在 Visual Basic 5.0 中的工具窗口、 ActiveX 设计器在 Visual Basic 6.0 中，依次类推。  
  
  文档  
  用来泛指文档作为一个整体，同时`DocData`和`DocView`。 例如，包含 DocumentFrame `DocView`，，但它还会保留对引用`DocData`处理持久性。  
  
  DocView  
  在用户查看和操作基础交互 DocObject/嵌入/名称`DocData`。 请注意，用户不需要利用一部分的文档/视图分离`DocObject`接口设计。 用户使用整个 DocObject 充当一个视图，而不是使用更抽象 （和不太正式化） 的这一概念的基础数据称为`DocData`。 `DocView` 始终与文档框架对象 （MDI 子窗口） 的 IDE 嵌入对象。  
  
  DTE  
  `DTE` （开发工具扩展性） 对象是在 Visual Studio 自动化模型中，允许您以编程方式自动执行和扩展 IDE 的最顶层的访问点。  
  
  “动态帮助”窗口   
  工具窗口，通过 IDE 实现，并显示查找关键字或 F1 帮助主题的列表。  
  
  编辑器  
  实现的代码 （类，CLSID） `DocView`。 它还实现`DocData`如果受支持的视图/数据分离。  
  
  扩展  
  修改、 自定义，或将添加到 IDE 的功能。 创建使用自动化模型或 Vspackage 扩展。  
  
  外部编辑器  
  一种编辑器，并不特定于 IDE 中，如 Microsoft Word。 它通过其自己的机制已注册，并可以在 IDE 外部使用。 如果可以嵌入此编辑器，它将显示在 IDE 中窗口。 如果它不能嵌入，将创建一个单独的顶级窗口。  
  
  层次结构  
  为节点树，与一组属性相关联的每个节点。  
  
  独立的顶级组件  
  使用无模式的顶级窗口和作为独立应用程序窗口中，可以有效地运行，但实现为进程内对象的组件。 因此，独立的顶级组件必须协调模式和消息循环与 IDE 的服务。 进程内的对象不具有其自己的消息循环。  
  
  信息提供程序  
  信息提供程序是一个模块，可以查找关键字并返回的窗体中的主题，列表`IVsUserContextItem`对象。 若要为信息提供程序提供 F1 和查找关键字项，请注册已编译的帮助文件 (。HxS) 与系统。 这些文件中的帮助主题用于提供显示在动态帮助窗口中，并显示是否在用户按 F1 的主题的列表。  
  
  就地组件  
  实现的 VSPackage 对象`IOleInPlaceComponent`接口来管理以可视方式包含在归 IDE 的文档窗口的窗口。 就地组件不参与标准 OLE 菜单合并;而是他们将其用户界面元素集成到 IDE。  
  
  有两种类型的就地组件： 硬编码的就地组件和组件控件。  
  
  硬编码的就地组件有菜单、 工具栏和紧密集成到 IDE 中，显示为如果它们已直接内置于 IDE 的用户界面的命令。  
  
  组件控件不具有任何集成到 IDE; 其自身用户界面元素相反，它们使用 IDE 的菜单、 命令和工具栏。 例如，粗体命令无法用于在窗体中嵌入的富文本控件中的选定的文字设置为粗体。 但是，组件控件可以请求显示动态安装特定于组件的 UI 元素。  
  
  语言服务  
  允许 VSPackage 开发人员实现功能的计算机语言代码编辑器，例如，文本将标记和着色的对象集。  
  
  杂项文件项目  
  用于内部打开文件不在任何项目中的项目。 此项目中的项列表不会保留。  
  
  项目  
  项目组成层次结构对象或 COM 对象实现`IVsHierarchy`接口。  
  
  特定于项目的设计器或编辑器  
  不能独立于项目类型使用设计器。 所有特定于项目的设计器必须在注册表中输入其编辑器工厂的信息。 IDE 然后可以实例化设计器时，只要在特定项目中打开特定文件类型。  
  
  项目类型窗口  
  从全局选定内容上下文会持续跟踪的当前处于活动状态的项目层次结构和项的窗口。 项目类型 windows 使用`SVsTrackSelectionEx`服务发出警报的更改的 IDE，并能够将反馈显示给用户。 解决方案资源管理器是一个项目类型窗口的示例。  
  
  “属性”窗口  
  以前称为属性浏览器。  
  
  基于引用的项目  
  不需要为位于相同的目录中的项目文件的项目。 相反，对文件来自其他不相关的目录的引用存储和维护项目本身。  
  
  运行文档表  
  按其在 IDE 维护的所有当前打开的文档列表的内部结构。 此列表包括所有打开的文档在内存中而不考虑是否当前正在编辑的文档。 文档是包括在编辑器中，项目中的文件或主项目文件 （例如，*.vcproj 文件） 中打开的存储的过程的保存的任何项。  
  
  选定内容上下文  
  是在 IDE 中的每个窗口的详细信息的一部分，用于跟踪活动选择的数据。 选定内容上下文包括：  
  
- 指向`IVsHierarchy`项目层次结构的接口  
  
- 项目项的项标识符。  
  
- 指向`ISelectionContainer`用于访问属性的活动对象的接口。  
  
- 元素值的数组。  
  
  服务  
  一组 COM 接口驻留在单个的 COM 对象中的一个协定。 时创建一个服务，它由 GUID 标识，定义执行该服务的 COM 接口集。 COM 对象使用服务相互通信。  
  
  解决方案  
  组的用户的工作的相关项目。  
  
  标准设计器  
  一个设计器，可以使用独立于项目类型。 所有标准的设计器必须在注册表中输入其编辑器工厂的信息。 IDE 然后可以实例化设计器每次打开具有特定扩展名的文件。 数据必须保存到文件。  
  
  标准编辑器  
  可以使用独立于任何特定项目类型的编辑器。 此类编辑器都有 EditorFactories 在注册表中注册。 这使 IDE，可查找并调用编辑器。  
  
  标准 OS 编辑器  
  嵌入不是 Visual Studio 特定。 注册使用已知的 Win32 键 （例如，Win32 资源管理器知道如何调用）。 如果可以嵌入此类编辑器，在编辑器仍会出现在 IDE 中其原位置。 否则，为此类编辑器创建一个单独的顶级窗口。  
  
  子上下文包  
  `IVsUserContext`对象链接到上下文包。 此对象包含查找关键字、 F1 关键字和选择的 IDE 组件中的属性。 子上下文的示例包括一个命令中的工具窗口中或在编辑器中的关键字。  
  
  任务列表  
  工具窗口，通过 IDE 实现，并显示活动任务的列表。  
  
  文本缓冲区  
  对象的公用名`VSTextBuffer`。  
  
  文本视图  
  对象的公用名`VSTextView`。  
  
  工具顶级组件  
  作为无模式弹出窗口中，使用 IDE 的用户界面紧密协调运行一个组件。 独立的顶级组件一样工具顶级组件还必须协调模式和消息循环与 IDE 的服务。  
  
  顶级组件  
  VSPackage 对象，用于管理无模式的顶层窗口，而不是一个 IDE 窗口的工作区。 顶级组件实现`IOleComponent`接口以利用空闲时间的消息循环服务，例如访问。  
  
  UI 活动  
  VSPackage 对象是可见且当前具有焦点。  
  
  UI 层次结构  
  实现的 COM 对象`IVsUIHierarchy`接口以允许显示的层次结构。 UI 层次结构窗口实现`ISelectionContainer`接口更新属性窗口; 其他项目类型窗口可以使用此实现中，如果所需的。  
  
  VSCT  
  Visual Studio 命令表。 .Vsct 文件包含有关布局和菜单、 工具栏和 XML 格式中的命令的行为的信息。  
  
  VSPackage  
  通过参与一个或多个以下扩展 Visual Studio IDE 的软件可安装部分： 用户界面、 服务、 项目类型或编辑器/设计器。 VSPackage 包含实现的 COM 对象`IVsPackage`接口和一个或多个其他 COM 对象实现其他接口以支持所选内容和其他功能。 此外，VSPackage 还具有特定的注册要求。
