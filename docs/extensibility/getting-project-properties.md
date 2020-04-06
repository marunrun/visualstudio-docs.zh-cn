---
title: 获取项目属性 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- project properties, displaying in tool window
- tool windows, displaying project properties
ms.assetid: 96ba07ca-0811-4013-8602-12550ac4ba79
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9ddfd48827bc762c9189f9b7600cfe9200e5c866
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711412"
---
# <a name="get-project-properties"></a>获取项目属性

本演练演示如何在工具窗口中显示项目属性。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

### <a name="to-create-a-vsix-project-and-add-a-tool-window"></a>创建 VSIX 项目并添加工具窗口

1. 每个 Visual Studio 扩展都从 VSIX 部署项目开始，该项目将包含扩展资产。 创建[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]名为 的`ProjectPropertiesExtension`VSIX 项目。 您可以通过搜索"vsix"在 **"新项目**"对话框中找到 VSIX 项目模板。

2. 通过添加名为 的`ProjectPropertiesToolWindow`自定义工具窗口项模板来添加工具窗口。 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 在 **"添加新项目"对话框**中，转到**可视化 C# 项** > **扩展性**并选择 **"自定义工具窗口**"。 在对话框底部的 **"名称"** 字段中，将文件名更改为`ProjectPropertiesToolWindow.cs`。 有关如何创建自定义工具窗口的详细信息，请参阅[使用工具窗口创建扩展](../extensibility/creating-an-extension-with-a-tool-window.md)。

3. 生成解决方案并确认编译时不会产生错误。

### <a name="to-display-project-properties-in-a-tool-window"></a>在工具窗口中显示项目属性

1. 在ProjectPropertiesToolWindowCommand.cs文件中，使用指令添加以下指令。

    ```csharp
    using EnvDTE;
    using System.Windows.Controls;

    ```

2. 在*ProjectPropertiesToolWindowControl.xaml 中*，删除现有按钮并从工具箱中添加树视图。 您还可以从*ProjectPropertiesToolWindowControl.xaml.cs*文件中删除单击事件处理程序。

3. 在*ProjectPropertiesToolWindowCommand.cs*中使用`ShowToolWindow()`方法打开项目并读取其属性，然后将属性添加到 TreeView。 ShowToolWindow 的代码应如下所示：

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

4. 生成项目并启动调试。 应出现实验实例。

5. 在实验实例中，打开一个项目。

6. 在 **"查看** > **其他窗口**"中单击 **"项目属性工具窗口**"。

  您应该在工具窗口中看到树控件以及第一个项目及其所有项目属性的名称。
