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
ms.openlocfilehash: d83c8ffd4fe5ebb627b70fa07f010bdc713225dd
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72984500"
---
# <a name="debug-sharepoint-solutions"></a>调试 SharePoint 解决方案
  您可以使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试器调试 SharePoint 解决方案。 开始调试时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将项目文件部署到 SharePoint 服务器，然后在 Web 浏览器中打开 SharePoint 站点的实例。 以下部分说明如何在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中调试 SharePoint 应用程序。

- [启用调试](#enable-debugging)

- [F5 调试和部署过程](#f5-debug-and-deployment-process)

- [SharePoint 项目功能](#sharepoint-project-features)

- [调试工作流](#debug-workflows)

- [调试功能事件接收器](#debug-feature-event-receivers)

- [启用 ehanced 调试信息](#enable-enhanced-debugging-information)

## <a name="enable-debugging"></a>启用调试
 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中首次调试 SharePoint 解决方案时，会有一个对话框警告您未将 web.config 文件配置为启用调试。 （Web.config 文件是在你安装 SharePoint server 时创建的。 有关详细信息，请参阅使用 web.config[文件](/previous-versions/office/developer/sharepoint-2010/ms460914(v=office.14))。）使用该对话框，您可以选择运行项目而不调试或修改 web.config 文件以启用调试。 如果选择第一个选项，则项目会正常运行。 如果选择第二个选项，则 web.config 文件将配置为：

- 打开调用堆栈（`CallStack="true"`）

- 禁用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] （`<customErrors mode="Off" />`）中的自定义错误

- 启用编译调试（`<compilation debug="true">`）

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

 若要撤消更改并禁用调试，请在 web.config 文件中更改以下 [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]：

- 关闭调用堆栈（`CallStack="false"`）

- 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] （`<customErrors mode="On" />`）中启用自定义错误

- 禁用编译调试（`<compilation debug="false">`）

## <a name="f5-debug-and-deployment-process"></a>F5 调试和部署过程
 在调试模式下运行 SharePoint 项目时，SharePoint 部署过程将执行以下任务：

1. 运行可自定义的预先部署命令。

2. 使用 [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] 命令创建 Web 解决方案包（.wsp）文件。 .Wsp 文件包含所有必需的文件和功能。 有关详细信息，请参阅[解决方案概述](/previous-versions/office/developer/sharepoint-2010/aa543214(v=office.14))。

3. 如果 SharePoint 解决方案是场解决方案，则回收指定站点 [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)]的 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] 应用程序池。 此步骤将释放 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] 工作进程锁定的文件。

4. 如果先前版本的包已存在，则将收回 .wsp 文件中以前版本的功能和文件。 此步骤停用功能，卸载解决方案包，然后删除 SharePoint 服务器上的解决方案包。

5. 在 .wsp 文件中安装功能和文件的当前版本。 此步骤在 SharePoint 服务器上添加和安装解决方案。

6. 对于工作流，将安装工作流程序集。 您可以通过使用 "*程序集位置*" 属性来更改其位置。

7. 如果范围为站点或 Web，则在 SharePoint 中激活项目的功能。 不会激活场和 WebApplication 范围中的功能。

8. 对于工作流，将工作流与在 " **Sharepoint 自定义向导**" 中选择的 sharepoint 库、列表或网站相关联。

   > [!NOTE]
   > 仅当在向导中选择了 "**自动关联工作流**" 时，才会发生此关联。

9. 运行可自定义的部署后命令。

10. 将 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试器附加到 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] 进程（*w3wp.exe*）。 如果项目类型允许您更改*沙盒解决方案*属性，并且其值设置为**true**，则调试器会附加到另一个进程（*spucworkerprocess.exe*）。 有关详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

11. 如果 SharePoint 解决方案是场解决方案，则启动 JavaScript 调试器。

12. 在 Web 浏览器中显示适当的库、列表或网站页面。

    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 在每个任务完成后，在 "输出" 窗口中显示一条状态消息。 如果任务无法完成，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会在错误列表窗口中显示一条错误消息。

## <a name="sharepoint-project-features"></a>SharePoint 项目功能
 功能是一种易于使用的模块化功能，它通过使用站点定义简化站点的修改。 它也是可为特定范围激活的 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] （WSS）元素包，可帮助用户完成特定目标或任务。 模板部署为功能。

 在调试模式下运行项目时，部署过程会在 *%COMMONPROGRAMFILES%\Microsoft Shared\web server extensions\14\TEMPLATE\FEATURES*的*功能*目录中创建一个文件夹。 功能名称的格式为*项目名称*_Feature*x*，如 TestProject_Feature1。

 功能目录中的解决方案文件夹包含*功能定义*文件和*工作流定义*文件。 功能定义文件（功能 .xml）描述项目功能中的文件。项目定义文件（*元素 .xml*）描述项目模板。 可以在**解决方案资源管理器**中找到*元素 .xml* ，但在创建解决方案包时将生成功能 .xml。 有关这些文件的详细信息，请参阅[SharePoint 项目和项目项模板](../sharepoint/sharepoint-project-and-project-item-templates.md)。

## <a name="debug-workflows"></a>调试工作流
 在调试工作流项目时，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 会将工作流模板（取决于其类型）添加到库或列表中。 然后，您可以手动启动工作流模板，也可以通过添加或更新项来启动。 然后，可以使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 来调试工作流。

> [!NOTE]
> 如果添加了对其他程序集的引用，请确保这些程序集安装在全局程序集缓存（[!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)]）中。 否则，工作流解决方案将会失败。 有关如何安装程序集的信息，请参阅[在文档或项上手动启动工作流](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963)。

 但是，部署过程不会启动工作流。 您必须从 SharePoint 网站启动工作流。 还可以通过使用客户端应用程序（如 Microsoft Office Word 2010）或使用单独的服务器端代码来启动工作流。 使用 " **SharePoint 自定义向导**" 中指定的一种方法。

 例如，如果指定可以手动启动工作流，请直接从库或列表中的项启动工作流。 有关如何手动启动工作流的详细信息，请参阅[在文档项上手动启动工作流](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963)。

## <a name="debug-feature-event-receivers"></a>调试功能事件接收器
 默认情况下，当你运行 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 的 SharePoint 应用程序时，将自动为你在 SharePoint 服务器上激活其功能。 但是，当调试功能事件接收器时，这会导致问题，因为在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]激活某个功能时，该功能将在与调试器不同的进程中运行。 这意味着某些调试功能（例如断点）将无法正常工作。

 若要禁用自动激活 SharePoint 中的功能并允许对功能事件接收器进行适当的调试，请在调试之前将项目的 "**活动部署配置**" 属性的值设置为 "**无激活**"。 然后，在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中开始调试 SharePoint 应用程序后，在 SharePoint 中手动激活此功能。 若要激活该功能，请打开 SharePoint 中的 "**站点操作**" 菜单，选择 "**站点设置**"，选择 "**管理站点功能**" 链接，然后选择该功能旁边的 "**激活**" 按钮，以继续正常调试。

## <a name="enable-enhanced-debugging-information"></a>启用增强的调试信息
 由于在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 进程（devenv） [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]、Sharepoint 宿主进程（*vssphost4.exe 进程*）、SHAREPOINT 和 WCF 层之间有时进行复杂的交互，因此，诊断生成、部署等时发生的错误可能是严峻. 为了帮助您解决此类错误，您可以启用增强的调试信息。 为此，请在 Windows 注册表中中转到以下注册表项：

 **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools**

 如果 "EnableDiagnostics" **REG_DWORD**值尚不存在，请手动创建。 将 "EnableDiagnostics" 值设置为 "1"。

 将此项值设置为1会导致当在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中运行时出现项目系统错误时，堆栈跟踪信息将显示在 "**输出**" 窗口中。 若要禁用增强的调试信息，请将 EnableDiagnostics 设置回 0 或者删除该值。

 有关其他 SharePoint 注册表项的详细信息，请参阅[Visual Studio 中的 SharePoint 工具调试扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

## <a name="see-also"></a>请参阅
- [SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)
