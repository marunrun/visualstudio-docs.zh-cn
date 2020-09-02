---
title: 扩展输出窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Output window, about Output window
ms.assetid: b02fa88c-f92a-4ff6-ba5f-2eb4d48a643a
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2788903c60564d501770616fbe3ad2335e60a250
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204424"
---
# <a name="extending-the-output-window"></a>扩展输出窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

" **输出** " 窗口是一组读/写文本窗格。 Visual Studio 包含这些内置窗格： " **生成**"，其中的项目用于传达有关生成的消息 **，并传达**有关 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE 的消息。 项目通过接口方法自动获得对 " **生成** " 窗格的引用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> ，Visual Studio 通过服务提供对 **常规** 窗格的直接访问 <xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane> 。 除了内置窗格外，还可以创建和管理自己的自定义窗格。  
  
 您可以通过和接口直接控制 " **输出** " 窗口 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> 。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>接口由 <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow> 服务提供，用于定义用于创建、检索和销毁**输出**窗口窗格的方法。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>接口定义用于显示窗格、隐藏窗格和操作其文本的方法。 控制 " **输出** " 窗口的另一种方法是 <xref:EnvDTE.OutputWindow> 通过 <xref:EnvDTE.OutputWindowPane> Visual Studio 自动化对象模型中的和对象。 这些对象封装了和接口的几乎所有功能 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane> 。 此外， <xref:EnvDTE.OutputWindow> 和对象还 <xref:EnvDTE.OutputWindowPane> 添加了一些更高级别的功能，使您可以更轻松地枚举 " **输出** " 窗口窗格和从窗格中检索文本。  
  
## <a name="creating-an-extension-that-uses-the-output-pane"></a>创建使用 "输出" 窗格的扩展  
 您可以使用一个扩展来执行 "输出" 窗格的不同方面。  
  
1. `TestOutput`使用名为**为 testoutput.txt**的菜单命令创建一个名为的 VSIX 项目。 有关详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。  
  
2. 添加以下引用：  
  
    1. EnvDTE  
  
    2. EnvDTE80  
  
3. 在 TestOutput.cs 中，添加以下 using 语句：  
  
    ```f#  
    using EnvDTE;  
    using EnvDTE80;  
    ```  
  
4. 在 TestOutput.cs 中，删除 ShowMessageBox 方法。 添加以下方法存根：  
  
    ```csharp  
    private void OutputCommandHandler(object sender, EventArgs e)  
    {  
    }  
    ```  
  
5. 在为 testoutput.txt 构造函数中，将命令处理程序更改为 OutputCommandHandler。 下面是添加命令的部分：  
  
    ```csharp  
    OleMenuCommandService commandService = this.ServiceProvider.GetService(typeof(IMenuCommandService)) as OleMenuCommandService;  
    if (commandService != null)  
    {  
        CommandID menuCommandID = new CommandID(MenuGroup, CommandId);  
        EventHandler eventHandler = OutputCommandHandler;  
        MenuCommand menuItem = new MenuCommand(eventHandler, menuCommandID);  
        commandService.AddCommand(menuItem);  
    }  
    ```  
  
6. 以下各节提供了不同的方法，这些方法显示了处理输出窗格的不同方式。 可以将这些方法调用到 OutputCommandHandler ( # A1 方法的正文。 例如，以下代码将添加下一节中给出的 CreatePane ( # A1 方法。  
  
    ```csharp  
    private void OutputCommandHandler(object sender, EventArgs e)  
    {  
        CreatePane(new Guid(), "Created Pane", true, false);  
    }  
    ```  
  
## <a name="creating-an-output-window-with-ivsoutputwindow"></a>使用 IVsOutputWindow 创建输出窗口  
 此示例演示如何使用接口创建新的 " **输出** " 窗口窗格 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow> 。  
  
```csharp  
void CreatePane(Guid paneGuid, string title,   
    bool visible, bool clearWithSolution)  
{  
    IVsOutputWindow output =   
        (IVsOutputWindow)GetService(typeof(SVsOutputWindow));  
    IVsOutputWindowPane pane;  
  
    // Create a new pane.  
    output.CreatePane(  
        ref paneGuid,   
        title,   
        Convert.ToInt32(visible),   
        Convert.ToInt32(clearWithSolution));  
  
    // Retrieve the new pane.  
    output.GetPane(ref paneGuid, out pane);  
  
     pane.OutputString("This is the Created Pane \n");  
}  
```  
  
 如果将此方法添加到上一部分中给定的扩展，则在单击 " **调用为 testoutput.txt** " 命令时，应会看到 " **输出** " 窗口，其中标头 **显示 "显示输出来源： CreatedPane** " 和 "这是窗格中的 **已创建" 窗格** 。  
  
## <a name="creating-an-output-window-with-outputwindow"></a>使用 OutputWindow 创建输出窗口  
 此示例演示如何使用对象创建 " **输出** " 窗口窗格 <xref:EnvDTE.OutputWindow> 。  
  
```csharp  
void CreatePane(string title)  
{  
    DTE2 dte = (DTE2)GetService(typeof(DTE));  
    OutputWindowPanes panes =  
        dte.ToolWindows.OutputWindow.OutputWindowPanes;  
  
    try  
    {  
        // If the pane exists already, write to it.  
        panes.Item(title);  
    }  
    catch (ArgumentException)  
    {  
        // Create a new pane and write to it.  
        return panes.Add(title);  
    }  
}  
```  
  
 尽管 <xref:EnvDTE.OutputWindowPanes> 集合允许您按标题检索 " **输出** " 窗口窗格，但并不保证窗格标题是唯一的。 如果怀疑标题的唯一性，请使用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow.GetPane%2A> 方法通过其 GUID 检索正确的窗格。  
  
 如果将此方法添加到上一部分中给定的扩展，则单击 " **调用为 testoutput.txt** " 命令时，应会看到 "输出" 窗口，其中包含一个标头，该标头 **显示 "显示输出来源： DTEPane** " 和 "在窗格中添加词汇" **窗格** 。  
  
## <a name="deleting-an-output-window"></a>删除输出窗口  
 此示例演示如何删除 " **输出** " 窗口窗格。  
  
```csharp  
void DeletePane(Guid paneGuid)  
{  
    IVsOutputWindow output =  
    (IVsOutputWindow)ServiceProvider.GetService(typeof(SVsOutputWindow));  
  
    IVsOutputWindowPane pane;  
    output.GetPane(ref paneGuid, out pane);  
  
    if (pane == null)  
    {  
        CreatePane(paneGuid, "New Pane\n", true, true);  
    }  
     else  
    {  
        output.DeletePane(ref paneGuid);  
    }  
}  
```  
  
 如果将此方法添加到上一部分中给定的扩展，则单击 " **调用为 testoutput.txt** " 命令时，应会看到 "输出" 窗口，其中包含一个标头，其中 **显示 "显示输出来源：新建" 窗格** 和 "在窗格中添加的单词" **窗格** 。 如果再次单击 " **调用为 testoutput.txt** " 命令，该窗格将被删除。  
  
## <a name="getting-the-general-pane-of-the-output-window"></a>获取输出窗口的常规窗格  
 此示例演示如何获取 "**输出**" 窗口的内置**一般**窗格。  
  
```csharp  
void GetGeneralPane()  
{  
    return (IVsOutputWindowPane)GetService(  
        typeof(SVsGeneralOutputWindowPane));  
}  
```  
  
 如果将此方法添加到上一部分中给定的扩展，则单击 " **调用为 testoutput.txt** " 命令时，应会看到 " **输出** " 窗口显示了窗格中的 " **常规" 窗格** 。  
  
## <a name="getting-the-build-pane-of-the-output-window"></a>获取输出窗口的生成窗格  
 此示例演示如何查找生成窗格并向其写入。 由于默认情况下不会激活 "生成" 窗格，因此它也会激活它。  
  
```csharp  
void OutputTaskItemStringExExample(string buildMessage)  
{  
    EnvDTE80.DTE2 dte = (EnvDTE80.DTE2)ServiceProvider.GetService(typeof(EnvDTE.DTE));  
  
    EnvDTE.OutputWindowPanes panes =  
        dte.ToolWindows.OutputWindow.OutputWindowPanes;  
    foreach (EnvDTE.OutputWindowPane pane in panes)  
        {  
            if (pane.Name.Contains("Build"))  
            {  
                pane.OutputString(buildMessage + "\n");  
                pane.Activate();  
                return;  
             }  
        }  
}  
```
