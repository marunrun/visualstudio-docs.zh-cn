---
title: 扩展输出窗口 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Output window, about Output window
ms.assetid: b02fa88c-f92a-4ff6-ba5f-2eb4d48a643a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 800b443b079111d1d09fffdd900b246a020578f4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711647"
---
# <a name="extend-the-output-window"></a>扩展输出窗口
**输出**窗口是一组读/写文本窗格。 Visual Studio 具有这些内置窗格 **：Build**，其中项目会传达有关生成的消息，在 **"常规"** 中[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，它们传达有关 IDE 的消息。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>项目通过接口方法自动获得对 **"生成**"窗格的引用，Visual Studio 提供通过<xref:Microsoft.VisualStudio.Shell.Interop.SVsGeneralOutputWindowPane>服务直接访问 **"常规**"窗格。 除了内置窗格之外，您还可以创建和管理自己的自定义窗格。

 您可以通过<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>接口直接控制**输出**窗口。 <xref:Microsoft.VisualStudio.Shell.Interop.SVsOutputWindow>服务<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>提供的接口定义用于创建、检索和销毁**输出**窗口窗格的方法。 该<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>接口定义用于显示窗格、隐藏窗格和操作其文本的方法。 控制**输出**窗口的另一种方法是通过 Visual Studio <xref:EnvDTE.OutputWindow> <xref:EnvDTE.OutputWindowPane>自动化对象模型中 的 和 对象。 这些对象几乎封装了<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane>接口的所有功能。 此外，<xref:EnvDTE.OutputWindow>和<xref:EnvDTE.OutputWindowPane>对象添加了一些更高级别的功能，以便更轻松地枚举 **"输出**"窗口窗格并从窗格中检索文本。

## <a name="create-an-extension-that-uses-the-output-pane"></a>创建使用"输出"窗格的扩展
 可以进行扩展，以练习"输出"窗格的不同方面。

1. 创建`TestOutput`一个 VSIX 项目，该项目名为 **"测试输出**"的菜单命令。 有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 添加以下引用：

    1. EnvDTE

    2. EnvDTE80

3. 在*TestOutput.cs*中，添加以下使用语句：

    ```f#
    using EnvDTE;
    using EnvDTE80;
    ```

4. 在*TestOutput.cs*，删除`ShowMessageBox`方法。 添加以下方法存根：

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
    }
    ```

5. 在测试输出构造函数中，将命令处理程序更改为"输出命令处理程序"。 下面是添加命令的部分：

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

6. 以下各节具有不同的方法，这些方法显示了处理"输出"窗格的不同方法。 可以将这些方法调用方法的主体`OutputCommandHandler()`。 例如，以下代码添加下一`CreatePane()`节中给出的方法。

    ```csharp
    private void OutputCommandHandler(object sender, EventArgs e)
    {
        CreatePane(new Guid(), "Created Pane", true, false);
    }
    ```

## <a name="create-an-output-window-with-ivsoutputwindow"></a>使用 IV 输出窗口创建输出窗口
 此示例演示如何使用接口创建新的<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow>**"输出**"窗口窗格。

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

 如果将此方法添加到上一节中给出的扩展中，则单击 **"调用测试输出"** 命令时，应看到 **"输出"** 窗口，该窗口的标题显示 **："已创建窗格"** 和"**这是窗格本身中创建窗格"** 字样。

## <a name="create-an-output-window-with-outputwindow"></a>使用输出窗口创建输出窗口
 此示例演示如何使用<xref:EnvDTE.OutputWindow>对象创建**输出**窗口窗格。

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

 尽管<xref:EnvDTE.OutputWindowPanes>集合允许您按其标题检索 **"输出**"窗口窗格，但窗格标题不保证是唯一的。 当您怀疑标题的唯一性时，<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindow.GetPane%2A>请使用 方法按其 GUID 检索正确的窗格。

 如果将此方法添加到上一节中给出的扩展中，则单击 **"调用测试输出"** 命令时，应看到"输出"窗口，该窗口的标题显示**输出：DTEPane**和窗格本身**中添加的 DTE 窗格**。

## <a name="delete-an-output-window"></a>删除输出窗口
 此示例演示如何删除 **"输出"** 窗口窗格。

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

 如果将此方法添加到上一节中给出的扩展中，则单击 **"调用测试输出"** 命令时，应看到"输出"窗口，该窗口的标题显示 **："新窗格**"和窗格本身中**添加的"已创建窗格"** 字样。 如果再次单击 **"调用测试输出"** 命令，窗格将被删除。

## <a name="get-the-general-pane-of-the-output-window"></a>获取输出窗口的"常规"窗格
 此示例演示如何获取 **"输出"** 窗口的内置**常规**窗格。

```csharp
IVsOutputWindowPane GetGeneralPane()
{
    return (IVsOutputWindowPane)GetService(
        typeof(SVsGeneralOutputWindowPane));
}
```

 如果将此方法添加到上一节中给出的扩展项，则单击 **"调用测试输出"** 命令时，应看到 **"输出"** 窗口在窗格中显示单词 **"找到常规"窗格**。

## <a name="get-the-build-pane-of-the-output-window"></a>获取"输出"窗口的生成窗格
 此示例演示如何查找**生成**窗格并将其写入该窗格。 由于默认情况下不会激活 **"生成**"窗格，因此还会激活它。

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
