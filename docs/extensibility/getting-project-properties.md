---
title: 获取项目属性 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- project properties, displaying in tool window
- tool windows, displaying project properties
ms.assetid: 96ba07ca-0811-4013-8602-12550ac4ba79
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7f766be25015081338b887a5b08413e77f5f17f9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342526"
---
# <a name="get-project-properties"></a>获取项目属性

本演练演示如何在工具窗口中显示项目属性。

## <a name="prerequisites"></a>系统必备

从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="to-create-a-vsix-project-and-add-a-tool-window"></a>若要创建 VSIX 项目并添加工具窗口

1. 每个 Visual Studio 扩展开始于 VSIX 部署项目，它将包含扩展资产。 创建[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]VSIX 项目名为`ProjectPropertiesExtension`。 您可以发现中的 VSIX 项目模板**新的项目**通过搜索"vsix"对话框。

2. 通过添加一个名为的自定义工具窗口项模板添加工具窗口`ProjectPropertiesToolWindow`。 在中**解决方案资源管理器**，右键单击项目节点并选择**添加** > **新项**。 在中**添加新项对话框**，请转到**Visual C# 项** > **扩展性**，然后选择**自定义工具窗口**。 在中**名称**在对话框底部字段中，将文件名称更改为`ProjectPropertiesToolWindow.cs`。 有关如何创建自定义工具窗口的详细信息，请参阅[与工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

3. 生成解决方案并确认编译时不会产生错误。

### <a name="to-display-project-properties-in-a-tool-window"></a>若要在工具窗口中显示项目属性

1. 在 ProjectPropertiesToolWindowCommand.cs 文件中，添加以下 using 语句。

    ```csharp
    using EnvDTE;
    using System.Windows.Controls;

    ```

2. 在中*ProjectPropertiesToolWindowControl.xaml*，删除现有按钮并从工具箱添加 TreeView。 您还可以删除 click 事件处理程序从*ProjectPropertiesToolWindowControl.xaml.cs*文件。

3. 在中*ProjectPropertiesToolWindowCommand.cs*，使用`ShowToolWindow()`方法来打开该项目并读取其属性，然后将属性添加到树视图。 ShowToolWindow 的代码应如下所示：

    ```csharp
    private void ShowToolWindow(object sender, EventArgs e)
    {
        ToolWindowPane window = this.package.FindToolWindow(typeof(ProjectPropertiesToolWindow), 0, true);
        if ((null == window) || (null == window.Frame))
        {
            throw new NotSupportedException("Cannot create window.");
        }
        IVsWindowFrame windowFrame = (IVsWindowFrame)window.Frame;
        Microsoft.VisualStudio.ErrorHandler.ThrowOnFailure(windowFrame.Show());

        // Get the tree view and populate it if there is a project open.
        ProjectPropertiesToolWindowControl control = (ProjectPropertiesToolWindowControl)window.Content;
        TreeView treeView = control.treeView;

        // Reset the TreeView to 0 items.
        treeView.Items.Clear();

        DTE dte = (DTE)this.ServiceProvider.GetService(typeof(DTE));
        Projects projects = dte.Solution.Projects;
        if (projects.Count == 0)   // no project is open
        {
            TreeViewItem item = new TreeViewItem();
            item.Name = "Projects";
            item.ItemsSource = new string[]{ "no projects are open." };
            item.IsExpanded = true;
            treeView.Items.Add(item);
            return;
        }

        Project project = projects.Item(1);
        TreeViewItem item1 = new TreeViewItem();
        item1.Header = project.Name + "Properties";
        treeView.Items.Add(item1);

        foreach (Property property in project.Properties)
        {
            TreeViewItem item = new TreeViewItem();
            item.ItemsSource = new string[] { property.Name };
            item.IsExpanded = true;
            treeView.Items.Add(item);
        }
    }
    ```

4. 生成项目并启动调试。 应显示在实验实例。

5. 在实验实例中，打开一个项目。

6. 在中**视图** > **其他 Windows**单击**ProjectPropertiesToolWindow**。

  应会看到工具窗口以及名称和它的所有项目属性的第一个项目中的树控件。