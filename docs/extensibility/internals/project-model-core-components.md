---
title: 项目模型核心组件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project models, objects and interfaces
- project models, services
ms.assetid: b2f572d3-b26d-4846-92d1-84055fac141a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 34f65973f0f3edc1dd6264c32d165503dca78681
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706541"
---
# <a name="project-model-core-components"></a>项目模型核心组件
下表将展开项目模型。 这些表简要描述了模型中标识的接口和服务以及与特定对象关联的接口和服务。 此外，这些表还详细介绍了在项目创建和维护中可选的其他接口，具体取决于特定项目类型的要求。

 有关详细信息，请参阅[支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)。

### <a name="package-object"></a>包对象

|接口|注释|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPackage>|在 IDE 中初始化 VS 包，并将其服务提供给 IDE。|

### <a name="project-factory-object"></a>项目工厂对象

|接口|注释|
|---------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|管理创建新项目和打开现有项目。|

### <a name="project-objects"></a>项目对象

|接口|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>|管理项目项的添加和删除，打开编辑器，并维护每个文档名字项和 之间的`VSITEMID`映射。 继承`IVsProject`和`IVsProject2`。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|管理导航和显示属性并提供事件。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>|启用类似于命令执行的命令，`IOleCommandTarget`这些命令（如剪切和重命名）仅在焦点位于解决方案资源管理器中时应用。|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|用作项目层次结构的主命令目标接口。 它是查询对象的命令状态或状态和正在运行的命令的标准接口。 当您未在"项目"窗口中集中时可用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|协调项目状态的持久性。 通常，项目状态存储为项目文件，但可以适应不基于文件的存储系统。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2>|使项目能够管理其项目项的持久性的所有方面，无论是磁盘上的文件还是其他存储系统中的对象。 该`IVsPersistHierarchyItem2`接口用于不实现接口的<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>项。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>|协调与源代码控制的交互。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfgProvider>|使项目能够管理配置信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2>|管理项目配置对象，如调试/释放配置。 生成、部署和调试操作通过项目配置对象进行协调。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDeleteHandler>|按层次结构实现，以控制层次结构项的删除（破坏性）或删除（非破坏性）选项。 从`IVsHierarchy`接口调用接口上的`IVsHierarchyDeleteHandler`查询接口。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsGetCfgProvider>|提供实现选项，使支持`IVsCfgProvider2`接口的对象位于不同的 COM 标识上，而不是实现`IVsHierarchy`接口的项目对象。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectStartupServices>|实现可选的接口，使项目可被其他开发人员扩展。 该`IVsProjectStartupServices`接口使第三方 VSPackage 能够注册您保存到项目文件中的 GUID，以便每次项目加载时，您都会将第三方服务 GUID 加载到项目文件中并调用`QueryService`该 GUID。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierWinClipboardHelperEvents>|按`UIHierarchy`窗口中的源层次结构实现，以协调剪贴板操作（如剪切、复制和粘贴）。 使用界面`AdviseClipboardHelperEvents`注册剪贴板事件。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataSource2>|在 UI 层次结构窗口中的拖放操作期间，提供有关拖动项相对于其数据源的信息。 从`IVsHierarchy`接口调用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchyDropDataTarget>|在 UI 层次结构窗口中的拖放操作中提供有关拖动项相对于其放置目标的信息。 从`IVsHierarchy`接口调用。|

### <a name="configuration-object"></a>配置对象

|接口|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg>|提供有关配置的信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg2>|使项目能够管理配置信息。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|使项目能够在调试器的控制下运行。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>|由对其他项目执行部署操作的部署项目实现。|

### <a name="configuration-builder-object"></a>配置生成器对象

|接口|注释|
|----------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>|管理项目配置的生成操作。|

### <a name="additional-project-objects"></a>其他项目对象

|接口|注释|
|----------------|--------------|
|`IDispatch`<br /><br /> <xref:Microsoft.VisualStudio.OLE.Interop.ISpecifyPropertyPages>|在 **"属性"** 窗口中显示项属性。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsEnumOutputs>|显示用于部署的输出。|

 下表简要描述了项目模型中标识的服务。

### <a name="services"></a>服务

|服务|注释|
|-------------|--------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRegisterProjectTypes>|VSPackages 用于实现项目类型以注册其项目工厂是否存在 IDE。 VSPackage 必须调用`QueryService`此服务，并在调用方法时`IVsPackage::SetSite`注册其项目工厂。 如果未调用`SetSite`该方法，则不会实例化项目。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolution>|提供对 IDE 当前解决方案的内部内置概念的访问，例如枚举项目、创建新项目、注意项目更改等。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSccManager>|由希望参与源代码管理的项目调用。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>|维护打开的文档表，以确定是否已打开一个或多个项目项。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>|包含使用标准编辑器或特定编辑器实际打开项目项而调用的接口和方法。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsTrackProjectDocuments>|所有项目在添加、删除或重命名项目时都需要调用它们。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsFileChangeEx>|管理对文件或目录的更改，并在磁盘上更改选定文件时通知客户端。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsQueryEditQuerySave>|要求所有项目和编辑在脏题或保存项目之前调用它们。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsSolutionBuildManager>|管理项目配置的生成和部署操作的顺序。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellDebugger>|提供对用于大多数调试控件的低级调试器服务的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>|启用 VSPackages 访问有关当前选择的信息，并启用与 **"属性"** 窗口的通信。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShell>|提供与 UI 相关的基本 IDE 功能，例如创建和枚举工具窗口或文档窗口或向用户报告错误的能力。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsStatusbar>|提供对 IDE 状态栏的访问。|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsExtensibility3>|用于实现自动化模型。 在项目模型中，您将返回一个属性对象，该对象允许您创建该对象的实例。|
|<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIHierWinClipboardHelper>|用于在层次结构中的项目对象上实现剪贴板事件。 `SVsUIHierWinClipboardHelper`允许您正确处理剪切、复制和粘贴操作。|

## <a name="see-also"></a>请参阅
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [清单：新建项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [不在生成中：使用 HierUtil7 项目类实现项目类型 （C++）](https://msdn.microsoft.com/library/a5c16a09-94a2-46ef-87b5-35b815e2f346)
- [支持符号浏览工具](../../extensibility/internals/supporting-symbol-browsing-tools.md)
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)
