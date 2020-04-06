---
title: 使用菜单命令创建扩展 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- write a vspackage
- vspackage
- tutorials
- visual studio package
ms.assetid: f97104c8-2bcb-45c7-a3c9-85abeda8df98
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: da1be8c6e00efd5d9ac94e53bf551d82d0f17ca4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739563"
---
# <a name="create-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展

本演练演示如何使用启动记事本的菜单命令创建扩展。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-menu-command"></a>创建菜单命令

1. 创建名为**FirstMenu 命令 的**VSIX 项目。 您可以通过搜索"vsix"在 **"新项目**"对话框中找到 VSIX 项目模板。

2. 打开项目时，添加名为**FirstCommand 的**自定义命令项模板。 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 在"**添加新项目"** 对话框中，转到**可视化 C#** > **扩展性**并选择 **"自定义命令**"。 在窗口底部的 **"名称"** 字段中，将命令文件名更改为*FirstCommand.cs*。

3. 生成项目并启动调试。

    视觉工作室的实验实例出现。 有关实验实例的详细信息，请参阅[实验实例](../extensibility/the-experimental-instance.md)。

::: moniker range="vs-2017"

4. 在实验例中，打开 **"工具** > **扩展"和"更新"** 窗口。 您应该在此处看到**FirstMenu 命令**扩展。 （如果在 Visual Studio 的工作实例中打开**扩展和更新**，则看不到**FirstMenu命令**）。

::: moniker-end

::: moniker range=">=vs-2019"

4. 在实验例中，打开**扩展** > **管理扩展**窗口。 您应该在此处看到**FirstMenu 命令**扩展。 （如果在可视化工作室的工作实例中打开 **"管理扩展"，** 则看不到**FirstMenu 命令**。

::: moniker-end

现在转到实验实例中的 **"工具"** 菜单。 您应该会看到**调用第一命令命令**。 此时，该命令会显示一个消息框，其中显示**FirstMenu命令中的 FirstCommand 包.FirstCommand.Menuitemcall（）**。 我们将在下一节中了解如何从该命令实际启动记事本。

## <a name="change-the-menu-command-handler"></a>更改菜单命令处理程序

现在，让我们更新命令处理程序以启动记事本。

1. 停止调试并返回可视化工作室的工作实例。 打开*FirstCommand.cs*文件并添加以下使用语句：

    ```csharp
    using System.Diagnostics;
    ```

2. 查找私有 FirstCommand 构造函数。 这是命令连接到命令服务并指定命令处理程序的位置。 将命令处理程序的名称更改为 StartNotepad，如下所示：

    ```csharp
    private FirstCommand(AsyncPackage package, OleMenuCommandService commandService)
    {
        this.package = package ?? throw new ArgumentNullException(nameof(package));
        commandService = commandService ?? throw new ArgumentNullException(nameof(commandService));

        CommandID menuCommandID = new CommandID(CommandSet, CommandId);
        // Change to StartNotepad handler.
        MenuCommand menuItem = new MenuCommand(this.StartNotepad, menuCommandID);
        commandService.AddCommand(menuItem);
    }
    ```

3. 删除`MenuItemCallback`方法并添加一`StartNotepad`个方法，该方法将启动记事本：

    ```csharp
    private void StartNotepad(object sender, EventArgs e)
    {
        Process proc = new Process();
        proc.StartInfo.FileName = "notepad.exe";
        proc.Start();
    }
    ```

4. 现在试试看。当您开始调试项目并单击 **"工具** > **调用第一命令**"时，您应该会看到一个记事本实例出现。

    您可以使用类的<xref:System.Diagnostics.Process>实例来运行任何可执行文件，而不仅仅是记事本。 例如，使用`calc.exe`尝试。

## <a name="clean-up-the-experimental-environment"></a>清理实验环境

如果您正在开发多个扩展，或者只是使用扩展代码的不同版本探索结果，则实验环境可能会停止以应有的方式工作。 在这种情况下，您应该运行重置脚本。 它被称为**重置视觉工作室实验实例**，并作为可视化工作室 SDK 的一部分提供。 此脚本从实验环境中删除对扩展的所有引用，因此您可以从头开始。

您可以通过两种方式之一访问此脚本：

1. 从桌面上，找到**重置可视化工作室实验实例**。

2. 从命令行运行以下命令：

    ```xml
    <VSSDK installation>\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe /Reset /VSInstance=<version> /RootSuffix=Exp && PAUSE

    ```

## <a name="deploy-your-extension"></a>部署扩展

现在，您的工具扩展程序可以按照您所需的方式运行，是时候考虑与朋友和同事共享它了。 这很容易，只要他们安装了 Visual Studio 2015。 所有你需要做的是向他们发送你构建的 *.vsix*文件。 （请确保在发布模式下生成它。

您可以在*FirstMenu 命令*箱目录中找到此扩展名的 *.vsix*文件。 具体来说，假设您已经构建了发布配置，它将在以下版本中：

*\<代码目录>_FirstMenu命令\第一菜单命令\bin\释放]第一菜单命令.vsix*

要安装扩展名，您的好友需要关闭 Visual Studio 的所有打开实例，然后双击 *.vsix*文件，该文件将启动**VSIX 安装程序**。 这些文件将复制到 *%LocalAppData%%\Microsoft_VisualStudio\<版本>\扩展目录*。

当你的朋友再次提出 Visual Studio 时，他们会在**工具** > **扩展和更新**中找到 FirstMenu命令扩展。 它们也可以转到**扩展和更新**以卸载或禁用扩展。

## <a name="next-steps"></a>后续步骤

本演练只显示使用 Visual Studio 扩展程序可以执行的部分操作。 以下是使用 Visual Studio 扩展可以执行的其他（相当简单）操作的简短列表：

1. 您可以使用简单的菜单命令执行更多操作：

   1. 添加您自己的图标：[向菜单命令添加图标](../extensibility/adding-icons-to-menu-commands.md)

   2. 更改菜单命令的文本：[更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md)

   3. 向命令添加菜单快捷方式：[将键盘快捷键绑定到菜单项](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)

2. 添加不同类型的命令、菜单和工具栏：[扩展菜单和命令](../extensibility/extending-menus-and-commands.md)

3. 添加工具窗口并扩展内置可视化工作室工具窗口：[扩展和自定义工具窗口](../extensibility/extending-and-customizing-tool-windows.md)

4. 将 IntelliSense、代码建议和其他功能添加到现有代码编辑器：[扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)

5. 将选项和属性页面和用户设置添加到扩展名：[扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md)并[扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)

   其他类型的扩展需要更多的工作，例如创建一种新型的项目（[扩展项目](../extensibility/extending-projects.md)）、创建新类型的编辑器（[创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)），或在隔离 shell 中实现扩展[：Visual Studio 隔离外壳](https://visualstudio.microsoft.com/vs/older-downloads/isolated-shell/)
