---
title: 使用 Visual Basic 和 WPF 生成 Hello World 应用
description: 使用 Visual Basic 在 Visual Studio 中通过 Windows Presentation Foundation (WPF) UI 框架创建简单的 Windows Desktop .NET 应用。
ms.custom: seodec18, get-started
ms.date: 04/23/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: conceptual
dev_langs:
- VB
ms.assetid: f84339c7-d617-4f56-bfcd-af2215c347ba
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a7e9269c5de8d95ef66b1633da024c8a46c42758
ms.sourcegitcommit: 44e9b1d9230fcbbd081ee81be9d4be8a485d8502
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/30/2019
ms.locfileid: "70180407"
---
# <a name="tutorial-create-a-simple-application-with-visual-basic"></a>教程：使用 Visual Basic 创建简单应用

通过完成本教程，你将熟悉在使用 Visual Studio 开发应用程序时可使用的许多工具、对话框和设计器。 你将创建“Hello, World”应用程序、设计 UI、添加代码并调试错误。在此期间，你将了解如何使用集成开发环境 ([IDE](visual-studio-ide.md))。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="configure-the-ide"></a>配置 IDE

::: moniker range="vs-2017"

首次打开 Visual Studio 时，系统会提示你登录。 在本教程中，此步骤为可选步骤。 接下来可能会显示一个对话框，让你选择开发设置和颜色主题。 保留默认值，然后选择“启动 Visual Studio”  。

![选择设置对话框](../media/exploreide-settings.png)

启动 Visual Studio 后，将看到工具窗口、菜单和工具栏，以及主窗口空间。 工具窗口停靠在应用程序窗口的左侧和右侧，其顶部有 **“快速启动”** 、菜单栏和标准工具栏。 应用程序窗口的中心是 **“起始页”** 。 当您加载解决方案或项目时，编辑器和设计器将显示在 **起始页** 的空间中。 开发应用程序时，大部分时间都将用在此中心区域。

![应用了常规设置的 Visual Studio 2017 IDE](../media/exploreide-idewithgeneralsettings.png)

::: moniker-end

::: moniker range=">=vs-2019"

启动 Visual Studio 时，“启动”窗口首先打开。 选择“继续但无需代码”打开开发环境  。 将看到工具窗口、菜单和工具栏，以及主窗口空间。 “工具”窗口停靠在“应用程序”窗口左右两侧，其顶部有搜索框、菜单栏和标准工具栏。 加载解决方案或项目时，编辑器和设计器显示在应用程序窗口中间。 开发应用程序时，大部分时间都将用在此中心区域。

::: moniker-end

## <a name="create-the-project"></a>创建项目

在 Visual Studio 中创建应用程序时，应首先创建项目和解决方案。 此示例将创建一个 Windows Presentation Foundation (WPF) 项目。

::: moniker range="vs-2017"

1. 创建新项目。 在菜单栏上，依次选择“文件” > “新建” > “项目”    。

     ![在菜单栏上，依次选择“文件”、“新建”和“项目”](../media/exploreide-filenewproject.png)

2. 在“新项目”  对话框中，依次选择“已安装”   > “Visual Basic”   > “Windows 桌面”  类别和“WPF 应用(.NET Framework)”  模板。 将项目命名为“HelloWPFApp”  并选择“确定”  。

     ![Visual Studio“新建项目”对话框中的 WPF 应用模板](media/exploreide-newproject-vb.png)

Visual Studio 将创建 HelloWPFApp 项目和解决方案，“解决方案资源管理器”  将显示各种文件。 “WPF 设计器”  在拆分视图中显示 MainWindow.xaml  的设计视图和 XAML 视图。 您可以滑动拆分器，以显示任一视图的更多或更少部分。 您可以选择只查看可视化视图或 XAML 视图。  “解决方案资源管理器”中显示以下项：

![已加载 HelloWPFApp 文件的解决方案资源管理器](../media/exploreide-hellowpfappfiles.png)

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio 2019。

2. 在“创建新项目”  屏幕上，搜索“WPF”，选择“WPF App (.NET Framework)”  ，然后选择“下一步”  。

   ![Visual Studio“新建项目”对话框中的 WPF 应用模板](media/vs-2019/exploreide-newprojectvb-vs2019.png)

3. 在下一个屏幕中，为项目指定名称“HelloWPFApp”  ，然后选择“创建”  。

Visual Studio 将创建 HelloWPFApp 项目和解决方案，“解决方案资源管理器”  将显示各种文件。 “WPF 设计器”  在拆分视图中显示 MainWindow.xaml  的设计视图和 XAML 视图。 您可以滑动拆分器，以显示任一视图的更多或更少部分。 您可以选择只查看可视化视图或 XAML 视图。  “解决方案资源管理器”中显示以下项：

![已加载 HelloWPFApp 文件的解决方案资源管理器](../media/vs-2019/exploreide-hellowpfappfiles.png)

::: moniker-end

> [!NOTE]
> 若要详细了解 XAML (eXtensible Application Markup Language)，请参阅 [WPF 的 XAML 概述](/dotnet/framework/wpf/advanced/xaml-overview-wpf)页。

你可以在创建项目后进行自定义。 通过使用 **属性** 窗口（ **视图** 菜单上），您可以显示和更改应用程序中的项目项、控件和其他项的选项。

### <a name="change-the-name-of-mainwindowxaml"></a>更改 MainWindow.xaml 的名称

为 MainWindow 指定更具体的名称。

1. 在“解决方案资源管理器”  中，选择 MainWindow.xaml  。 此时应看到“属性”窗口，如果没有，请选择“视图”菜单，然后再选择“属性窗口”项    。

1. 将 **“文件名称”** 属性更改为 `Greetings.xaml`。

     ![突出显示文件名的“属性”窗口](../media/exploreide-filenameinpropertieswindow.png)

     “解决方案资源管理器”  显示文件现在名为“Greetings.xaml”  ，而嵌套代码文件现在名为“Greetings.xaml.vb”  。 此代码文件嵌套在 .xaml  文件节点下，表明它们的关系十分紧密。

## <a name="design-the-user-interface-ui"></a>设计用户界面 (UI)

我们会将三种类型的控件添加到此应用程序：一个 <xref:System.Windows.Controls.TextBlock> 控件、两个 <xref:System.Windows.Controls.RadioButton> 控件和一个 <xref:System.Windows.Controls.Button> 控件。

### <a name="add-a-textblock-control"></a>添加 TextBlock 控件

1. 输入“Ctrl+Q”以激活搜索框，然后键入“工具箱”    。 从结果列表中选择“查看”>“工具箱”  。

2. 在“工具箱”  中，展开“公共 WPF 控件”  节点以查看 TextBlock 控件。

     ![突出显示 TextBlock 控件的工具箱](../media/exploreide-textblocktoolbox.png)

3. 通过选择“TextBlock”  项并将其拖到设计图面的窗口中，将 TextBlock 控件添加到设计图面中。 把控件居中到窗口的顶部附近。

你的窗口应与下图类似：

![Greetings 窗体上的 TextBlock 控件](../media/exploreide-greetingswithtextblockonly.png)

XAML 标记应如下面的示例所示：

```xaml
<TextBlock HorizontalAlignment="Left" Margin="381,100,0,0" TextWrapping="Wrap" Text="TextBlock" VerticalAlignment="Top"/>
```

### <a name="customize-the-text-in-the-text-block"></a>自定义文本块中的文本

1. 在 XAML 视图中，找到 TextBlock 的标记并更改 Text 属性：

   ```xaml
   Text="Select a message option and then choose the Display button."
   ```

2. 视需要再次使 TextBlock 居中，并通过按 Ctrl+S 或使用“文件”  菜单项保存更改。

接下来，向窗体添加两个 [RadioButton](/dotnet/framework/wpf/controls/radiobutton) 控件。

### <a name="add-radio-buttons"></a>添加单选按钮

1. 在“工具箱”  中，查找“RadioButton”  控件。

     ![选定 RadioButton 控件的“工具箱”窗口](../media/exploreide-radiobuttontoolbox.png)

2. 通过选择“RadioButton”  项并将其拖到设计图面的窗口中，将两个 RadioButton 控件添加到设计图面中。 移动按钮（通过选择它们并使用箭头键），以便按钮并排显示在 TextBlock 控件下。

     你的窗口应如下所示：

     ![包含 TextBlock 控件和两个单选按钮的 Greetings 窗体](../media/exploreide-greetingswithradiobuttons.png)

3. 在左侧 RadioButton 控件的 **“属性”** 窗口中，将 **“名称”** 属性（位于 **“属性”** 窗口顶部）更改为 `HelloButton`。

     ![RadioButton 属性窗口](../media/exploreide-buttonproperties.png)

4. 在右侧 RadioButton 控件的“属性”  窗口中，将“名称”  属性更改为 `GoodbyeButton`，然后保存更改。

你现在可以为每个 RadioButton 控件添加显示文本。 以下程序将更新 RadioButton 控件的 **“内容”** 属性。

### <a name="add-display-text-for-each-radio-button"></a>添加每个单选按钮的显示文本

1. 在设计界面上，通过在 HelloButton 上按鼠标右键打开 HelloButton 的快捷菜单，选择“编辑文本”  ，然后输入 `Hello`。

2. 在 GoodbyeButton 上按鼠标右键打开 GoodbyeButton 的快捷菜单，选择“编辑文本”  ，然后输入 `Goodbye`。

### <a name="set-a-radio-button-to-be-checked-by-default"></a>设置要默认选中的单选按钮

这一步将设置要默认选中的 HelloButton，这样两个单选按钮中始终有一个处于选中状态。

在 XAML 视图中，找到 HelloButton 的标记并添加“IsChecked”  属性：

```xaml
IsChecked="True"
```

最后添加的 UI 元素是 [Button](/dotnet/framework/wpf/controls/button) 控件。

### <a name="add-the-button-control"></a>添加按钮控件

1. 在“工具箱”  中，找到“按钮”  控件，然后通过将控件拖到设计视图的窗体中，将其添加到 RadioButton 控件下方的设计界面中。

2. 在 XAML 视图中，将 Button 控件的“内容”  值从 `Content="Button"` 更改为 `Content="Display"`，然后保存更改。

     标记应与以下示例类似：`<Button Content="Display" HorizontalAlignment="Left" VerticalAlignment="Top" Width="75" Margin="215,204,0,0"/>`

     你的窗口应与下图类似。

     ![包含控制标签的 Greetings 窗体](../media/exploreide-greetingswithcontrollabels.png)

### <a name="add-code-to-the-display-button"></a>向显示按钮添加代码

此应用程序运行时，用户选择单选按钮，再选择“显示”  按钮之后，会显示一个消息框。 选择 Hello 将显示一个消息框，选择 Goodbye 将显示另一个。 要创建此行为，需将代码添加到 Greetings.xaml.vb  或 Greetings.xaml.cs  中的 `Button_Click` 事件。

1. 在设计图面上，双击 **“显示”** 按钮。

     此时，“Greetings.xaml.vb”  打开，光标位于 `Button_Click` 事件上。

    ```vb
    Private Sub Button_Click_1(sender As Object, e As RoutedEventArgs)

    End Sub
    ```

2. 输入以下代码：

    ```vb
    If HelloButton.IsChecked = True Then
        MessageBox.Show("Hello.")
    ElseIf GoodbyeButton.IsChecked = True Then
        MessageBox.Show("Goodbye.")
    End If
    ```

3. 保存应用程序。

## <a name="debug-and-test-the-application"></a>调试并测试应用程序

接下来将调试应用程序，查找错误并测试两个消息框是否正确显示。 下面的说明介绍如何生成和启动调试器，但以后可以阅读[生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf) 和[调试 WPF](../../debugger/debugging-wpf.md) 获取有关详细信息。

### <a name="find-and-fix-errors"></a>查找并修复错误

在此步骤中，将遇到之前因更改 MainWindow.xaml  文件的名称而引起的错误。

#### <a name="start-debugging-and-find-the-error"></a>开始调试和查找错误

1. 通过按 F5  或选择“调试”，然后选择“启动调试”  ，启动调试程序  。

   将出现“中断模式”窗口，“输出”窗口指示发生 IOException   :“找不到资源 'mainwindow.xaml'”。

   ![IOException 消息屏幕截图](../media/exploreide-ioexception.png)

2. 依次选择“调试”   > “停止调试”  ，停止调试程序。

开始学习本教程时，我们将 MainWindow.xaml  重命名为 Greetings.xaml  ，但是该代码仍然引用 MainWindow.xaml  作为应用程序的启动 URI，因此该项目无法启动。

#### <a name="specify-greetingsxaml-as-the-startup-uri"></a>将 Greetings.xaml 指定为启动 URI

1. 在“解决方案资源管理器”  中，打开“Application.xaml”  文件。

2. 将 `StartupUri="MainWindow.xaml"` 更改为 `StartupUri="Greetings.xaml"`，然后保存更改。

再次启动调试程序 （按“F5”  ）。 应可看到应用程序的 Greetings  窗口。 现在关闭应用程序窗口，停止调试。

### <a name="debug-with-breakpoints"></a>使用断点进行调试

可通过添加一些断点，在调试期间测试代码。 可以通过选择“调试”   > “切换断点”  、通过在编辑器中想要添加断点的代码行旁边的左边距中单击或按 F9  来添加断点。

#### <a name="add-breakpoints"></a>添加断点

1. 打开“Greetings.xaml.vb”  ，并选择以下行：`MessageBox.Show("Hello.")`

2. 通过按 F9 或从菜单选择“调试”  ，然后选择“切换断点”   添加断点。

   编辑器窗口最左侧边距中该代码行附近将显示一个红圈。

3. 选择以下行： `MessageBox.Show("Goodbye.")`。

4. 按“F9”  键添加断点，然后按“F5”  启动调试。

5. 在 **“Greetings”** 窗口中，选择 **“Hello”** 单选按钮，然后选择 **“显示”** 按钮。

   行 `MessageBox.Show("Hello.")` 将用黄色突出显示。 在 IDE 底部，“自动”、“本地”和“监视”窗口一起停靠在左侧，而“调用堆栈”、“断点”、“异常设置”、“命令”、“即时”和“输出”窗口一起停靠在右侧。

   ![调试程序中断点的屏幕截图](media/exploreide-debugbreakpoint.png)

6. 在菜单栏上，选择“调试”   > “跳出”  。

     应用程序继续执行，并将显示出带有“Hello”的消息框。

7. 选择消息框上的 **“确定”** 按钮将其关闭。

8. 在 **“Greetings”** 窗口中，选择 **“Goodbye”** 单选按钮，然后选择 **“显示”** 按钮。

     行 `MessageBox.Show("Goodbye.")` 将用黄色突出显示。

9. 按“F5”  键继续调试。 当消息框出现时，选择消息框上的 **“确定”** 按钮将其关闭。

10. 关闭应用程序窗口，停止调试。

11. 在菜单栏上，选择“调试”   > “禁用所有断点”  。

### <a name="build-a-release-version-of-the-application"></a>生成应用程序的发布版本

确认一切就绪后，可以准备该应用程序的发布版本。

1. 在主菜单中，依次选择“生成”   > “清理解决方案”  ，删除上一生成过程中创建的中间文件和输出文件。 这不是必需的，但它会清理调试生成输出。

2. 使用工具栏（当前显示“调试”）上的下拉列表控件把 HelloWPFApp 的生成配置从“调试”更改为“发布”   。

3. 选择“生成” > “生成解决方案”来生成解决方案   。

恭喜你完成本教程！ 可在解决方案和项目目录 (...\HelloWPFApp\HelloWPFApp\bin\Release  ) 下找到生成的 .exe  文件。

## <a name="see-also"></a>请参阅

::: moniker range="vs-2017"

- [Visual Studio 2017 中的新增功能](../../ide/whats-new-visual-studio-2017.md)
- [工作效率提示](../../ide/productivity-features.md)

::: moniker-end

::: moniker range="vs-2019"

- [Visual Studio 2019 中的新增功能](../../ide/whats-new-visual-studio-2019.md)
- [工作效率提示](../../ide/productivity-features.md)

::: moniker-end