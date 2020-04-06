---
title: 创建 WPF 工具箱控件 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- toolbox control
- toolbox
- wpf
ms.assetid: 9cc34db9-b0d1-4951-a02f-7537fbbb51ad
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c1400efb0095760bf1cee302dd33dcf6ebb90152
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739566"
---
# <a name="create-a-wpf-toolbox-control"></a>创建 WPF 工具箱控件

通过 WPF（Windows 演示框架）工具箱控制模板，您可以创建在安装扩展名时自动添加到**工具箱**中的 WPF 控件。 本演练演示如何使用模板创建可分发给其他用户**的工具箱**控件。

从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-the-toolbox-control"></a>创建工具箱控件

### <a name="create-an-extension-with-a-wpf-toolbox-control"></a>使用 WPF 工具箱控件创建扩展

1. 创建名为 的`MyToolboxControl`VSIX 项目。 您可以通过搜索"vsix"在 **"新项目**"对话框中找到 VSIX 项目模板。

2. 打开项目时，添加名为`MyToolboxControl`**的 WPF 工具箱控制**项模板。 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** > **项**"。 在 **"添加新项目"** 对话框中，转到**可视化 C#** > **可扩展性**并选择**WPF 工具箱控件**。 在窗口底部的 **"名称"** 字段中，将命令文件名更改为*MyToolboxControl.cs*。

    该解决方案现在包含一个用户控件，一`ProvideToolboxControlAttribute`<xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>个将控件添加到**工具箱**，以及**Microsoft.VisualStudio.Toolbox 控制**资产条目，用于部署。

#### <a name="to-create-the-control-ui"></a>创建控件 UI

1. 在设计器中打开*MyToolboxControl.xaml。*

    此设计器显示包含 <xref:System.Windows.Controls.Button> 控件的 <xref:System.Windows.Controls.Grid> 控件。

2. 排列网格布局。 选择<xref:System.Windows.Controls.Grid>控件时，蓝色控制栏将显示在网格的顶部和左边缘。 您可以通过单击条形来向网格添加行和列。

3. 将子控件添加到网格。 可以通过将子控件从**工具箱**拖动到网格的一部分，或者通过在 XAML 中设置其`Grid.Row`和`Grid.Column`属性来定位子控件。 下面的示例在网格的顶行上添加两个标签，在第二行上添加一个按钮。

    ```xaml
    <Grid>
        <Label Grid.Row="0" Grid.Column="0" Name="label1" />
        <Label Grid.Row="0" Grid.Column="1" Name="label2" />
        <Button Name="button1" Click="button1_Click" Grid.Row="1" Grid.ColumnSpan="2" />
    </Grid>
    ```

## <a name="renaming-the-control"></a>重命名控件

 默认情况下，您的控件将显示在名为**MyToolboxControl.MyToolbox 控制**组中的 **"我的工具箱控制"工具箱中**。 **Toolbox** 您可以在*MyToolboxControl.xaml.cs*文件中更改这些名称。

1. 在代码视图中打开*MyToolboxControl.xaml.cs。*

2. 查找类`MyToolboxControl`并将其重命名为测试控制。 （执行此操作的最快方法是重命名类，然后从上下文菜单中选择 **"重命名**"并完成这些步骤。 （有关**重命名**命令的详细信息，请参阅[重命名重构 （C#）](../ide/reference/rename.md)。

3. 转到 属性`ProvideToolboxControl`并将第一个参数的值更改为 **"测试**"。 这是将在**工具箱**中包含控件的组的名称。

    生成的代码应如下所示：

    ```csharp
    [ProvideToolboxControl("Test", true)]
    public partial class TestControl : UserControl
    {
        public TestControl()
        {
            InitializeComponent();
        }
    }
    ```

## <a name="build-test-and-deployment"></a>生成、测试和部署

 调试项目时，应找到安装在 Visual Studio 实验实例**工具箱**中的控件。

### <a name="to-build-and-test-the-control"></a>生成并测试控件

1. 重建项目并开始调试。

2. 在 Visual Studio 的新实例中，创建 WPF 应用程序项目。 确保 XAML 设计器处于打开状态。

3. 在“工具箱” **** 中查找控件，并将其拖动到设计图面上。

4. 开始调试 WPF 应用程序。

5. 验证控件是否出现。

### <a name="to-deploy-the-control"></a>部署控件

1. 生成测试项目后，您可以在项目的 _bin_调试\*文件夹中找到 *.vsix*文件。

2. 您可以通过双击 *.vsix*文件并遵循安装过程将其安装在本地计算机上。 要卸载控件，请转到 **"工具** > **扩展"和"更新"** 并查找控件扩展，然后单击"**卸载**"。

3. 将 *.vsix*文件上载到网络或网站。

    如果将文件上载到[可视化工作室应用商店](https://marketplace.visualstudio.com/)网站，其他用户可以使用 Visual Studio 中的**工具** > **扩展和更新**联机查找控件并安装它。
