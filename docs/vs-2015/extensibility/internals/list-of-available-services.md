---
title: 可用服务列表 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- services, Visual Studio
- Visual Studio, services
ms.assetid: 724eb24b-b87c-4971-a2e7-adee7afc03b2
caps.latest.revision: 50
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d67d0300d99cf43165446458414cc2244c6ede0c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203818"
---
# <a name="list-of-available-services"></a>可用服务的列表
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] 和 Visual Studio SDK 支持以下服务。 某些程序包提供其自己的服务未在此处列出的 — 例如，语言服务不具有单个服务的 GUID。 必须使用的语言名称以在注册表中找到的语言服务的 GUID。  
  
 使用服务 Guid 此处列出或获取来自其他源 （例如，语言服务） 来获取的主要接口或基接口与每个服务所示。  
  
## <a name="the-services"></a>服务  
  
|服务|接口|Visual Studio|Visual Studio 2005|描述|  
|-------------|---------------|-------------------|------------------------|-----------------|  
|<xref:Microsoft.VisualStudio.OLE.Interop.SBindHost>|<xref:Microsoft.VisualStudio.OLE.Interop.IBindHost>|是|是|使用 Vspackage 获取<xref:Microsoft.VisualStudio.OLE.Interop.IBindHost>ActiveX 控件以便于异步数据传输中的接口。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SDTE>|<xref:EnvDTE.DTE>|No|是|获取用于自动化的设计时可扩展性 (DTE) 对象。<br /><br /> C /C++ ID:SID_SDTE|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SCodeNavigate>|<xref:Microsoft.VisualStudio.Shell.Interop.ICodeNavigate>|是|是|由窗体设计器以显示控件的默认事件处理程序实现。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.SContainerDispatch>|IDispatch|是|是|允许 VSPackage 来访问另一个 VSPackage 或控件的自动化接口。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SExtendedTypeLib>|<xref:Microsoft.VisualStudio.Shell.Interop.IExtendedTypeLib>|是|是|允许 VSPackage 来添加或创建一个扩展的类型库。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SDirList>|<xref:Microsoft.VisualStudio.Shell.Interop.IDirList>|No|是|提供对容器的访问的名为列表的列表;例如，要搜索中所示的目录的列表**查找和替换**对话框中的**查找范围**下拉列表。 <xref:Microsoft.VisualStudio.Shell.Interop.IDirList>对象可以是从读取以及写入。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SIVsPackageDynamicToolOwner>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackageDynamicToolOwner>|是|是|使 VSPackage 能够动态显示或隐藏其自身工具窗口。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SLicensedClassManager>|<xref:Microsoft.VisualStudio.Shell.Interop.ILicensedClassManager>|是|是|允许 VSPackage 以指示[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]它需要通过指定的许可证密钥列表的类。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SLocalRegistry>|<xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2>|是|是|允许 VSPackage 访问相对于本地注册表[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]注册表配置单元。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.SOleComponentManager>|<xref:Microsoft.VisualStudio.OLE.Interop.IOleComponentManager>|是|是|提供组件协调服务，例如消息循环、 键盘循环和事件通知。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SOleComponentUIManager>|<xref:Microsoft.VisualStudio.Shell.Interop.IOleComponentUIManager>|是|是|允许 VSPackage 访问的各种用户界面 (UI) 元素[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]，如帮助、 状态栏和 UI 事件。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponent>|<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponent>|是|是|可以将其 UI 的 UI 的 VSPackage [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SOleInPlaceComponentSite>|<xref:Microsoft.VisualStudio.Shell.Interop.IOleInPlaceComponentSite>|是|是|允许 VSPackage 来控制特定于工具的 UI 更改。|  
|<xref:Microsoft.VisualStudio.OLE.Interop.SOleUndoManager>|<xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager>|是|是|允许 VSPackage 访问容器的撤消管理器或者参与该容器的撤消堆栈或访问该容器的撤消堆栈。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SProfferService>|<xref:Microsoft.VisualStudio.Shell.Interop.IProfferService>|是|是|允许 VSPackage 以提供其自己的服务。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SProfferTypeLib>|<xref:Microsoft.VisualStudio.Shell.Interop.IProfferTypeLib>|是|是|启用窗体设计器，以便可以引用类型库。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>|<xref:Microsoft.VisualStudio.Shell.Interop.ITrackSelection>|是|是|提供访问权限的选择容器中的选项。 由窗体设计器。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SUIHostCommandDispatcher>|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|是|是|启用命令处理程序链中参与，处理代表集成的开发环境 (IDE) 或自身的命令的 VSPackage。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SUIHostLocale>|<xref:Microsoft.VisualStudio.Shell.Interop.IUIHostLocale>|是|是|提供对主机的 UI 区域设置信息的访问。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>|No|是|启用日志记录打开时记录高级消息的 VSPackage。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsAddProjectItemDlg>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsAddProjectItemDlg>|是|是|提供对访问**添加项目项**对话框，允许 Vspackage 实现其自己**添加项**菜单选项。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsAddWebReferenceDlg>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsAddWebReferenceDlg>|是|是|显示**添加引用**对话框。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsAppCommandLine>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsAppCommandLine>|是|是|允许 VSPackage 来确定是否命令行开关提供给 devenv.exe。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsCallBrowser>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCallBrowser>|No|是|允许创建新的 VSPackage**调用浏览器**在调试时使用。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsClassView>|是|是|允许 VSPackage 来同步**类视图**到特定对象。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsCmdNameMapping>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCmdNameMapping>|是|是|映射到 Guid 并返回命令名称并确定所有可用命令和名称的名称提供支持。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeDefView>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeDefView>|No|是|启用操作的 VSPackage**代码定义视图**。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsCodeShareHandler>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCodeShareHandler>|是|是|内部服务。 请勿使用。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindow>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|是|是|提供对可以包含一个或多个文档的代码窗口访问。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.SVsCodeWindowManager>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindowManager>|是|是|允许 VSPackage 来将更改添加到代码窗口下拉栏等。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindow>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindow2>|是|是|可以运行命令的 VSPackage**命令窗口**并与之否则交互**命令窗口**。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsCommandWindowsCollection>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCommandWindowsCollection>|No|是|允许 VSPackage 来操作的列表**命令**由 windows 维护[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsComplusLibrary>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsLibraryReferenceManager>|是|是|允许 VSPackage 来浏览信息提供给**对象浏览器**。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg>|No|是|启用以支持的 VSPackage**添加引用**选项，让用户选择要添加到项目的外部组件。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsComponentSelectorDlg2>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsComponentSelectorDlg2>|No|是|启用以支持的 VSPackage**添加引用**选项，让用户选择要添加到项目的外部组件。 在显示之前，此版本对话框的允许预填充的组件列表。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsConfigurationManagerDlg>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsConfigurationManagerDlg>|No|是|显示**Configuration Manager**对话框。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsCreateAggregateProject>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCreateAggregateProject>|No|是|允许 VSPackage 来创建包含一系列的其他项目的项目。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsDebuggableProtocol>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProtocol>|是|是|允许 VSPackage 来更新的可调试 IDE 用于启动特定的调试引擎的协议列表。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsDebugLaunch>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugLaunch>|是|是|允许 VSPackage 来支持启动调试器。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsDiscoveryService>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDiscoveryService>|是|是|允许 VSPackage 创建发现会话，用来发现 Web 服务。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsEnumHierarchyItemsFactory>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory>|是|是|提供了一个工厂来创建<xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumHierarchyItemsFactory>对象用于枚举指定层次结构 （项目）。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsErrorList>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsErrorList>|No|是|提供用于操作的其他方法**生成错误列表**任务窗口。 具体而言，带来**生成错误列表**排在任务窗口，并强制显示所有错误。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsExternalFilesManager>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsExternalFilesManager>|是|是|提供对访问**杂项文件**当前解决方案的项目节点。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChange>||是|是|已过时。 使用`SVsFileChangeEx`改为服务。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx>|是|是|允许 VSPackage 访问由 IDE 触发的各种文件更改事件。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterAddProjectItemDlg>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg>|是|是|使 VSPackage 能够筛选器中显示的项**添加项**对话框。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFilterKeys>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterKeys>|是|是|允许 VSPackage 来执行高级的键盘筛选。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorCacheManager>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager>|No|是|字体提供对缓存中的组访问和中的颜色[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]刷新或清除某个特定缓存或所有缓存。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFontAndColorStorage>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorUtilities>|是|是|允许 VSPackage 处理维护的字体和颜色设置[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 此外，此服务提供的实用工具方法，用于操作字体和颜色数据集合的访问权限。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>|是|是|提供对常规访问权限**输出窗口**窗格中，根据需要创建它。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsHelpService>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHelpSystem>|是|是|提供访问权限的帮助系统。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsHTMLConverter>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHTMLConverter>|是|是|由[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]调试器要设置其输出格式的 HTML 句柄。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsIME>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsIME>|是|是|为输入方法编辑器 (IME) 中的 API 在 VSPackage 中提供的访问。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsIntegratedHelp>|<xref:Microsoft.VisualStudio.VSHelp.SVsHelp>|是|是|提供对访问[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]帮助系统的关键字或 URL 访问和导航控制通过帮助文件。 该服务可帮助集成到才[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE 和作为外部程序未运行。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsIntelliMouseHandler>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntelliMouseHandler>|是|是|允许 VSPackage 访问等使用鼠标滚轮单击鼠标滚轮时处理滚动和平移位图的缩放功能。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseEngine>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseEngine>|No|是|使项目层次结构节点来加载或卸载文件作为 IntelliSense 操作支持的一部分。 加载和卸载可能会影响项目的 IntelliSense 工具提示中显示的内容的触发器事件的过程。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectHost>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectHost>|No|是|使项目层次结构节点提供有关嵌套 IntelliSense 项目的信息 (实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>接口)，可以显示在 IntelliSense 工具提示。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsIntellisenseProjectManager>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProjectManager>|No|是|使项目层次结构节点向建议侦听器的事件，例如更改引用或配置，这可能会影响 IntelliSense 工具提示中显示的内容。 设计与包含语言一起使用。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsInvisibleEditorManager>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsInvisibleEditorManager>|是|是|允许 VSPackage 注册不可见编辑器，也就是说，一种编辑器，提供完整的编辑功能，但不是对用户可见。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.SVsLanguageFilter>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewFilter>|是|是|允许 VSPackage 以提供其他信息，如数据提示文本视图和单词的程度。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPad>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad>|是|是|允许 VSPackage 来执行临时批处理脚本，执行其输出发送到输出窗格中，一个命令行程序并进行分析标准警告和错误消息发送到一个错误窗口。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsLaunchPadFactory>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPadFactory>|是|是|提供用于创建一个工厂<xref:Microsoft.VisualStudio.Shell.Interop.IVsLaunchPad>对象。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.SVsLinkedUndoTransactionManager>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoTransactionManager>|是|是|提供对链接的撤消管理器访问。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsMenuEditor>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditorFactory>|是|是|使窗体设计器来访问共享的菜单编辑器。 可以为查询 IVsMenuEditorFactory <xref:Microsoft.VisualStudio.Shell.Interop.IVsMenuEditor>。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsMonitorUserContext>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorUserContext>|是|是|允许 VSPackage 来创建"上下文包"，用于将相关联的特定上下文的帮助关键字。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjBrowser>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjBrowser>|是|是|启用导航到中的特定对象的 VSPackage**对象浏览器**。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectManager>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectManager>|是|是|允许 VSPackage 来使用其库管理器中注册[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]用于管理命名空间、 类和枚举等对象。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsObjectSearch>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsObjectSearch>|是|是|允许 VSPackage 来搜索特定对象。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsOpenProjectOrSolutionDlg>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOpenProjectOrSolutionDlg>|No|是|允许 VSPackage 来使用标准[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]对话框以打开项目或解决方案。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>|是|是|可以在常规输出窗口中创建附加输出窗格的 VSPackage。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsParseCommandLine>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsParseCommandLine>|是|是|启用的实现器<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口来分析命令行。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsPathVariableResolver>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPathVariableResolver>|No|是|提供方法来解决这些变量特定于[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]和嵌入在路径以生成最终的路径。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsPreviewChangesService>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPreviewChangesService>|No|是|显示**预览更改**重构代码中使用的对话框。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsProfileDataManager>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProfileDataManager>|No|是|提供访问权限的配置文件管理器[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]允许导入和导出设置数据，以及显示当前用户的配置文件设置的 UI。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsProfilesManagerUI>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProfilesManagerUI>|No|是|显示一个对话框，其中显示当前用户的配置文件设置。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsPropertyPageFrame>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPropertyPageFrame>|是|是|允许重写在最初显示的属性页的 VSPackage**属性**窗口。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>|No|是|由 Vspackage 来通知文件是要在内存中更改或保存源代码管理提供程序。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterDebugTargetProvider>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectDebugTargetProvider>|No|是|允许 VSPackage 项目，以编程方式重写要在调试器中启动的目标。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterEditors>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterEditors>|是|是|允许 VSPackage 来向 IDE 注册一个编辑器工厂。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.SVsRegisterFindScope>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsRegisterFindScope>|No|是|允许 VSPackage 注册为搜索范围**在文件中查找**对话框。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterPriorityCommandTarget>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterPriorityCommandTarget>|是|是|可以将自身注册为高优先级命令处理程序，它允许 VSPackage，若要查看所有命令的 VSPackage。 请慎用，根本。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsRegisterProjectTypes>|是|是|允许 VSPackage 来向 IDE 注册项目类型。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceManager>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceManager>|No|是|允许 VSPackage 来从附属 Dll 加载托管和非托管资源。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsResourceView>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsResourceView>|是|是|使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsClassView>改为服务。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable>|是|是|提供了访问到 IDE 的正在运行文档表 (RDT)，用于跟踪所有当前打开的文档。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>|No|是|允许 Vspackage 自行注册到源代码管理提供程序使它们可以参与源代码管理中。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccToolsOptions>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccToolsOptions>|是|是|允许 VSPackage 获取和设置源代码管理提供程序选项。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSettingsReader>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsReader>|No|是|提供对用户的配置文件设置读取访问权限。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShell>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsShell>|是|是|允许 VSPackage 来直接交互和处理其他 Vspackage。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebugger>|是|是|提供对访问[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]调试器。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection>|是|是|允许 VSPackage 访问当前所选内容和管理命令 UI 上下文。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVSMDCodeDomProvider>|IVSMDCodeDomProvider|No|是|提供对代码文档对象模型 (DOM) 提供程序可在本机代码中访问。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVSMDDesignerService>|IVSMDCodeDomCreator<br /><br /> IVSMDDesignerService|No|是|对于托管窗体设计器提供对 IDE 的支持访问。 `IVSMDCodeDomCreator`可用于创建 DOM 提供程序的代码。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVSMDPropertyBrowser>|IVSMDPropertyBrowser|No|是|提供对设计器属性 windows 服务的访问。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVSMDTypeResolutionService>|<xref:Microsoft.VisualStudio.Shell.Interop.IVSMDTypeResolutionService>|No|是|提供一个接口，可以返回到访问<xref:System.ComponentModel.Design.ITypeResolutionService>易于在本机代码中使用的对象。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSmartOpenScope>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSmartOpenScope>|No|是|提供了一种方法，以打开程序集，并考虑锁定根据需要在作用域。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution>|是|是|提供对当前解决方案的顶级访问。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionBuildManager>|是|是|使 VSPackage 能够与解决方案的生成过程进行交互。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionObject>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution>|是|是|使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>改为服务。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionPersistence>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionPersistence>|是|是|允许 VSPackage 来存储和从当前解决方案的.sln 文件中检索信息。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSQLCLRReferences>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSQLCLRReferences>|No|是|提供的功能添加和更新中托管的代码程序集的引用。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStartPageDownload>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStartPageDownload>|No|是|提供用于启动和停止下载服务在后台线程上的启动页下载服务的访问权限。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbar>|是|是|提供对 IDE 的状态栏的访问。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStrongNameKeys>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStrongNameKeys>|No|是|提供用于创建强密钥名称和密钥文件包含对托管的代码程序集签名中使用的密码的方法的访问权限。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStructuredFileIO>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStructuredFileIO>|是|是|允许 VSPackage 以提供有关将数据保存在多个格式的支持。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTaskList>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTaskList>|是|是|IDE 的任务列表窗口中提供的访问。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextImageUtilities>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextImageUtilities>|No|是|提供用于加载和保存文本文件的实用程序。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextManager>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextManager><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextManager>|是|是|提供对所有文本缓冲区，以及可在 IDE 中的隐藏的文本，会话 （适用于的隐藏区域） 的访问。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTextOut>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTextOut>|是|是|提供的 Win32 版本`TextOut`函数用于将文本写入设备上下文 （需要 DC 句柄）。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.SVsTextSpanSet>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextSpanSet>|是|是|提供访问权限的文本图像或缓冲区中的文本范围的列表。 此服务通常实现上文档的一个容器，并引用当前文档。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadedWaitDialog>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadedWaitDialog>|No|是|允许 VSPackage 来显示一个对话框，在不同的线程 （后台任务正在等待用于） 上等待。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsThreadPool>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsThreadPool>|No|是|允许 VSPackage 来启动后台任务，然后由维护[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsToolbox>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolbox>|是|是|提供对 IDE 的访问权限**工具箱**。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxActiveXDataProvider>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProvider>|是|是|启用以获取信息的 VSPackage**工具箱**项。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsToolboxDataProviderRegistry>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxDataProviderRegistry>|No|是|允许 VSPackage 注册工具箱数据提供程序而不会产生性能成本的预加载整个**工具箱**。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsToolsOptions>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolsOptions>|No|是|允许 VSPackage 来判断**选项**对话框处于打开状态，并可刷新所有选项页的可见性。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments3>|No|是|允许 VSPackage 来监视项目的文件中的更改并提供对源代码管理提供程序的批处理控制。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackSelectionEx>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackSelectionEx>|是|是|允许 VSPackage 通知可能会影响当前选定的项目项的选择内容更改的 IDE。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelper>|是|是|使层次结构 （如 VSPackage 项目） 来协调与其他层次结构将剪贴板中的使用。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell>|是|是|提供对 IDE 的 UI 元素，如工具窗口和文档窗口访问。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellDocumentWindowMgr>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellDocumentWindowMgr>|是|是|允许 VSPackage 还原基于数据的流内容的所有窗口的位置，或者将保存到流的所有窗口的位置。 很少使用。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>|是|是|允许 VSPackage 中通过多种方式打开的文档并确定谁拥有哪个文档。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUpgradeLogger>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUpgradeLogger>|No|是|由实施者的使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectUpgradeViaFactory>报告错误和信息性消息的接口。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsWebBrowsingService>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWebBrowsingService>|是|是|允许 VSPackage 来创建和控制 Web 浏览会话。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsWebFavorites>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWebFavorites>|是|是|启用要添加到用户的 VSPackage**收藏夹**列表。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsWebPreview>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWebPreview>|是|是|允许 VSPackage 预览 Web 页，通常在子窗口。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsWebURLMRU>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWebURLMRU>|是|是|使 VSPackage 可以向 Url 的最近使用过的 (MRU) 列表添加 URL 并获取 MRU 列表中的所有 Url 的列表。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsWindowFrame>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame>|是|是|启用以获取包的一部分的包可能会置于该窗口框架的 VSPackage。|  
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsXMLMemberIndexService>|<xref:Microsoft.VisualStudio.Shell.Interop.IVsXMLMemberIndexService>|是|是|提供对与特定的元数据文件相关联的 XML 格式文档文件的访问。|  
  
## <a name="see-also"></a>请参阅  
 [COM 和托管的服务](/java/api/overview/partnercenter/managedservices?view=partnercenter-1.8.1)   
 [使用并提供服务](../../extensibility/using-and-providing-services.md)
