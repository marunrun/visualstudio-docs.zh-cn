---
title: 项目模型核心组件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project models, objects and interfaces
- project models, services
ms.assetid: b2f572d3-b26d-4846-92d1-84055fac141a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6966f7a0dbde78e996f81adc4d8d8d406489d298
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328388"
---
# <a name="project-model-core-components"></a>项目模型核心组件
下表展开项目模型。 这些表格显示接口和服务模型的接口和与特定对象关联的服务中标识的简短说明。 此外，在表详细介绍在项目的创建和维护，具体取决于特定项目类型的要求中是可选的其他接口。

 有关详细信息，请参阅[支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)。

### <a name="package-object"></a>包对象

|接口|注释|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>|初始化在 IDE 中的 VSPackage 并使其服务可供 IDE。|

### <a name="project-factory-object"></a>项目工厂对象

|接口|注释|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|管理创建新项目和打开现有项目。|

### <a name="project-objects"></a>项目对象

|接口|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>|管理添加和删除项目项，将打开编辑器，并维护每个文档名字对象之间的映射和`VSITEMID`。 继承自`IVsProject`和`IVsProject2`。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|管理导航和显示属性并提供事件。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>|启用命令执行类似于`IOleCommandTarget`只有当焦点位于解决方案资源管理器中应用如剪切和重命名命令。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|充当主命令目标接口的项目层次结构。 它是用于查询其命令的状态或状态和运行命令的对象的标准接口。 在您不想在项目窗口才可用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|协调项目状态的持久性。 通常情况下，项目状态存储为项目文件，但可适用于不是基于文件的存储系统。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>|使项目以管理其项目项，以作为磁盘或其他存储系统中的对象上的文件的持久性的所有方面。 `IVsPersistHierarchyItem2`接口用于未实现的项<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>接口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|协调与源代码管理的交互。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfgProvider>|使项目能够管理配置信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>|管理项目配置对象，例如 Debug/Release 配置。 生成、 部署和调试操作进行协调通过项目配置对象。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler>|实现的层次结构，以控制删除 （破坏性） 或删除的层次结构项的 （非破坏性） 选项。 在调用查询界面`IVsHierarchyDeleteHandler`接口从`IVsHierarchy`接口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsGetCfgProvider>|提供的支持的对象的实现选项`IVsCfgProvider2`接口上实现的项目对象比不同的 COM 标识`IVsHierarchy`接口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectStartupServices>|若要使你的项目扩展由实现其他开发人员的可选接口。 `IVsProjectStartupServices`接口，以注册一个 GUID，以便每次你的项目加载后，您加载到你的项目文件和调用第三方服务 GUID 保存到项目文件的第三方 VSPackage`QueryService`对于该 GUID。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelperEvents>|由源层次结构中实现`UIHierarchy`窗口来协调剪贴板操作，例如剪切、 复制和粘贴。 使用`AdviseClipboardHelperEvents`接口来注册剪贴板事件。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataSource2>|提供有关拖动的项相对于其数据源中的 UI 层次结构窗口拖放操作期间的信息。 从调用`IVsHierarchy`接口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataTarget>|提供有关相对于其拖放目标拖动的项在用户界面层次结构窗口中拖放操作期间的信息。 从调用`IVsHierarchy`接口。|

### <a name="configuration-object"></a>配置对象

|接口|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>|提供有关配置的信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>|使项目能够管理配置信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|使一个项目可以在调试器的控制下运行。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>|通过部署项目执行的其他项目的部署操作的实现。|

### <a name="configuration-builder-object"></a>配置生成器对象

|接口|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>|管理项目配置的生成操作。|

### <a name="additional-project-objects"></a>其他项目对象

|接口|注释|
|----------------|--------------|
|`IDispatch`<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages>|显示项中的属性**属性**窗口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>|显示部署的输出结果。|

 下表列出了项目模型中标识的服务的简短说明。

### <a name="services"></a>Services

|服务|注释|
|-------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes>|由与 IDE 存在其项目工厂实现项目类型，若要注册的 Vspackage。 你的 VSPackage 必须调用`QueryService`此服务并注册其项目工厂时`IVsPackage::SetSite`调用方法。 如果`SetSite`不会调用方法，你的项目不会实例化。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|提供访问权限的当前解决方案中，例如能够枚举项目、 创建新的项目中，注意项目更改等 IDE 的内部的内置概念。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>|调用想要参与源代码管理的项目。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>|维护打开的文档以确定是否已打开一个或多个项目项的表。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>|包含接口和方法调用时实际打开项目项使用的标准编辑器或特定的编辑器。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>|所需的所有项目添加、 删除或重命名其项时调用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>|管理对文件或目录的更改并通知客户端时所选的文件已被更改磁盘上。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>|所需已更新项或将它们保存之前将调用的所有项目和编辑器。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager>|管理项目配置为生成和部署操作的顺序。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger>|提供对用于大多数调试控件的低级别调试器服务的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>|启用 Vspackage 访问有关当前选择的信息，并启用与通信**属性**窗口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|提供基本与 UI 相关的 IDE 功能，例如创建和枚举工具窗口或文档窗口或向用户报告错误的功能。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>|提供对 IDE 的状态栏的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibility3>|用于实现自动化模型。 在您的项目模型，将返回属性对象，允许您创建该对象的实例。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper>|用于对项目对象层次结构中实现剪贴板事件。 `SVsUIHierWinClipboardHelper` 可正确句柄剪切、 复制和粘贴操作。|

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [不在生成中：使用 HierUtil7 项目类来实现一种项目类型 (C++)](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)