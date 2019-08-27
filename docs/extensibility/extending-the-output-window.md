---
title: 扩展输出窗口 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Output window, about Output window
ms.assetid: b02fa88c-f92a-4ff6-ba5f-2eb4d48a643a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dd02ce74f2fee8255d92c47149a46f1003b02011
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66311027"
---
# <a name="extend-the-output-window"></a>扩展输出窗口
**输出**窗口是一组的读/写文本窗格。 Visual Studio 提供了这些内置窗格：**构建**，有关生成，消息通信中的项目和**常规**，在其中[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]将有关 IDE 的消息传递。 项目将获得对的引用**构建**窗格中会自动通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>接口方法和 Visual Studio 提供了直接访问权限**常规**窗格通过<xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane>服务。 除了内置的窗格中，可以创建和管理自己的自定义窗格。

 您可以控制**输出**窗口直接通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>接口。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>接口，由提供<xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow>服务，请定义用于创建、 检索和销毁方法**输出**窗口窗格。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>接口定义用于显示窗格中，隐藏窗格，和操作其文本的方法。 控制的替代方法**输出**窗口是通过<xref:EnvDTE.OutputWindow>和<xref:EnvDTE.OutputWindowPane>Visual Studio 自动化对象模型中的对象。 几乎所有的功能，这些对象将封装<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>接口。 此外，<xref:EnvDTE.OutputWindow>并<xref:EnvDTE.OutputWindowPane>对象添加一些更高级别的功能，以使其更轻松地枚举**输出**窗口窗格并从窗格中检索文本。

## <a name="create-an-extension-that-uses-the-output-pane"></a>创建使用输出窗格中的扩展
 您可以进行练习的输出窗格中的不同方面的扩展。

1. 创建一个名为的 VSIX 项目`TestOutput`菜单命令与名为**TestOutput**。 有关详细信息，请参阅[与菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 添加以下引用：

    1. EnvDTE

    2. EnvDTE80

3. 在中*TestOutput.cs*，添加以下 using 语句：

    ```f#
    using EnvDTE;
    using EnvDTE80;
    ```

4. 在中*TestOutput.cs*，删除`ShowMessageBox`方法。 添加以下方法存根 （stub）：

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
    }
    ```

5. 在 TestOutput 构造函数将更改为 OutputCommandHandler 的命令处理程序。 下面是将命令添加的部分：

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

6. 以下各节具有不同显示输出窗格中处理的不同方法的方法。 您可以调用这些方法的正文为`OutputCommandHandler()`方法。 例如，下面的代码添加`CreatePane()`下一节中给出的方法。

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
        CreatePane(new Guid(), "Created Pane", true, false);
    }
    ```

## <a name="create-an-output-window-with-ivsoutputwindow"></a>使用 IVsOutputWindow 创建输出窗口
 此示例演示如何创建一个新**输出**使用的窗口窗格<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>接口。

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

 如果将此方法添加到提供在前面部分中，单击时的扩展名**调用 TestOutput**命令应会看到**输出**窗口中的使用标头指出**显示输出从：CreatedPane**和文字**这是创建窗格**本身的窗格中。

## <a name="create-an-output-window-with-outputwindow"></a>使用 OutputWindow 创建输出窗口
 此示例演示如何创建**输出**使用的窗口窗格<xref:EnvDTE.OutputWindow>对象。

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
        panes.Add(title);
    }
}
```

 尽管<xref:EnvDTE.OutputWindowPanes>收集允许您检索**输出**窗口窗格中的通过其标题，窗格标题不能保证是唯一的。 如果您不能确定标题的唯一性，使用<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow.GetPane%2A>方法来检索正确窗格中的 GUID。

 如果将此方法添加到提供在前面部分中，单击时的扩展名**调用 TestOutput**命令可以看到输出窗口显示一个标头与**显示输出来源：DTEPane**和文字**添加 DTE 窗格**本身的窗格中。

## <a name="delete-an-output-window"></a>删除输出窗口
 此示例演示如何删除**输出**窗口窗格。

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

 如果将此方法添加到提供在前面部分中，单击时的扩展名**调用 TestOutput**命令可以看到输出窗口显示一个标头与**显示输出来源：新窗格**和文字**添加创建窗格**本身的窗格中。 如果单击**调用 TestOutput**同样，命令窗格中删除。

## <a name="get-the-general-pane-of-the-output-window"></a>获取输出窗口的常规窗格
 此示例演示如何获取内置**常规**窗格**输出**窗口。

```csharp
IVsOutputWindowPane GetGeneralPane()
{
    return (IVsOutputWindowPane)GetService(
        typeof(SVsGeneralOutputWindowPane));
}
```

 如果将此方法添加到提供在前面部分中，单击时的扩展名**调用 TestOutput**命令，您应该会看到**输出**窗口会显示单词**找到常规窗格**在窗格中。

## <a name="get-the-build-pane-of-the-output-window"></a>获取在生成窗格的输出窗口
 此示例演示如何查找**生成**窗格并向其写入。 由于**生成**窗格未激活默认情况下，它还将其激活。

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
