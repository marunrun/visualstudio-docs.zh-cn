---
title: 使用菜单命令创建扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- write a vspackage
- vspackage
- tutorials
- visual studio package
ms.assetid: f97104c8-2bcb-45c7-a3c9-85abeda8df98
caps.latest.revision: 57
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e3bbf6b3b1ed2565d5e58806bd0935f713ba5bfd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62572882"
---
# <a name="creating-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何使用可启动记事本的菜单命令创建扩展。  
  
## <a name="prerequisites"></a>必备条件  
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="creating-a-menu-command"></a>创建菜单命令  
  
1. 创建名为 **FirstMenuCommand**的 VSIX 项目。 可以在 " **新项目** " 对话框中的 " **Visual c #/扩展性**" 下找到 VSIX 项目模板。  
  
2. 当项目打开时，添加一个名为 **FirstCommand**的自定义命令项模板。 在 **解决方案资源管理器**中，右键单击项目节点，然后选择 " **添加/新建项**"。 在 " **添加新项** " 对话框中，切换到 " **Visual c #/扩展性** "，然后选择 " **自定义命令**"。 在窗口底部的 " **名称** " 字段中，将命令文件名更改为 **FirstCommand.cs**。  
  
3. 生成项目并启动调试。  
  
     此时将显示 Visual Studio 的实验实例。 有关实验实例的详细信息，请参阅 [实验实例](../extensibility/the-experimental-instance.md)。  
  
4. 在实验实例中，打开 "  **工具"/"扩展和更新** " 窗口。 此处应会显示 **FirstMenuCommand** 扩展。  (如果打开 Visual Studio 的工作实例中的 **扩展和更新** ，则不会看到 **FirstMenuCommand**) 。  
  
     现在，请在实验实例中中转到 " **工具** " 菜单。 应会看到 " **调用 FirstCommand** " 命令。 此时，将显示一个消息框，其中显示 "FirstCommandPackage 内部 FirstMenuCommand. FirstCommand ( # A1"。 在下一部分中，我们将了解如何实际从此命令启动记事本。  
  
## <a name="changing-the-menu-command-handler"></a>更改菜单命令处理程序  
 现在，让我们更新命令处理程序以启动记事本。  
  
1. 停止调试并返回到 Visual Studio 的工作实例。 打开 FirstCommand.cs 文件并添加以下 using 语句：  
  
    ```csharp  
    using System.Diagnostics;  
    ```  
  
2. 查找 private FirstCommand 构造函数。 这是命令与命令服务挂钩的位置，并且指定了命令处理程序。 将命令处理程序的名称更改为 StartNotepad，如下所示：  
  
    ```csharp  
    private FirstCommand(Package package)  
    {  
        if (package == null)  
        {  
            throw new ArgumentNullException(nameof(package));  
        }  
  
        this.package = package;  
  
         OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
        if (commandService != null)  
        {  
            CommandID menuCommandID = new CommandID(CommandSet, CommandId);  
            // Change to StartNotepad handler.  
            MenuCommand menuItem = new MenuCommand(this.StartNotepad, menuCommandID);  
            commandService.AddCommand(menuItem);  
        }  
    }  
    ```  
  
3. 删除 MenuItemCallback 方法并添加 StartNotepad 方法，该方法将只启动记事本：  
  
    ```csharp  
    private void StartNotepad(object sender, EventArgs e)  
    {  
        Process proc = new Process();  
        proc.StartInfo.FileName = "notepad.exe";  
        proc.Start();  
    }  
    ```  
  
4. 现在试试看。当你开始调试项目并单击 " **工具"/"调用 FirstCommand**" 时，你应该会看到 "记事本" 的实例。  
  
     您可以使用类的实例 <xref:System.Diagnostics.Process> 来运行任何可执行文件，而不只是记事本。 例如，尝试 calc.exe。  
  
## <a name="cleaning-up-the-experimental-environment"></a>清理实验环境  
 如果要开发多个扩展，或者只是使用不同版本的扩展代码浏览结果，则试验环境可能会以它的方式停止工作。 在这种情况下，应运行重置脚本。 它被称为 **Reset Visual studio 2015 实验实例**，并作为 VISUAL studio SDK 的一部分提供。 此脚本从实验环境中删除对扩展的所有引用，以便可以从头开始。  
  
 可以通过以下两种方式之一访问此脚本：  
  
1. 在桌面上，查找 **"重置 Visual Studio 2015 实验实例"**。  
  
2. 从命令行运行以下命令：  
  
    ```  
    <VSSDK installation>\VisualStudioIntegration\Tools\Bin\CreateExpInstance.exe /Reset /VSInstance=14.0 /RootSuffix=Exp && PAUSE  
  
    ```  
  
## <a name="deploying-your-extension"></a>部署扩展  
 现在，你已使用所需的方式运行了你的工具扩展，接下来可以考虑将它与朋友和同事共享。 这很简单，只要安装了 Visual Studio 2015。 你需要做的就是向其发送生成的 .vsix 文件。  (确保在发布模式下生成它。 )   
  
 可以在 FirstMenuCommand bin 目录中找到此扩展的 .vsix 文件。 具体而言，假设你已经生成了版本配置，它将位于：  
  
 **\<code directory>\FirstMenuCommand\FirstMenuCommand\bin\Release\ FirstMenuCommand**  
  
 若要安装该扩展，您的朋友需要关闭 Visual Studio 的所有打开的实例，然后双击 .vsix 文件，该文件将显示 **Vsix 安装程序**。 文件将复制到 **%LocalAppData%\Microsoft\VisualStudio\14.0\Extensions** 目录中。  
  
 当您的朋友再次出现 Visual Studio 时，他将在 " **工具/扩展和更新**" 中找到 FirstMenuCommand 扩展。 他还可以通过 " **扩展和更新** " 来卸载或禁用该扩展。  
  
## <a name="next-steps"></a>后续步骤  
 本演练仅介绍了使用 Visual Studio 扩展可以执行的操作的一小部分。 下面是可以使用 Visual Studio 扩展执行的更简单的其他 () 操作的简短列表：  
  
1. 您可以使用一个简单的菜单命令来执行更多操作：  
  
   1. 添加自己的图标：向 [菜单命令添加图标](../extensibility/adding-icons-to-menu-commands.md)  
  
   2. 更改菜单命令的文本： [更改菜单命令的文本](../extensibility/changing-the-text-of-a-menu-command.md)  
  
   3. 添加命令的菜单快捷方式：将 [键盘快捷方式绑定到菜单项](../extensibility/binding-keyboard-shortcuts-to-menu-items.md)  
  
2. 添加不同种类的命令、菜单和工具栏： [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)  
  
3. 添加工具窗口并扩展内置 Visual Studio 工具窗口： [扩展和自定义工具窗口](../extensibility/extending-and-customizing-tool-windows.md)  
  
4. 将 IntelliSense、代码建议和其他功能添加到现有代码编辑器： [扩展编辑器和语言服务](../extensibility/extending-the-editor-and-language-services.md)  
  
5. 向扩展添加选项和属性页和用户设置： [扩展属性和属性窗口](../extensibility/extending-properties-and-the-property-window.md) 以及 [扩展用户设置和选项](../extensibility/extending-user-settings-and-options.md)  
  
   其他类型的扩展需要更多的工作，例如创建新类型的项目 ([扩展项目](../extensibility/extending-projects.md)) 、创建新类型的编辑器 ([创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)) 或在独立 shell 中实现扩展： [Visual Studio 独立 shell](../extensibility/visual-studio-isolated-shell.md)
