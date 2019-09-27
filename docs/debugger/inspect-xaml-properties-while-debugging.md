---
title: 在调试时检查 XAML 属性 |Microsoft Docs
ms.date: 03/06/2017
ms.topic: conceptual
ms.assetid: 390edde4-7b8d-4c89-8d69-55106b7e6b11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 182c9e37764a247ec24b4b477975ccb7b8811c4b
ms.sourcegitcommit: 4d2620bee4688fb881e09a07ea4a264b99f0743e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71322550"
---
# <a name="inspect-xaml-properties-while-debugging"></a>在调试时检查 XAML 属性
通过“实时可视化树”和“实时属性资源管理器”，可以获取正在运行 XAML 代码的实时视图。 这些工具为你提供了正在运行的 XAML 应用程序的 UI 元素的树视图，并显示你选择的任何 UI 元素的运行时属性。

可以在下列配置中使用这些工具：

|应用类型|操作系统和工具|
|-----------------|--------------------------------|
|Windows Presentation Foundation（4.0 和更高版本）应用程序|Windows 7 和更高版本|
|通用 Windows 应用|Windows 10 及更高版本的[windows 10 SDK](https://dev.windows.com/en-us/downloads/windows-10-sdk)|

## <a name="looking-at-elements-in-the-live-visual-tree"></a>查看实时可视化树中的元素
我们来看看一个非常简单的 WPF 应用程序，该应用程序包含一个列表视图和一个按钮。 每次单击按钮时，另一个项将添加到列表中。 偶数项以灰色显示，奇数项以黄色显示。

创建新 C# WPF 应用程序（“文件”/“新建”/“项目”，然后选择 C# 并查找 WPF 应用程序）。 将其命名为 TestXAML。

将 MainWindow.xaml 更改为以下内容：

```xaml
<Window x:Class="TestXAML.MainWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    xmlns:local="clr-namespace:TestXAML"
    mc:Ignorable="d"
    Title="MainWindow" Height="350" Width="525">
    <Grid>
        <Button x:Name="button" Background="LightBlue" Content="Add Item" HorizontalAlignment="Left" Margin="216,206,0,0" VerticalAlignment="Top" Width="75" Click="button_Click"/>
        <ListBox x:Name="listBox" HorizontalAlignment="Left" Height="100" VerticalAlignment="Top" Width="100" Margin="205,80,0,0"/>
    </Grid>
</Window>
```

将下面的命令处理程序添加到 MainWindow.xaml.cs 文件中：

```csharp
int count;

private void button_Click(object sender, RoutedEventArgs e)
{
    ListBoxItem item = new ListBoxItem();
    item.Content = "Item" + ++count;
    if (count % 2 == 0)
    {
        item.Background = Brushes.LightGray;
    }
    else
    {
        item.Background = Brushes.LightYellow;
    }
    listBox.Items.Add(item);
}
```

生成项目并启动调试。 （生成配置必须为“调试”，而不是“发布”。 有关生成配置的详细信息，请参阅[了解生成配置](../ide/understanding-build-configurations.md)。）

当窗口出现时，单击“添加项”按钮两次。 将显示如下所示的内容：

![应用的主窗口](../debugger/media/livevisualtree-app.png "LiveVIsualTree-应用")

现在打开“实时可视化树”窗口（“调试”>“Windows”>“实时可视化树”，或沿 IDE 左侧查找它）。 将其拖离其停靠位置以便我们可以并排查看此窗口和“实时属性”窗口。 在“实时可视化树”窗口中，展开 ContentPresenter 节点。 它应包含按钮和列表框的节点。 展开该列表框（然后展开 ScrollContentPresenter 和 ItemsPresenter）以查找列表框各项。 该窗口应如下所示：

![实时可视化树中的 listboxitem](../debugger/media/livevisualtree-listboxitems.png "LiveVisualTree-listboxitem")

返回到应用程序窗口并再添加几个项。 “实时可视化树”中应会显示更多列表框项。

现在让我们看看其中一个列表框项的属性。 选择“实时可视化树”中的第一个列表框项并单击工具栏上的“显示属性”图标。 应显示“实时属性资源管理器”。 请注意，"**内容**" 字段是 "Item1"，**背景** > **色**字段 **#FFFFFFE0**。 返回到“实时可视化树”，然后选择第二个列表框项。 "**实时属性资源管理器**" 应显示 "**内容**" 字段是 "Item2"，并且 **#FFD3D3D3** **背景** > **色**字段。

> [!NOTE]
> **实时属性资源管理器**中的属性周围的黄色边框表示属性值是通过绑定（如`Color = {BindingExpression}`）设置的。 绿色边框表示使用资源（如`Color = {StaticResource MyBrush}`）设置该值。

XAML 的实际结构具有大量你可能并不直接感兴趣的元素，并且如果不熟悉代码，可能很难导航树以查找正在寻找的内容。 因此“实时可视化树”有几种方法可使用应用程序的 UI 来帮助找到想要检查的元素。

在运行的应用程序中启用选择。 当选择“实时可视化树”工具栏上最左侧的按钮时，可以启用此模式。 在此模式下，可以在应用程序中选择 UI 元素，并且“实时可视化树”（以及“实时属性查看器”）会自动更新以显示对应于该元素及其属性的树中的节点。

在运行的应用程序中显示布局装饰器。 当选择“启用选择”按钮右侧紧靠的按钮时，可以启用此模式。 当“显示布局装饰器”打开时，它会导致应用程序窗口沿所选对象的边界显示水平线和垂直线，以便看到它与什么对齐，以及显示边距的矩形。 例如，打开“启用选择”和“显示布局”这两项，然后选择应用程序中的“添加项”文本块。 应看到“实时可视化树”中的文本块节点和“实时属性查看器”中的文本块属性，以及文本块边界上的水平线和垂直线。

![DisplayLayout 中的 displaylayout](../debugger/media/livevisualtreelivepropertyviewer-displaylayout.png "LiveVisualTreeLivePropertyViewer-DisplayLayout")

预览所选内容。 你可以通过选择“实时可视化树”工具栏上从左侧起第三个按钮来启用此模式。 如果你有访问该应用程序的源代码的权限，则此模式将在声明元素处显示 XAML。 选择“启用选择”和“预览所选内容”，然后在测试应用程序中选择该按钮。 MainWindow.xaml 文件在 Visual Studio 中打开并且光标放置在定义按钮的行上。

## <a name="using-xaml-tools-with-running-applications"></a>将 XAML 工具用于运行的应用程序
即使在没有源代码时，也可以使用这些 XAML 工具。 当附加到正在运行的 XAML 应用程序后，也可以使用该应用程序的 UI 元素上的“实时可视化树”。 下面是一个示例，使用与我们之前使用的相同的 WPF 测试应用程序。

1. 在“发布”配置中启动 TestXaml 应用程序。 不能附加到正在“调试”配置中运行的进程。

2. 打开 Visual Studio 的第二个实例，然后单击“调试”>“附加到进程”。 在可用进程的列表中查找 TestXaml.exe，然后单击“附加”。

3. 则应用程序开始运行。

4. 在 Visual Studio 的第二个实例中，打开“实时可视化树”（“调试”>“Windows”>“实时可视化树”）。 应看到 TestXaml UI 元素，并能像在直接调试应用程序时所做的那样操作它们。

## <a name="see-also"></a>请参阅

[通过 XAML 热重载编写和调试正在运行的 XAML 代码](xaml-hot-reload.md)
