---
title: 创建 WPF 工具箱控件 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- toolbox control
- toolbox
- wpf
ms.assetid: 9cc34db9-b0d1-4951-a02f-7537fbbb51ad
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fc124c767ac9a84e62c17fb868e1dc114642f884
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349031"
---
# <a name="create-a-wpf-toolbox-control"></a>创建 WPF 工具箱控件

WPF (Windows Presentation Framework) 工具箱控件模板允许你创建的自动添加到 WPF 控件**工具箱**时安装该扩展。 本演练演示如何使用模板创建**工具箱**可以分发给其他用户的控件。

从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-the-toolbox-control"></a>创建工具箱控件

### <a name="create-an-extension-with-a-wpf-toolbox-control"></a>使用 WPF 工具箱控件创建的扩展

1. 创建一个名为的 VSIX 项目`MyToolboxControl`。 您可以发现中的 VSIX 项目模板**新的项目**通过搜索"vsix"对话框。

2. 项目打开后，添加**WPF 工具箱控件**项模板名为`MyToolboxControl`。 在中**解决方案资源管理器**，右键单击项目节点并选择**添加** > **新项**。 在中**添加新项**对话框中，转到**Visual C#**  > **扩展性**，然后选择**WPF 工具箱控件**。 在中**名称**在窗口底部字段中，将命令文件名称更改为*MyToolboxControl.cs*。

    解决方案现在包含一个用户控件， `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute>添加到控件**工具箱**，和一个**Microsoft.VisualStudio.ToolboxControl**资产的 VSIX 清单中的项 部署。

#### <a name="to-create-the-control-ui"></a>若要创建 UI 控件

1. 打开*MyToolboxControl.xaml*在设计器中。

    此设计器显示包含 <xref:System.Windows.Controls.Button> 控件的 <xref:System.Windows.Controls.Grid> 控件。

2. 排列网格布局。 当选择<xref:System.Windows.Controls.Grid>控制，蓝色的控件条显示在网格的顶部和左侧边缘上。 您可以添加到网格的行和列，方法是单击标题栏。

3. 向网格添加子控件。 可以将其从拖来定位子控件**工具箱**部分的网格中，或通过设置其`Grid.Row`和`Grid.Column`XAML 中的属性。 下面的示例将两个标签添加在顶部行的网格中，然后第二行上的按钮。

    ```xaml
    <Grid>
        <Label Grid.Row="0" Grid.Column="0" Name="label1" />
        <Label Grid.Row="0" Grid.Column="1" Name="label2" />
        <Button Name="button1" Click="button1_Click" Grid.Row="1" Grid.ColumnSpan="2" />
    </Grid>
    ```

## <a name="renaming-the-control"></a>重命名控件

 默认情况下，您的控件将出现在**工具箱**作为**MyToolboxControl**中名为的组**MyToolboxControl.MyToolboxControl**。 您可以更改这些名称在*MyToolboxControl.xaml.cs*文件。

1. 打开*MyToolboxControl.xaml.cs*在代码视图中。

2. 查找`MyToolboxControl`类，并将它重命名为 TestControl。 (若要执行此操作的最快方法是重命名类，然后选择**重命名**从上下文菜单，然后完成步骤。 (有关详细信息**重命名**命令，请参阅[重命名重构 (C# 中)](../ide/reference/rename.md)。)

3. 转到`ProvideToolboxControl`属性，更改到的第一个参数的值**测试**。 这是将包含中的控件的组的名称**工具箱**。

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

## <a name="build-test-and-deployment"></a>生成、 测试和部署

 当调试项目时，您应发现中安装此控件**工具箱**的 Visual Studio 的实验实例。

### <a name="to-build-and-test-the-control"></a>生成并测试控件

1. 重新生成项目并启动调试。

2. 在 Visual Studio 的新实例中，创建 WPF 应用程序项目。 请确保在 XAML 设计器处于打开状态。

3. 在“工具箱”  中查找控件，并将其拖动到设计图面上。

4. 开始调试 WPF 应用程序。

5. 验证显示控件。

### <a name="to-deploy-the-control"></a>部署控件

1. 生成测试的项目后，可以找到 *.vsix*文件中 * \bin\debug\*项目文件夹中的。

2. 可以通过双击而在本地计算机上安装 *.vsix*文件并按照安装过程。 若要卸载该控件，请转到**工具** > **扩展和更新**并查找控件扩展，然后单击**卸载**。

3. 上传 *.vsix*文件到网络或网站。

    如果您将文件上载到[Visual Studio Marketplace](https://marketplace.visualstudio.com/)网站，其他用户可以使用**工具** > **扩展和更新**在 Visual Studio 中查找联机控制并将其安装。
