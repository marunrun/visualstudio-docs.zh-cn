---
title: 调试 SharePoint 解决方案 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.WebConfigModificationDialog
- VS.SharePointTools.Project.DebuggingNotEnabled
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, debugging
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 60aa38d5042625393132ffceb3cc226f44e67645
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443496"
---
# <a name="debug-sharepoint-solutions"></a>调试 SharePoint 解决方案
  您可以通过使用调试 SharePoint 解决方案[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]调试器。 当开始调试，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将项目文件部署到 SharePoint 服务器，然后在 Web 浏览器中打开 SharePoint 站点的实例。 以下各节说明如何调试 SharePoint 应用程序中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

- [启用调试](#enable-debugging)

- [F5 调试和部署过程](#f5-debug-and-deployment-process)

- [SharePoint 项目功能](#sharepoint-project-features)

- [调试工作流](#debug-workflows)

- [调试功能事件接收器](#debug-feature-event-receivers)

- [启用 ehanced 调试信息](#enable-enhanced-debugging-information)

## <a name="enable-debugging"></a>启用调试
 当你第一次调试 SharePoint 解决方案中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，对话框中向你发出警报的 web.config 文件未配置为启用调试。 （在安装 SharePoint server 时，被创建 web.config 文件。 有关详细信息，请参阅[使用 Web.config 文件](http://go.microsoft.com/fwlink/?LinkID=149266)。)对话框中显示的不调试或修改 web.config 文件的情况下运行该项目启用调试的选项。 如果选择第一个选项，则项目会正常运行。 如果选择第二个选项，则 web.config 文件将配置为：

- 打开调用堆栈 (`CallStack="true"`)

- 禁用中的自定义错误[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)](`<customErrors mode="Off" />`)

- 启用编译调试 (`<compilation debug="true">`)

  生成的 web.config 文件如下所示：

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <configuration>
        ...
        <SharePoint>
            <SafeMode MaxControls="200"
                CallStack="true"
                DirectFileDependencies="10"
                TotalFileDependencies="50"
                AllowPageLevelTrace="false">
                ...
            </SafeMode>
        ...
        </SharePoint>
        <system.web>
            ...
            <customErrors mode="Off" />
            ...
            <compilation debug="true">
            ...
            </compilation>
            ...
        </system.web>
        ...
    </configuration>
```

 若要撤消所做的更改并禁用调试，更改以下[!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]web.config 文件中：

- 关闭调用堆栈 (`CallStack="false"`)

- 启用的自定义错误[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)](`<customErrors mode="On" />`)

- 禁用编译调试 (`<compilation debug="false">`)

## <a name="f5-debug-and-deployment-process"></a>F5 调试和部署过程
 在调试模式下运行您的 SharePoint 项目时，SharePoint 部署过程将执行以下任务：

1. 在运行的可自定义预先部署命令。

2. 使用创建 Web 解决方案包 (.wsp) 文件[!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)]命令。 .Wsp 文件包含所有必要的文件和功能。 有关详细信息，请参阅[解决方案概述](http://go.microsoft.com/fwlink/?LinkID=128154)。

3. 如果 SharePoint 解决方案的场解决方案，请回收[!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)]指定站点的应用程序池[!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)]。 此步骤将释放锁定的文件[!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)]工作进程。

4. 如果以前版本的包已存在，收回上一版本的功能和.wsp 文件中的文件。 此步骤中停用了功能、 卸载解决方案包，然后删除 SharePoint 服务器上的解决方案包。

5. 在.wsp 文件中安装的功能和文件的当前版本。 此步骤中添加，并在 SharePoint 服务器上安装解决方案。

6. 对于工作流，工作流程序集的安装。 可以通过更改其位置*程序集位置*属性。

7. 如果该范围位于站点，激活 SharePoint 中的项目的功能。 未激活场和 web 应用程序作用域中的功能。

8. 对于工作流，将与 SharePoint 库、 列表或你在中选择的站点关联工作流**SharePoint 自定义向导**。

   > [!NOTE]
   > 仅当你选择，会发生这种关联**自动关联工作流**向导中。

9. 在运行的可自定义后期部署命令。

10. 将附加[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]调试器[!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)]过程 (*w3wp.exe*)。 如果项目类型允许您更改*沙盒解决方案*属性和其值设置为**true**，调试器会附加到另一进程 (*SPUCWorkerProcess.exe*). 有关详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

11. 如果 SharePoint 解决方案已部署场解决方案，请启动 JavaScript 调试器。

12. 在 Web 浏览器中显示相应的库、 列表或站点页。

    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 每个任务完成后，请在输出窗口中显示的状态消息。 如果无法完成任务，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]错误列表窗口中显示一条错误消息。

## <a name="sharepoint-project-features"></a>SharePoint 项目功能
 一项功能是功能的一个可移植的可修改站点简化通过使用站点定义模块化单元。 它也是一个软件包[!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)](WSS) 元素的特定作用域可以激活，以帮助用户完成特定目标或任务。 模板部署为功能。

 在调试模式下运行项目时，部署过程会创建一个文件夹中的*功能*在目录 *%COMMONPROGRAMFILES%\Microsoft Shared\web server extensions\14\TEMPLATE\FEATURES*。 功能名称采用格式*项目名称*_Feature*x*，如 TestProject_Feature1。

 解决方案的文件夹中的功能目录包含*的功能定义*文件和一个*工作流定义*文件。 功能定义文件 (Feature.xml) 描述项目的功能项目定义文件中的文件 (*Elements.xml*) 介绍了项目模板。 *Elements.xml*可在**解决方案资源管理器**，但 Feature.xml 在创建解决方案包时生成。 有关这些文件的详细信息，请参阅[SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

## <a name="debug-workflows"></a>调试工作流
 调试工作流项目时[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]将 （具体取决于它的类型） 的工作流模板添加到库或列表。 然后，可以手动或通过添加或更新项启动工作流模板。 然后，可以使用[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]调试工作流。

> [!NOTE]
> 如果添加对其他程序集的引用，请确保这些程序集文件安装在全局程序集缓存 ( [!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)])。 否则，工作流解决方案将会失败。 有关如何安装的程序集的信息，请参阅[手动启动工作流上的文档或项](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963)。

 但是，部署过程不会启动工作流。 必须从 SharePoint Web 站点启动工作流。 使用的客户端应用程序，例如 Microsoft Office Word 2010 中，或使用单独的服务器端代码，还可以启动工作流。 使用一种方法中指定**SharePoint 自定义向导**。

 例如，如果您指定可以手动启动工作流，请直接从库或列表中的项启动工作流。 有关如何手动启动工作流的详细信息，请参阅[手动启动工作流上的文档项](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963)。

## <a name="debug-feature-event-receivers"></a>调试功能事件接收器
 默认情况下，在运行时[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 应用程序，它的功能会自动为你激活 SharePoint 服务器上。 但是，这会导致问题时调试功能事件接收器，因为通过激活某个功能时[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，它在不同于调试器进程中运行。 这意味着某些调试功能，如断点，将无法在正常工作。

 若要禁用自动激活 SharePoint 中的功能，从而允许正确的调试功能事件接收器，项目的值设置**活动部署配置**属性设置为**无激活**之前调试。 然后，在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中开始调试 SharePoint 应用程序后，在 SharePoint 中手动激活此功能。 若要激活该功能，请打开**站点操作**在 SharePoint 中，菜单中，选择**站点设置**，选择**管理站点功能**链接，，然后选择**激活**功能，若要继续调试作为普通旁边的按钮。

## <a name="enable-enhanced-debugging-information"></a>启用增强的调试信息
 由于之间有时会比较复杂的交互[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]进程 (devenv.exe) [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 宿主进程 (*vssphost4.exe*)，SharePoint，并诊断发生的错误的 WCF 层时生成、 部署和等可以是一个挑战。 若要帮助你解决此类错误，可以启用增强的调试信息。 若要执行此操作，请转到 Windows 注册表中的以下注册表项：

 **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools**

 如果"EnableDiagnostics" **REG_DWORD**值尚不存在不存在，手动创建它。 将"EnableDiagnostics"值设为"1。

 将此密钥值设置为 1 会导致堆栈跟踪信息显示在**输出**窗口运行时，项目系统错误发生时，随时[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 若要禁用增强的调试信息，请将 EnableDiagnostics 设置回 0 或者删除该值。

 有关其他 SharePoint 注册表项的详细信息，请参阅[调试的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [对 SharePoint 解决方案进行故障排除](../sharepoint/troubleshooting-sharepoint-solutions.md)
