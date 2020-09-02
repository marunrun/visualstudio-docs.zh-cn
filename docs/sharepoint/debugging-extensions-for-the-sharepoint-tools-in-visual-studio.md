---
title: Visual Studio 中的 SharePoint 工具调试扩展 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, debugging extensions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e170a5ed703a9bf5aae2e73126de52ecf88e8084
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "64785347"
---
# <a name="debug-extensions-for-the-sharepoint-tools-in-visual-studio"></a>Visual Studio 中的 SharePoint 工具的调试扩展
  可以在实验实例中调试 SharePoint 工具扩展，或在 Visual Studio 的常规实例中调试。 如果需要对扩展的行为进行故障排除，还可以修改注册表值以显示其他错误信息，并配置 Visual Studio 执行 SharePoint 命令的方式。

## <a name="debug-extensions-in-the-experimental-instance-of-visual-studio"></a>Visual Studio 的实验实例中的调试扩展
 为了保护你的 Visual Studio 开发环境不受未经测试的扩展的意外损坏，Visual Studio SDK 提供了一个替代的 Visual Studio 实例，该实例称为 *实验实例*，你可以使用它来安装和测试扩展。 您可以通过使用 Visual Studio 的常规实例来开发新扩展，但您可以在实验实例中调试并运行它们。 有关详细信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。

 如果使用 VSIX 项目来部署扩展，并且 VSIX 项目是解决方案中的启动项目，则当调试解决方案时，Visual Studio 会在实验实例中自动安装和运行该扩展。 启动项目是在调试包含多个项目的解决方案时启动的项目。 有关使用 VSIX 项目部署扩展的详细信息，请参阅 [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

 有关演示如何在 Visual Studio 的实验实例中调试各种类型的扩展的示例，请参阅以下演练：

- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)

- [演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)

- [演练：为 SharePoint 项目创建自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)

- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)

- [演练：在服务器资源管理器扩展中调入 SharePoint 客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)

## <a name="debug-extensions-in-the-regular-instance-of-visual-studio"></a>Visual Studio 的常规实例中的调试扩展
 如果要在 Visual Studio 的常规实例中调试扩展项目，请先在常规实例中安装该扩展。 然后，将调试器附加到另一个 Visual Studio 进程。 完成后，可以删除该扩展，使其不再加载到开发计算机上。

#### <a name="to-install-the-extension"></a>安装扩展

1. 关闭 Visual Studio 的所有实例。

2. 在扩展项目的生成输出文件夹中，通过双击 .vsix 文件或打开其快捷菜单，然后选择 "**打开**" 来打开 *.vsix*文件：

3. 在 " **Visual Studio 扩展安装程序** " 对话框中，选择要安装扩展的 Visual studio 版本，然后选择 " **安装** " 按钮。

     Visual Studio 将扩展文件安装到%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions \\ *作者名称* \\ *扩展名称* \\ *版本*。 此路径中的最后三个文件夹是从 `Author` 扩展的 `Name` `Version` *source.extension.vsixmanifest* 文件中的、和元素构造而来的。

4. 在 Visual Studio 安装扩展后，选择 " **关闭** " 按钮。

#### <a name="to-debug-the-extension"></a>调试扩展

1. 以管理员权限打开 Visual Studio 并打开扩展项目。 以下步骤引用此 Visual Studio 实例作为 *第一个实例*。

2. 以管理员权限启动 Visual Studio 的另一个实例。 以下步骤引用此 Visual Studio 实例作为 *第二个实例*。

3. 切换到 Visual Studio 的第一个实例。

4. 在菜单栏上，选择 " **调试**"、" **附加到进程**"。

5. 在 " **可用进程** " 列表中，选择 " *devenv.exe*"。 此项引用 Visual Studio 的第二个实例;这是您要在其中调试项目扩展的实例。

6. 选择 " **附加** " 按钮。

     Visual Studio 在调试模式下运行扩展项目。

7. 切换到 Visual Studio 的第二个实例。

8. 创建用于加载扩展的新 SharePoint 项目。 例如，如果您正在调试列表定义项目项的扩展，则创建一个 **列表定义** 项目。

9. 执行测试扩展代码所需的任何步骤。

10. 完成调试扩展后，请关闭 Visual Studio 的第二个实例。

#### <a name="to-remove-the-extension"></a>删除扩展

1. 在 Visual Studio 的菜单栏上，依次选择 " **工具**"、" **扩展和更新**"。

     此时，“扩展和更新”**** 对话框打开。

2. 在扩展列表中，选择扩展的名称，然后选择 " **卸载** " 按钮。

3. 在出现的对话框中，选择 " **是"** 按钮，确认要卸载该扩展。

4. 选择 " **立即重新启动** " 按钮以完成卸载。

## <a name="debug-sharepoint-commands"></a>调试 SharePoint 命令
 如果要调试作为 SharePoint 工具扩展的一部分的 SharePoint 命令，则必须将调试器附加到 *vssphost4.exe* 进程。 这是执行 SharePoint 命令的64位主机进程。 有关 SharePoint 命令和 *vssphost4.exe*的详细信息，请参阅 [调入 sharepoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

#### <a name="to-attach-the-debugger-to-the-vssphost4exe-process"></a>将调试器附加到 vssphost4.exe 进程

1. 按照上述说明，开始在 Visual Studio 的实验实例或 Visual Studio 的 Visual Studio 实例中调试扩展。

2. 在运行调试器的 Visual Studio 实例中的菜单栏上，选择 " **调试**"、" **附加到进程**"。

3. 在 " **可用进程** " 列表中，选择 " *vssphost.exe*"。

    > [!NOTE]
    > 如果 vssphost.exe 未出现在列表中，则必须在运行该扩展的 Visual Studio 实例中启动 *vssphost4.exe* 进程。 通常，通过执行导致 Visual Studio 连接到开发计算机上的 SharePoint 站点的操作来执行此操作。 例如，当 (你在 "**服务器资源管理器**" 窗口中的 " **SharePoint 连接**" 节点下，或者将某些 SharePoint 项目项（如**列表实例**或**事件接收**项）添加到 SharePoint 项目中时，Visual Studio 将开始*vssphost4.exe*) 。

4. 选择 " **附加** " 按钮。

5. 在要调试的 Visual Studio 实例中，执行执行命令所需的步骤。

## <a name="modify-registry-values-to-help-debug-sharepoint-tools-extensions"></a>修改注册表值以帮助调试 SharePoint 工具扩展
 当你在 Visual Studio 中调试 SharePoint 工具扩展时，你可以在注册表中修改值，以帮助你对扩展进行故障排除。 这些值位于 **HKEY_CURRENT_USER \software\microsoft\visualstudio\11.0\sharepointtools** 键下。 默认情况下，这些值不存在。

 若要帮助排查 SharePoint 工具的任何扩展，可以创建和设置 EnableDiagnostics 值。 下表描述了此值。

|值|说明|
|-----------|-----------------|
|EnableDiagnostics|指定是否在 " **输出** " 窗口中显示诊断消息的 REG_DWORD。<br /><br /> 若要显示诊断消息，请将此值设置为1。 若要停止显示消息，请将此值设置为0或删除此值。<br /><br /> 若要从 SharePoint 工具扩展将消息写入到 " **输出** " 窗口，请使用 sharepoint 项目服务。 有关详细信息，请参阅 [使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。|

 如果你的扩展包含一个 SharePoint 命令，你可以创建并设置其他值以帮助对命令进行故障排除。 下表介绍了这些值。

|值|说明|
|-----------|-----------------|
|AttachDebuggerToHostProcess|REG_DWORD，它指定是否显示一个对话框，通过该对话框，可以在启动时将调试器附加到 *vssphost4.exe* 。 如果要调试的命令在启动后立即 vssphost.exe 执行，并且在执行命令之前没有足够的时间手动附加调试器，这会很有用。 若要显示该对话框， *vssphost4.exe* <xref:System.Diagnostics.Debugger.Break%2A> 在启动时调用方法。<br /><br /> 若要启用此行为，请将此值设置为1。 若要禁用此行为，请将此值设置为0或删除此值。<br /><br /> 如果将此值设置为 "1"，则可能还需要增加 HostProcessStartupTimeout 值，以便为自己分配足够的时间来附加调试器，然后 Visual Studio 会要求 *vssphost4.exe* 指示它已成功启动。|
|ChannelOperationTimeout|REG_DWORD，它指定 Visual Studio 等待 SharePoint 命令执行的时间（以秒为单位）。 如果命令未在时间执行，则 <xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException> 会引发。<br /><br /> 默认值为 120 秒。|
|HostProcessStartupTimeout|REG_DWORD，它指定 Visual Studio *vssphost4.exe* 等待的时间（以秒为单位），以表示它已成功启动。 如果 *vssphost4.exe* 在时间上没有通知成功启动， <xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException> 则会引发。<br /><br /> 默认值为 60 秒。|
|MaxReceivedMessageSize|REG_DWORD，它指定在 Visual Studio 和 *vssphost4.exe*之间传递的 WCF 消息的最大允许大小（以字节为单位）。<br /><br /> 默认值为1048576字节 (1 MB) 。|
|MaxStringContentLength|REG_DWORD，它指定在 Visual Studio 和 *vssphost4.exe*之间传递的字符串的最大允许大小（以字节为单位）。<br /><br /> 默认值为1048576字节 (1 MB) 。|

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中扩展 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [在 Visual Studio 中部署 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
