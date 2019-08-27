---
title: 调试 Visual Studio 中的 SharePoint 工具扩展 |Microsoft Docs
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
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63443518"
---
# <a name="debug-extensions-for-the-sharepoint-tools-in-visual-studio"></a>调试 Visual Studio 中的 SharePoint 工具扩展
  您可以调试实验实例或 Visual Studio 常规实例中的 SharePoint 工具扩展。 如果需要进行故障排除的行为扩展，还可以修改注册表值以显示其他错误信息并配置 Visual Studio 执行 SharePoint 命令的方式。

## <a name="debug-extensions-in-the-experimental-instance-of-visual-studio"></a>调试 Visual Studio 的实验实例中的扩展
 为了保证未经测试的扩展插件的 Visual Studio 开发环境免遭意外损坏，请在 Visual Studio SDK，提供了一个备用的 Visual Studio 实例，称为*实验实例*，可以使用若要安装和测试扩展。 使用 Visual Studio 中，常规实例开发新的扩展，但调试并在实验实例中运行它们。 有关详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。

 如果您使用 VSIX 项目来部署你的扩展，并且 VSIX 项目是你的解决方案中的启动项目，Visual Studio 将自动安装和调试你的解决方案时，在实验实例中运行扩展。 启动项目是启动时调试包含多个项目的解决方案的项目。 有关使用 VSIX 项目来部署您的扩展插件的详细信息，请参阅[部署的 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)。

 演示如何调试各种类型的 Visual Studio 的实验实例中的扩展的示例，请参阅以下演练：

- [演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)

- [演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)

- [演练：创建 SharePoint 项目的自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)

- [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)

- [演练：调入 SharePoint 客户端对象模型中的服务器资源管理器扩展](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)

## <a name="debug-extensions-in-the-regular-instance-of-visual-studio"></a>调试 Visual Studio 常规实例中的扩展
 如果你想要调试你的 Visual Studio 常规实例中的扩展项目，首先在正则实例中安装扩展。 然后，将调试器附加到第二个 Visual Studio 进程。 完成后，可以删除该扩展，以便它不能再在开发计算机上加载。

#### <a name="to-install-the-extension"></a>安装扩展

1. 关闭 Visual Studio 的所有实例。

2. 在扩展项目的生成输出文件夹，打开 *.vsix*文件通过双击它或通过打开其快捷菜单，然后选择**打开**:

3. 在中**Visual Studio Extension Installer**对话框框中，选择你想要安装该扩展，然后选择 Visual Studio 的版本**安装**按钮。

     Visual Studio 将扩展文件安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions\\*作者姓名*\\*扩展名*\\*版本*。 此路径中的最后三个文件夹从构造`Author`， `Name`，并`Version`中的元素*extension.vsixmanifest*扩展文件。

4. Visual Studio 会安装扩展后，请选择**关闭**按钮。

#### <a name="to-debug-the-extension"></a>若要调试扩展

1. 使用管理员特权打开 Visual Studio 并打开扩展项目。 以下步骤，请参阅 Visual Studio 的此实例*首次实例*。

2. 使用管理员权限启动 Visual Studio 的另一个实例。 以下步骤，请参阅 Visual Studio 的此实例*第二个实例*。

3. 切换到 Visual Studio 的第一个实例。

4. 在菜单栏上依次选择**调试**，**附加到进程**。

5. 在中**可用进程**列表中，选择*devenv.exe*。 此项所引用的 Visual Studio; 第二个实例这是你想要调试你的项目扩展中的实例。

6. 选择**附加**按钮。

     Visual Studio 在调试模式下运行扩展项目。

7. 切换到 Visual Studio 的第二个实例。

8. 创建新的 SharePoint 项目加载你的扩展。 例如，如果你正在调试的列表定义项目项的扩展，创建**列表定义**项目。

9. 执行任何步骤所需测试您的扩展代码。

10. 当完成调试扩展后，关闭 Visual Studio 的第二个实例。

#### <a name="to-remove-the-extension"></a>若要删除扩展

1. 在 Visual Studio 中，在菜单栏上，选择**工具**，**扩展和更新**。

     此时，“扩展和更新”对话框打开。

2. 在扩展的列表，选择的扩展插件的名称，然后选择**卸载**按钮。

3. 在出现的对话框中，选择**是**按钮以确认你想要卸载扩展。

4. 选择**立即重新启动**按钮以完成卸载。

## <a name="debug-sharepoint-commands"></a>调试 SharePoint 命令
 如果你想要调试的是 SharePoint 工具扩展的一部分的 SharePoint 命令，则必须附加到调试器*vssphost4.exe*过程。 这是执行 SharePoint 命令的 64 位主机进程。 有关 SharePoint 命令的详细信息和*vssphost4.exe*，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

#### <a name="to-attach-the-debugger-to-the-vssphost4exe-process"></a>若要将调试器附加到 vssphost4.exe 进程

1. 开始调试你的 Visual Studio 实验实例或 Visual Studio 常规实例中的扩展，按照上面的说明。

2. 在菜单栏在其中运行调试器，Visual Studio 实例中，选择**调试**，**附加到进程**。

3. 在中**可用进程**列表中，选择*vssphost.exe*。

    > [!NOTE]
    > 如果列表中不显示 vssphost.exe，则必须首先*vssphost4.exe*进程中运行该扩展的 Visual Studio 的实例。 通常情况下，您会为此，执行的操作导致 Visual Studio 以连接到开发计算机上的 SharePoint 站点。 例如，Visual Studio 将启动*vssphost4.exe*当您展开站点连接节点 （节点显示站点 URL） 下**SharePoint 连接**中的节点**服务器资源管理器**窗口中，或当你添加特定的 SharePoint 项目项，例如**列表实例**或**事件接收器**向 SharePoint 项目项。

4. 选择**附加**按钮。

5. 在 Visual Studio 正在调试的实例中，执行执行命令所需的步骤。

## <a name="modify-registry-values-to-help-debug-sharepoint-tools-extensions"></a>修改注册表值，以帮助调试 SharePoint 工具扩展
 当你进行调试的 Visual Studio 中的 SharePoint 工具扩展时，可以修改注册表来帮助你解决扩展中的值。 值存在下**HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools**密钥。 默认情况下不存在这些值。

 若要帮助解决任何 SharePoint 工具扩展，可以创建并将 EnableDiagnostics 值设置。 下表描述了此值。

|“值”|描述|
|-----------|-----------------|
|EnableDiagnostics|指定是否在显示的诊断消息的 REG_DWORD**输出**窗口。<br /><br /> 若要显示的诊断消息，请将此值设置为 1。 若要停止显示消息，请将此值设置为 0，或删除此值。<br /><br /> 若要将消息写入**输出**窗口从 SharePoint 工具扩展，请使用 SharePoint 项目服务。 有关详细信息，请参阅[使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)。|

 如果您的扩展插件包括 SharePoint 命令，可以创建并设置其他值，以帮助进行故障排除命令。 下表介绍了这些值。

|“值”|描述|
|-----------|-----------------|
|AttachDebuggerToHostProcess|指定是否显示一个对话框，可以将附加到调试器的 REG_DWORD *vssphost4.exe*只要它启动。 如果你想要调试的命令在启动后立即 vssphost.exe 执行这很有用，并且没有足够的时间来手动将调试器附加之前执行此命令。 若要显示的对话框中， *vssphost4.exe*调用<xref:System.Diagnostics.Debugger.Break%2A>方法在启动时。<br /><br /> 若要启用此行为，请将此值设置为 1。 若要禁用此行为，请将此值设置为 0 或删除此值。<br /><br /> 如果此值设置为 1 时，可能要增加 HostProcessStartupTimeout 值以足够的时间来将调试器附加之前 Visual Studio 期望则给自己加*vssphost4.exe*以指示它已成功启动。|
|ChannelOperationTimeout|指定的时间，以秒为单位，Visual Studio 等待要执行的 SharePoint 命令的 REG_DWORD。 如果该命令不会执行的时间，<xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException>引发。<br /><br /> 默认值为 120 秒。|
|HostProcessStartupTimeout|指定的时间，以秒为单位的 REG_DWORD，Visual Studio 将等待*vssphost4.exe*以指示它已成功启动。 如果*vssphost4.exe*不表示成功的开始时间，<xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException>引发。<br /><br /> 默认值为 60 秒。|
|MaxReceivedMessageSize|指定的最大允许大小，以字节为单位，会在 Visual Studio 之间传递的 WCF 消息的 REG_DWORD 并*vssphost4.exe*。<br /><br /> 默认值为 1048576 字节 (1 MB)。|
|MaxStringContentLength|指定的最大允许大小，以字节为单位会在 Visual Studio 之间传递的字符串的 REG_DWORD 并*vssphost4.exe*。<br /><br /> 默认值为 1048576 字节 (1 MB)。|

## <a name="see-also"></a>请参阅

- [扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [部署 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
