---
title: 创建 WPF 工具箱控件 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: how-to
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
ms.openlocfilehash: a6aa6051648e495e21f7954a737f7b572ce6a6f2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903943"
---
# <a name="create-a-wpf-toolbox-control"></a>创建 WPF 工具箱控件

WPF (Windows Presentation Framework) 工具箱控件模板允许您创建在安装扩展后自动添加到 " **工具箱** " 的 wpf 控件。 此演练演示如何使用模板创建可分发给其他用户的 **工具箱** 控件。

从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-the-toolbox-control"></a>创建工具箱控件

### <a name="create-an-extension-with-a-wpf-toolbox-control"></a>使用 WPF 工具箱控件创建扩展

1. 创建一个名为的 VSIX 项目 `MyToolboxControl` 。 可以通过搜索 "vsix" 在 " **新建项目** " 对话框中找到 VSIX 项目模板。

2. 当项目打开时，添加一个名为的 **WPF 工具箱控件** 项模板 `MyToolboxControl` 。 在**解决方案资源管理器**中，右键单击项目节点，然后选择 "**添加**  >  **新项**"。 在 "**添加新项**" 对话框中，单击 " **Visual c #**  >  **扩展性**"，然后选择 **"WPF 工具箱控件"**。 在窗口底部的 " **名称** " 字段中，将命令文件名更改为 *MyToolboxControl.cs*。

    解决方案现在包含一个用户控件，一个 `ProvideToolboxControlAttribute` <xref:Microsoft.VisualStudio.Shell.RegistrationAttribute> 将控件添加到 " **工具箱**" 中，将 " **VisualStudio. ToolboxControl** " 资产条目添加到部署的 VSIX 清单中。

#### <a name="to-create-the-control-ui"></a>创建控件 UI

1. 在设计器中打开 *MyToolboxControl* 。

    此设计器显示包含 <xref:System.Windows.Controls.Button> 控件的 <xref:System.Windows.Controls.Grid> 控件。

2. 排列网格布局。 选择 <xref:System.Windows.Controls.Grid> 控件时，网格的上边缘和左边缘将显示蓝色控件条。 您可以通过单击相应的栏向网格中添加行和列。

3. 将子控件添加到网格。 您可以通过将子控件从 **工具箱** 拖动到网格中的某个部分或通过 `Grid.Row` 在 XAML 中设置其和属性来定位子控件 `Grid.Column` 。 下面的示例将两个标签添加到网格的顶部行中，并在第二行添加一个按钮。

    ```xaml
    <Grid>
        <Label Grid.Row="0" Grid.Column="0" Name="label1" />
        <Label Grid.Row="0" Grid.Column="1" Name="label2" />
        <Button Name="button1" Click="button1_Click" Grid.Row="1" Grid.ColumnSpan="2" />
    </Grid>
    ```

## <a name="renaming-the-control"></a>重命名控件

 默认情况下，控件将在 "**工具箱**" 中显示为名为**MyToolboxControl MyToolboxControl**的组中的**MyToolboxControl** 。 可以在 *MyToolboxControl.xaml.cs* 文件中更改这些名称。

1. 在代码视图中打开 *MyToolboxControl.xaml.cs* 。

2. 找到 `MyToolboxControl` 类，然后将其重命名为 TestControl。  (最快的方法是重命名类，然后从上下文菜单中选择 " **重命名** " 并完成这些步骤。  (有关 " **重命名** " 命令的详细信息，请参阅 [重命名重构 (c # ) ](../ide/reference/rename.md)。 ) 

3. 转到 `ProvideToolboxControl` 属性，并更改第一个参数的值以进行 **测试**。 这是将在 " **工具箱**" 中包含控件的组的名称。

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

 调试项目时，应在 Visual Studio 的实验实例的 **工具箱** 中找到所安装的控件。

### <a name="to-build-and-test-the-control"></a>生成并测试控件

1. 重新生成项目并启动调试。

2. 在 Visual Studio 的新实例中，创建 WPF 应用程序项目。 请确保 XAML 设计器处于打开状态。

3. 在“工具箱” **** 中查找控件，并将其拖动到设计图面上。

4. 开始调试 WPF 应用程序。

5. 验证控件是否显示。

### <a name="to-deploy-the-control"></a>部署控件

1. 生成测试的项目后，可以在项目的 * \bin\debug 文件夹中找到 *.vsix*文件。 \*

2. 通过双击 *.vsix* 文件并按照安装过程进行操作，可以将其安装在本地计算机上。 若要卸载控件，请依次单击 "**工具**" "  >  **扩展和更新**" 和 "控件扩展"，然后单击 "**卸载**"。

3. 将 *.vsix* 文件上载到网络或网站。

    如果将文件上传到[Visual Studio Marketplace](https://marketplace.visualstudio.com/)网站，则其他用户可以使用**Tools**  >  Visual Studio 中的工具**扩展和更新**来联机查找控件并安装。
