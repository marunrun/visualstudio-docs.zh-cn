---
title: 常见问题解答：将外接程序转换为 VSPackage 扩展 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: 3a01d333-6e31-423f-ae06-5091a4fcb7a9
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bc6ed31f96fc2021d0d9e104692f0440cfb78a5e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840689"
---
# <a name="faq-converting-add-ins-to-vspackage-extensions"></a>常见问题：将外接程序转换为 VSPackage 扩展
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

外接程序现在已弃用。 若要创建新的 Visual Studio 扩展，需要创建 VSIX 扩展。 下面是有关如何将 Visual Studio 外接程序转换为 VSIX 扩展的一些常见问题的解答。  
  
> [!WARNING]
> 从 Visual Studio 2015 开始，适用于 c # 和 Visual Basic 项目，你可以使用 VSIX 项目并添加菜单命令、工具窗口和 Vspackage 的项模板。 有关详细信息，请参阅 [Visual Studio 2015 SDK 的新增功能](../extensibility/what-s-new-in-the-visual-studio-2015-sdk.md)。  
  
> [!IMPORTANT]
> 在许多情况下，只需将外接程序代码传输到具有 VSPackage 项目项的 VSIX 项目。 你可以通过在 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 方法中调用 <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> 获取 DTE 自动化对象。  
>   
> `DTE2 dte = (DTE2)GetService(typeof(DTE));`  
>   
> 有关详细信息，请参阅下面 [的如何在 VSPackage 中运行外接程序代码？](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_RunAddin) 。  
  
## <a name="what-software-do-i-need-to-develop-vsix-extensions"></a>开发 VSIX 扩展需要什么软件？  
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 也可稍后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。  
  
## <a name="wheres-the-extension-documentation"></a>扩展文档在哪里？  
 开始 [开发 Visual Studio 扩展](../extensibility/starting-to-develop-visual-studio-extensions.md)。 有关 MSDN 上的 VSSDK 扩展开发的其他文章，请阅读此文。  
  
## <a name="can-i-convert-my-add-in-project-to-a-vsix-project"></a>是否可以将外接程序项目转换为 VSIX 项目？  
 外接程序项目无法直接转换为 VSIX 项目，因为 VSIX 项目中使用的机制与外接程序项目中使用的机制不同。 VSIX 项目模板和正确的项目项模板都有很多代码，使其相对容易地作为 VSIX 扩展启动和运行。  
  
## <a name="how-do-i-start-developing-vsix-extensions"></a><a name="BKMK_StartDeveloping"></a> 如何实现开始开发 VSIX 扩展？  
 下面介绍了如何生成具有菜单命令的 VSIX：  
  
#### <a name="to-make-a-vsix-extension-that-has-a-menu-command"></a>创建具有菜单命令的 VSIX 扩展  
  
1. 创建 VSIX 项目。  ("**快速启动**" 窗口中的 "**文件**"、"**新建**"、"**项目**" 或 "类型"**项目**) 。 在 " **新建项目** " 对话框中，展开 " **Visual c #/扩展性** " 或 " **Visual Basic/扩展性** "，然后选择 " **VSIX 项目**"。 ) 将项目命名为 **TestExtension** 并指定其位置。  
  
2. 添加 **自定义命令** 项目项模板。  (右键单击 **解决方案资源管理器** 中的项目节点，然后选择 " **添加/新建项**"。 在 Visual c # 或 Visual Basic 的 " **新建项目** " 对话框中，选择 " **扩展性** " 节点，然后选择 " **自定义命令**"。 )   
  
3. 按 F5 以在调试模式下生成并运行项目。  
  
     将出现 Visual Studio 的第二个实例。 此第二个实例称为实验实例，它具有的设置可能与你要用来编写代码的 Visual Studio 实例的设置不相同。 第一次运行实验实例时，系统将要求你登录到 VS Online 并指定你的主题和配置文件。  
  
     在实验实例中的 " **工具** " 菜单 (上) 应该会看到一个名为 **"我的命令名"** 的按钮。 选择此按钮时，将显示一条消息： **TestVSPackagePackage. MenuItemCallback ( # B1 **。  
  
## <a name="how-can-i-run-my-add-in-code-in-a-vspackage"></a><a name="BKMK_RunAddin"></a> 如何在 VSPackage 中运行外接程序代码？  
 通常采用以下两种方式之一来运行外接程序代码：  
  
- 由菜单命令触发（代码位于 `IDTCommandTarget.Exec` 方法中）  
  
- 启动时自动运行（代码位于 `OnConnection` 事件处理程序中。）  
  
  你可以在 VSPackage 中执行相同的操作。 以下显示了如何将一些外接程序代码添加到回调方法中：  
  
#### <a name="to-implement-a-menu-command-in-a-vspackage"></a>在 VSPackage 中实现菜单命令  
  
1. 创建具有菜单命令的 VSPackage。  (有关详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。 )   
  
2. 打开包含 VSPackage 定义的文件。  (在 c # 项目中，它是 <em>\<your project name></em> Package.cs。 )   
  
3. 向文件添加以下 `using` 语句：  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. 查找 `MenuItemCallback` 方法。 添加对 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 的调用以获取 <xref:EnvDTE80.DTE2> 对象：  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. 添加外接程序在其 `IDTCommandTarget.Exec` 方法中所具有的代码。 例如，以下代码将新窗格添加到 " **输出** " 窗口，并在新窗格中打印 "某些文本"。  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)  
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));  
       OutputWindow outputWindow = dte.ToolWindows.OutputWindow;  
  
       OutputWindowPane outputWindowPane = outputWindow.OutputWindowPanes.Add("A New Pane");  
       outputWindowPane.OutputString("Some Text");  
   }  
  
   ```  
  
6. 生成并运行此项目。 按 F5 或在 "**调试**" 工具栏上选择 "**启动**"。 在 Visual Studio 的实验实例中，" **工具** " 菜单应该具有一个名为 **"我的命令名"** 的按钮。 当您选择此按钮时， **一些文本** 将显示在 " **输出** " 窗口窗格中。  (可能需要打开 " **输出** " 窗口。 )   
  
   你还可以使代码在启动时运行。 但是，通常反对将此方法用于 VSPackage 扩展。 如果在 Visual Studio 启动时尝试加载太多扩展，则启动时间可能会明显加长。 更好的方法是，仅在满足一些条件（例如打开解决方案）时才自动加载 VSPackage。  
  
   此过程显示了如何在打开解决方案时自动加载的 VSPackage 中运行外接程序代码：  
  
#### <a name="to-autoload-a-vspackage"></a>自动加载 VSPackage  
  
1. 使用 Visual Studio 包项目项创建 VSIX 项目。  (执行此操作的步骤，请参阅 [如何实现开始开发 VSIX 扩展？](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping)。 只需添加 **Visual Studio 包** 项目项即可。 ) 将 VSIX 项目命名为 **TestAutoload**。  
  
2. 打开 TestAutoloadPackage.cs。 查找声明程序包类所在的行：  
  
   ```csharp  
   public sealed class <name of your package>Package : Package  
   ```  
  
3. 此行上方是一组特性。 添加此特性：  
  
   ```csharp  
   [ProvideAutoLoad(UIContextGuids80.SolutionExists)]  
   ```  
  
4. 在 `Initialize()` 方法中设置断点并启动调试 (F5)。  
  
5. 在实验实例中，打开一个项目。 应该加载 VSPackage，并且应该命中断点。  
  
   通过使用 <xref:Microsoft.VisualStudio.Shell.Interop.UIContextGuids80> 的字段，可指定要在其中加载你的 VSPackage 的其他上下文。 有关详细信息，请参阅 [加载 vspackage](../extensibility/loading-vspackages.md)。  
  
## <a name="how-can-i-get-the-dte-object"></a>如何获取 DTE 对象？  
 如果你的外接程序无法显示 UI（例如，菜单命令、工具栏按钮或工具窗口），则只要你从 VSPackage 中获取 DTE 自动化对象，你可能就能够按原样使用代码。 下面介绍如何操作：  
  
#### <a name="to-get-the-dte-object-from-a-vspackage"></a>从 VSPackage 中获取 DTE 对象  
  
1. 在具有 Visual Studio 包项模板的 VSIX 项目中，查找 <em>\<project name></em> Package.cs 文件。 这是派生自 <xref:Microsoft.VisualStudio.Shell.Package> 的类；它可以帮助你与 Visual Studio 进行交互。 在这种情况下，请使用其 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 来获取 <xref:EnvDTE80.DTE2> 对象。  
  
2. 添加以下 `using` 语句：  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
3. 查找 `Initialize` 方法。 此方法将处理你在程序包向导中指定的命令。 添加对 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 的调用以获取 DTE 对象：  
  
   ```csharp  
   DTE dte = (DTE)GetService(typeof(DTE));  
   ```  
  
   拥有 <xref:EnvDTE.DTE> 自动化对象之后，你可以将其余的外接程序代码添加到项目中。 如果你需要 <xref:EnvDTE80.DTE2> 对象，你可以执行相同的操作。  
  
## <a name="how-do-i-change-menu-commands-and-toolbar-buttons-in-my-add-in-to-the-vspackage-style"></a>如何将我的外接程序中的菜单命令和工具栏按钮更改为 VSPackage 样式？  
 VSPackage 扩展使用 .vsct 文件创建大多数菜单命令、工具栏、工具栏按钮和其他 UI。 **自定义命令**项目项模板提供了在 "**工具**" 菜单上创建命令的选项。 有关详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
 有关 .vsct 文件的详细信息，请参阅 [如何 Vspackage 添加用户界面元素](../extensibility/internals/how-vspackages-add-user-interface-elements.md)。 有关演示如何使用 .vsct 文件添加菜单项、工具栏和工具栏按钮的演练，请参阅 [扩展菜单和命令](../extensibility/extending-menus-and-commands.md)。  
  
## <a name="how-do-i-add-custom-tool-windows-in-the-vspackage-way"></a>如何采用 VSPackage 方式添加自定义工具窗口？  
 自定义工具窗口项目项模板提供了创建工具窗口的选项。 有关此项目项模板的详细信息，请参阅 [使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。 有关工具窗口的信息，请参阅 [扩展和自定义工具窗口](../extensibility/extending-and-customizing-tool-windows.md) 及其下的文章，尤其是 [添加工具窗口](../extensibility/adding-a-tool-window.md)。  
  
## <a name="how-do-i-manage-visual-studio-windows-in-the-vspackage-way"></a>如何采用 VSPackage 方式管理 Visual Studio 窗口？  
 如果你的外接程序管理 Visual Studio 窗口，则外接程序代码应该在 VSPackage 中有效。 例如，此过程演示如何将管理 **任务列表** 的代码添加到 `MenuItemCallback` VSPackage 的方法中。  
  
#### <a name="to-insert-window-management-code-from-an-add-in-into-a-vspackage"></a>将外接程序中的窗口管理代码插入到 VSPackage 中  
  
1. 创建具有菜单命令的 VSPackage，如 [如何实现开始开发 VSIX 扩展？ "](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping) 一节中所示。  
  
2. 打开包含 VSPackage 定义的文件。  (在 c # 项目中，它是 <em>\<your project name></em> Package.cs。 )   
  
3. 添加以下 `using` 语句：  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. 查找 `MenuItemCallback` 方法。 添加对 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 的调用以获取 <xref:EnvDTE80.DTE2> 对象：  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. 添加外接程序中的代码。 例如，以下代码将新任务添加到 **任务列表**，列出任务数，然后删除一个任务。  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)   
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));   
  
       TaskList tl = (TaskList)dte.ToolWindows.TaskList;   
       askItem tlItem;   
  
       // Add a couple of tasks to the Task List.   
       tlItem = tl.TaskItems.Add(" ", " ", "Test task 1.",    
           vsTaskPriority.vsTaskPriorityHigh, vsTaskIcon.vsTaskIconUser,   
           true, "", 10, true, true);  
       tlItem = tl.TaskItems.Add(" ", " ", "Test task 2.",   
           vsTaskPriority.vsTaskPriorityLow, vsTaskIcon.vsTaskIconComment, true, "", 20, true,true);  
  
       // List the total number of task list items after adding the new task items.  
       System.Windows.Forms.MessageBox.Show("Task Item 1 description: "+tl.TaskItems.Item(2).Description);  
       System.Windows.Forms.MessageBox.Show("Total number of task items: "+tl.TaskItems.Count);   
  
       // Remove the second task item. The items list in reverse numeric order.   
       System.Windows.Forms.MessageBox.Show("Deleting the second task item");  
       tl.TaskItems.Item(2).Delete();  
       System.Windows.Forms.MessageBox.Show("Total number of task items: "+tl.TaskItems.Count);   
   }  
   ```  
  
## <a name="how-do-i-manage-projects-and-solutions-in-a-vspackage"></a>如何在 VSPackage 中管理项目和解决方案？  
 如果你的外接程序可以管理项目和解决方案，则外接程序代码应在 VSPackage 中有效。 例如，此过程显示了如何添加获取启动项目的代码。  
  
1. 创建具有菜单命令的 VSPackage，如 [如何实现开始开发 VSIX 扩展？ "](../extensibility/faq-converting-add-ins-to-vspackage-extensions.md#BKMK_StartDeveloping) 一节中所示。  
  
2. 打开包含 VSPackage 定义的文件。  (在 c # 项目中，它是 <em>\<your project name></em> Package.cs。 )   
  
3. 添加以下 `using` 语句：  
  
   ```csharp  
   using EnvDTE;  
   using EnvDTE80;  
   ```  
  
4. 查找 `MenuItemCallback` 方法。 添加对 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 的调用以获取 <xref:EnvDTE80.DTE2> 对象：  
  
   ```csharp  
   DTE2 dte = (DTE2)GetService(typeof(DTE));  
   ```  
  
5. 添加外接程序中的代码。 例如，以下代码将获取解决方案中启动项目的名称。 （当此程序包运行时，多项目解决方案必须处于打开状态。）  
  
   ```csharp  
   private void MenuItemCallback(object sender, EventArgs e)  
   {  
       DTE2 dte = (DTE2) GetService(typeof(DTE));   
  
       SolutionBuild2 sb = (SolutionBuild2)dte.Solution.SolutionBuild;   
       Project startupProj;   
       string msg = "";  
  
       foreach (String item in (Array)sb.StartupProjects)   
       {  
           msg += item;   
       }  
       System.Windows.Forms.MessageBox.Show("Solution startup Project: "+msg);   
       startupProj = dte.Solution.Item(msg);   
       System.Windows.Forms.MessageBox.Show("Full name of solution's startup project: "+"/n"+startupProj.FullName);   
   }  
   ```  
  
## <a name="how-do-i-set-keyboard-shortcuts-in-a-vspackage"></a>如何在 VSPackage 中设置键盘快捷方式？  
 请使用 .vsct 文件的 `<KeyBindings>` 元素。 在以下示例中，命令 `idCommand1` 的键盘快捷方式是 Alt+A，命令 `idCommand2` 的键盘快捷方式是 Alt+Ctrl+A。 请注意键名的语法。  
  
```xml  
<KeyBindings>  
    <KeyBinding guid="MyProjectCmdSet" id="idCommand1" editor="guidVSStd97" key1="A" mod1="ALT" />  
    <KeyBinding guid="MyProjectCmdSet" id="idCommand2" editor="guidVSStd97" key1="A" mod1="CONTROL" mod2="ALT" />  
</KeyBindings>  
```  
  
## <a name="how-do-i-handle-automation-events-in-a-vspackage"></a>如何在 VSPackage 中处理自动化事件？  
 在 VSPackage 中采用与外接程序中相同的方法处理自动化事件。 以下代码显示了如何处理 `OnItemRenamed` 事件。 （本示例假设你已经获得 DTE 对象。）  
  
```csharp  
Events2 dteEvents = (Events2)dte.Events;  
dteEvents.ProjectItemsEvents.ItemRenamed += listener1.OnItemRenamed;   
. . .  
public void OnItemRenamed(EnvDTE.ProjectItem projItem, string oldName)   
{  
    string s = "[Event] Renamed " + oldName + " to " + Path.GetFileName(projItem.get_FileNames(1) + " in project " + projItem.ContainingProject.Name;   
}  
```
