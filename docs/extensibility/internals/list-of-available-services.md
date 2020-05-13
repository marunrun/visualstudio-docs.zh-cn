---
title: 可用服务列表 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, Visual Studio
- Visual Studio, services
ms.assetid: 724eb24b-b87c-4971-a2e7-adee7afc03b2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 302d4bcff647a74acc973c47e0b62e66c86e5859
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707347"
---
# <a name="list-of-available-services"></a>可用服务的列表

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]Visual Studio SDK 支持以下服务。 某些包提供此处未列出的服务，例如，语言服务没有单个服务 GUID。 您必须使用语言的名称才能在注册表中找到语言服务的 GUID。

使用此处列出的服务 GUID 或从其他来源（例如语言服务）获取与每个服务显示的主接口或接口。

## <a name="the-services"></a>服务

| 服务 | 接口 | Visual Studio | Visual Studio 2005 | 描述 |
| - | - |---------------|--------------------| - |
| <xref:Microsoft.VisualStudio.OLE.Interop.SBindHost> | <xref:Microsoft.VisualStudio.OLE.Interop.IBindHost> | 是 | 是 | VSPackages 用于从 ActiveX 控件获取<xref:Microsoft.VisualStudio.OLE.Interop.IBindHost>接口，以方便异步数据传输。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDTE> | <xref:EnvDTE.DTE> | 否 | 是 | 获取用于自动化的设计时间扩展 （DTE） 对象。<br /><br /> C/C++ ID：SID_SDTE |
| <xref:Microsoft.VisualStudio.Shell.Interop.SCodeNavigate> | <xref:Microsoft.VisualStudio.Shell.Interop.ICodeNavigate> | 是 | 是 | 由窗体设计器实现，以显示控件的默认事件处理程序。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SContainerDispatch> | IDispatch | 是 | 是 | 使 VSPackage 能够访问另一个 VSPackage 或控件的自动化接口。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SExtendedTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IExtendedTypeLib> | 是 | 是 | 使 VSPackage 能够添加或创建扩展类型库。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SDirList> | <xref:Microsoft.VisualStudio.Shell.Interop.IDirList> | 否 | 是 | 提供对容器命名列表的访问;例如，要搜索的目录列表，如"**查找和替换**"下拉列表中的"**查找**和替换"对话框中所示。 对象<xref:Microsoft.VisualStudio.Shell.Interop.IDirList>可以从读取并写入对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SIVsPackageDynamicToolOwner> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwner> | 是 | 是 | 使 VSPackage 能够动态显示或隐藏自己的工具窗口。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLicensedClassManager> | <xref:Microsoft.VisualStudio.Shell.Interop.ILicensedClassManager> | 是 | 是 | 通过指定许可证密钥列表，使[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]VSPackage 能够向所需的类指示它所需的类型。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> | 是 | 是 | 使 VSPackage 能够访问相对于本地[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]注册表配置单元的注册表。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleComponentManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager> | 是 | 是 | 提供组件协调服务，如消息循环、键盘循环和事件通知。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager> | 是 | 是 | 使 VSPackage 能够访问[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的各种用户界面 （UI） 元素，如帮助、状态栏和 UI 事件。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponent> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent> | 是 | 是 | 使 VS 包将其 UI 与 的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]UI 集成。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponentSite> | <xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentSite> | 是 | 是 | 使 VS 包能够控制特定于工具的 UI 更改。 |
| <xref:Microsoft.VisualStudio.OLE.Interop.SOleUndoManager> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager> | 是 | 是 | 使 VSPackage 能够访问容器的撤消管理器，以参与该容器的撤消堆栈或访问该容器的撤消堆栈。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferService> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferService> | 是 | 是 | 使 VSPackage 能够提供自己的服务。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SProfferTypeLib> | <xref:Microsoft.VisualStudio.Shell.Interop.IProfferTypeLib> | 是 | 是 | 使窗体设计器使类型库可供参考。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection> | 是 | 是 | 提供对选择容器中选择项的访问权限。 由窗体设计器使用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostCommandDispatcher> | <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> | 是 | 是 | 使 VSPackage 能够参与命令处理程序链，并代表集成开发环境 （IDE） 或本身处理命令。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SUIHostLocale> | <xref:Microsoft.VisualStudio.Shell.Interop.IUIHostLocale> | 是 | 是 | 提供对主机的 UI 区域设置信息的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> | 否 | 是 | 启用 VSPackage 可在启用日志记录时记录高级消息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg> | 是 | 是 | 提供对 **"添加项目项**"对话框的访问，允许 VS 包实现其自己的 **"添加项目"** 菜单选项。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAddWebReferenceDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg> | 是 | 是 | 显示"**添加参考"** 对话框。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine> | 是 | 是 | 启用 VSPackage 以确定是否将命令行开关提供给 devenv.exe。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCallBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCallBrowser> | 否 | 是 | 使 VSPackage 能够创建新的**调用浏览器**，用于调试。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsClassView> | 是 | 是 | 使 VS 包能够将**类视图**同步到特定对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCmdNameMapping> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCmdNameMapping> | 是 | 是 | 支持将命令名称映射到 GUID 并返回并确定所有可用命令和名称的名称。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeDefView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeDefView> | 否 | 是 | 使 VS 包能够操作**代码定义视图**。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeShareHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeShareHandler> | 是 | 是 | 内部服务。 请勿使用。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindow> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> | 是 | 是 | 提供对可以包含一个或多个文档的代码窗口的访问。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindowManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager> | 是 | 是 | 使 VSPackage 向代码窗口（如下拉栏）添加更改。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow2> | 是 | 是 | 使 VSPackage 通过**命令窗口**运行命令，然后以其他方式与**命令窗口**进行交互。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindowsCollection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindowsCollection> | 否 | 是 | 使 VSPackage 能够操作 由**Command**[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]维护的命令窗口的列表。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComplusLibrary> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLibraryReferenceManager> | 是 | 是 | 使 VS 包向**对象浏览器**提供浏览信息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg> | 否 | 是 | 使 VSPackage 支持**添加引用**选项，该选项允许用户选择要添加到项目的外部组件。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg2> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg2> | 否 | 是 | 使 VSPackage 支持**添加引用**选项，该选项允许用户选择要添加到项目的外部组件。 此版本的对话框允许在显示组件列表之前预填充组件列表。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsConfigurationManagerDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsConfigurationManagerDlg> | 否 | 是 | 显示 **"配置管理器**"对话框。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject> | 否 | 是 | 使 VSPackage 能够创建包含其他项目集合的项目。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebuggableProtocol> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProtocol> | 是 | 是 | 使 VSPackage 能够更新 IDE 用于启动特定调试引擎的可调试协议列表。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDebugLaunch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugLaunch> | 是 | 是 | 使 VS 包支持启动调试器。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsDiscoveryService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDiscoveryService> | 是 | 是 | 使 VSPackage 创建用于发现 Web 服务的发现会话。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsEnumHierarchyItemsFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory> | 是 | 是 | 提供用于创建<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory>用于枚举指定层次结构（项目）的对象的工厂。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsErrorList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsErrorList> | 否 | 是 | 提供了用于操作**生成错误列表**任务窗口的其他方法。 具体而言，将**生成错误列表**任务窗口置于最前沿，并强制显示所有错误。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager> | 是 | 是 | 提供对当前解决方案**的杂项文件**项目节点的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChange> | | 是 | 是 | 已过时。 而是`SVsFileChangeEx`使用服务。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx> | 是 | 是 | 使 VSPackage 能够访问由 IDE 触发的各种文件更改事件。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterAddProjectItemDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> | 是 | 是 | 使 VSPackage 能够筛选"**添加项目**"对话框中显示的项目。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterKeys> | 是 | 是 | 使 VSPackage 能够执行高级键盘筛选。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorCacheManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> | 否 | 是 | 提供对字体[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和颜色的缓存集的访问，以刷新或清除特定缓存或所有缓存。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorStorage> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorUtilities> | 是 | 是 | 使 VSPackage 能够操作 维护的[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]字体和颜色设置。 此外，此服务还提供对用于操作字体和颜色数据的实用程序方法集合的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> | 是 | 是 | 提供对常规**输出窗口**窗格的访问，根据需要创建它。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHelpService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHelpSystem> | 是 | 是 | 提供对帮助系统的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsHTMLConverter> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsHTMLConverter> | 是 | 是 | [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]调试器用于处理 HTML 以格式化其输出。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIME> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIME> | 是 | 是 | 从 VS 包中提供对输入方法编辑器 （IME） API 的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntegratedHelp> | <xref:Microsoft.VisualStudio.VSHelp.SVsHelp> | 是 | 是 | 提供对[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]关键字或 URL 访问的帮助系统的访问，以及通过帮助文件的导航控制。 仅当帮助集成到 IDE 而不是作为外部程序运行[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]时，此服务才可用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntelliMouseHandler> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntelliMouseHandler> | 是 | 是 | 使 VSPackage 能够访问 IntelliMouse 功能，例如使用鼠标滚轮，并在单击鼠标滚轮时处理滚动和平移位图。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseEngine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseEngine> | 否 | 是 | 使项目层次结构节点能够加载或卸载文件，作为支持 IntelliSense 操作的一部分。 加载和卸载过程触发可能影响 IntelliSense 工具提示中显示的事件。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectHost> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectHost> | 否 | 是 | 使项目层次结构节点能够提供有关嵌套 IntelliSense 项目（实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>接口）的信息，这些项目可以显示在 IntelliSense 工具提示中。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectManager> | 否 | 是 | 使项目层次结构节点能够通知侦听器事件，例如引用或配置的更改，这可能会影响 IntelliSense 工具提示中显示的内容。 设计用于包含语言。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsInvisibleEditorManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager> | 是 | 是 | 使 VSPackage 能够注册"不可见"编辑器，即提供完全编辑功能但用户不可见的编辑器。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLanguageFilter> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter> | 是 | 是 | 使 VSPackage 能够向文本视图提供其他信息，如数据提示和单词范围。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPad> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad> | 是 | 是 | 使 VSPackage 能够执行临时批处理脚本，执行其输出发送到输出窗格的命令行程序，并分析发送到错误窗口的标准警告和错误消息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPadFactory> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPadFactory> | 是 | 是 | 提供用于创建<xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad>对象的工厂。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsLinkedUndoTransactionManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager> | 是 | 是 | 提供对链接撤消管理器的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMenuEditor> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditorFactory> | 是 | 是 | 使窗体设计器可以访问共享菜单编辑器。 可以查询 IVMenu 编辑器工厂<xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditor>。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext> | 是 | 是 | 使 VSPackage 能够创建"上下文包"，用于关联特定上下文的帮助关键字。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjBrowser> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjBrowser> | 是 | 是 | 使 VS 包导航到**对象浏览器**中的特定对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager> | 是 | 是 | 使 VSPackage 将其库管理器注册用于[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]管理命名空间、类和枚举等对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectSearch> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectSearch> | 是 | 是 | 使 VS 包能够搜索特定对象。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOpenProjectOrSolutionDlg> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOpenProjectOrSolutionDlg> | 否 | 是 | 使 VSPackage 能够使用标准[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]对话框打开项目或解决方案。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> | 是 | 是 | 使 VSPackage 能够在常规输出窗口中创建其他输出窗格。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsParseCommandLine> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsParseCommandLine> | 是 | 是 | 使接口的<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>实现者能够解析命令行。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPathVariableResolver> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPathVariableResolver> | 否 | 是 | 提供了一种解决特定于[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的变量的方法，这些变量嵌入到路径中以生成最终路径。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPreviewChangesService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPreviewChangesService> | 否 | 是 | 显示重构代码中使用的 **"预览更改"** 对话框。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfileDataManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfileDataManager> | 否 | 是 | 提供对配置文件[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]管理器的访问，该管理器允许导入和导出设置数据，以及显示当前用户的配置文件设置的 UI。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsProfilesManagerUI> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsProfilesManagerUI> | 否 | 是 | 显示显示当前用户的配置文件设置的对话框。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsPropertyPageFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPageFrame> | 是 | 是 | 使 VSPackage 能够覆盖属性页最初显示在 **"属性"** 窗口中。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2> | 否 | 是 | VSPackages 用于通知源代码管理提供程序文件即将在内存中更改或保存。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterDebugTargetProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectDebugTargetProvider> | 否 | 是 | 使 VSPackage 项目能够以编程方式覆盖目标，以在调试器中启动。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors> | 是 | 是 | 使 VSPackage 向 IDE 注册编辑器工厂。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsRegisterFindScope> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsRegisterFindScope> | 否 | 是 | 使 VSPackage 注册"**在文件中查找**"对话框的搜索范围。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterPriorityCommandTarget> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget> | 是 | 是 | 使 VSPackage 能够将自己注册为高优先级命令处理程序，这允许 VSPackage 查看所有命令。 请谨慎使用（如果有的话）。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes> | 是 | 是 | 使 VS 包能够向 IDE 注册项目类型。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceManager> | 否 | 是 | 使 VSPackage 能够从附属 DLL 加载托管和非托管资源。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceView> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceView> | 是 | 是 | 而是<xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView>使用服务。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable> | 是 | 是 | 提供对 IDE 正在运行的文档表 （RDT） 的访问，该表可跟踪所有当前打开的文档。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2> | 否 | 是 | 使 VSPackages 能够向源代码管理提供程序注册，以便它们能够参与源代码管理。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSccToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions> | 是 | 是 | 使 VSPackage 获取和设置源代码管理提供程序选项。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSettingsReader> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsReader> | 否 | 是 | 提供对用户的配置文件设置的读取访问权限。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsShell> | 是 | 是 | 使 VS 包能够直接与其他 VS 包交互和操作。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger> | 是 | 是 | 提供对调试器[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection> | 是 | 是 | 使 VSPackage 可以访问当前选择并管理命令 UI 上下文。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDCodeDomProvider> | IVSMD代码提供者 | 否 | 是 | 提供对代码文档对象模型 （DOM） 提供程序的访问，该提供程序可在本机代码中使用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDDesignerService> | IVSMD代码创造者<br /><br /> IVSMD设计服务 | 否 | 是 | 提供对托管表单设计器的 IDE 支持的访问。 `IVSMDCodeDomCreator`可用于创建代码 DOM 提供程序。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDPropertyBrowser> | IVSMD属性浏览器 | 否 | 是 | 提供对设计器属性窗口服务的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVSMDTypeResolutionService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVSMDTypeResolutionService> | 否 | 是 | 提供对可以返回本机代码中可使用<xref:System.ComponentModel.Design.ITypeResolutionService>的对象的接口的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSmartOpenScope> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSmartOpenScope> | 否 | 是 | 提供了一种在程序集上打开作用域的方法，并考虑根据需要锁定。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | 是 | 是 | 提供对当前解决方案的顶级访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager> | 是 | 是 | 使 VSPackage 能够与解决方案的生成过程进行交互。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionObject> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution> | 是 | 是 | 改用<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>服务。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionPersistence> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence> | 是 | 是 | 使 VSPackage 能够存储和检索当前解决方案的 .sln 文件中的信息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsSQLCLRReferences> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsSQLCLRReferences> | 否 | 是 | 提供在托管代码程序集中添加和更新引用的能力。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStartPageDownload> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStartPageDownload> | 否 | 是 | 提供对 Visual Studio 2017 起始页的下载服务的访问，以便启动和停止后台线程上的下载服务。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar> | 是 | 是 | 提供对 IDE 状态栏的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStrongNameKeys> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStrongNameKeys> | 否 | 是 | 提供对使用用于对托管代码程序集进行签名的密码创建强密钥名称和密钥文件的方法的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsStructuredFileIO> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsStructuredFileIO> | 是 | 是 | 使 VSPackage 能够支持以多种格式保存数据。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList> | 是 | 是 | 提供访问 IDE 的任务列表窗口。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextImageUtilities> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextImageUtilities> | 否 | 是 | 提供用于加载和保存文本文件的实用程序。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager> | 是 | 是 | 提供对所有文本缓冲区以及 IDE 中可用的隐藏文本会话（对于隐藏区域）的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTextOut> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTextOut> | 是 | 是 | 提供 Win32`TextOut`函数的版本，用于将文本写入设备上下文（需要 DC 句柄）。 |
| <xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextSpanSet> | <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextSpanSet> | 是 | 是 | 提供对文本图像或缓冲区中文本范围列表的访问。 此服务通常在文档容器上实现，并引用当前文档。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadedWaitDialog> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadedWaitDialog> | 否 | 是 | 使 VSPackage 显示在另一个线程上等待的对话框（用于等待后台任务）。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadPool> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadPool> | 否 | 是 | 使 VS 包启动后台任务，然后由[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]维护。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox> | 是 | 是 | 提供对 IDE**工具箱**的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxActiveXDataProvider> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProvider> | 是 | 是 | 使 VSPackage 能够从**工具箱**项目获取信息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxDataProviderRegistry> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProviderRegistry> | 否 | 是 | 使 VSPackage 能够注册工具箱数据提供程序，而不会产生预加载整个**工具箱**的性能成本。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsToolsOptions> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsToolsOptions> | 否 | 是 | 启用 VSPackage 以确定 **"选项"** 对话框是否处于打开状态，并刷新所有选项页的可见性。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3> | 否 | 是 | 使 VSPackage 能够监视项目文件中的更改，并提供对源代码管理提供程序的批处理控制。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx> | 是 | 是 | 使 VSPackage 能够通知 IDE 对选区的更改，这些更改可能会影响当前选定的项目项。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelper> | 是 | 是 | 使层次结构（如项目 VSPackage）能够协调剪贴板与其他层次结构的使用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell> | 是 | 是 | 提供对 IDE 的 UI 元素（如工具窗口和文档窗口）的访问。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellDocumentWindowMgr> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellDocumentWindowMgr> | 是 | 是 | 使 VSPackage 能够根据数据流的内容还原所有窗口的位置，或将所有窗口的位置保存到流中。 很少使用。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument> | 是 | 是 | 使 VSPackage 能够以多种方式打开文档，并确定谁拥有哪些文档。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger> | 否 | 是 | 由<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>接口的实现者用于报告错误和信息消息。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebBrowsingService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebBrowsingService> | 是 | 是 | 使 VS 包能够创建和控制 Web 浏览会话。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebFavorites> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebFavorites> | 是 | 是 | 使 VS 包添加到用户的**收藏夹**列表中。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebPreview> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebPreview> | 是 | 是 | 使 VSPackage 能够预览网页，通常在子窗口中。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWebURLMRU> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWebURLMRU> | 是 | 是 | 使 VSPackage 能够将 URL 添加到最近使用的 URL 列表中，并获取 MRU 列表中所有 URL 的列表。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsWindowFrame> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame> | 是 | 是 | 使 VSPackage 能够获取包或包的一部分可能所在的窗口框架。 |
| <xref:Microsoft.VisualStudio.Shell.Interop.SVsXMLMemberIndexService> | <xref:Microsoft.VisualStudio.Shell.Interop.IVsXMLMemberIndexService> | 是 | 是 | 提供对与特定元数据文件关联的 XML 格式文档文件的访问。 |

## <a name="see-also"></a>请参阅

- [使用并提供服务](../../extensibility/using-and-providing-services.md)
