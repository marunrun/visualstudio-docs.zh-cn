---
title: 使用 Visual Studio 和 C# 创建通用 Windows 平台 (UWP) 应用
description: 使用 XAML 和 C# 在 Visual Studio 中创建 UWP 应用
titleSuffix: ''
ms.custom: seodec18, get-started
ms.date: 09/20/2019
ms.technology: vs-ide-general
ms.topic: tutorial
ms.devlang: CSharp
author: ornellaalt
ms.author: ornella
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- multiple
ms.openlocfilehash: 8be56581374aefbef41a5173836d1189cceff290
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "77579996"
---
# <a name="tutorial-create-your-first-universal-windows-platform-application-in-visual-studio-with-xaml-and-c35"></a>教程：在 Visual Studio 中使用 XAML 和 C&#35 创建第一个通用 Windows 平台应用程序；

在这个 Visual Studio 集成开发环境 (IDE) 简介中，你将创建能在任何 Windows 10 设备上运行的“Hello World”应用。 为此，将使用通用 Windows 平台 (UWP) 项目模板、Extensible Application Markup Language (XAML) 和 C# 编程语言。

::: moniker range="vs-2017"
如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。
::: moniker-end
::: moniker range="vs-2019"
如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。
::: moniker-end

## <a name="create-a-project"></a>创建项目

首先，创建通用 Windows 平台项目。 项目类型随附了所需的全部模板文件，无需添加任何内容！

::: moniker range="vs-2017"
1. 打开 Visual Studio。

1. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

1. 在“新建项目”对话框的左侧窗格中，展开“Visual C#”，然后选择“Windows 通用”    。 在中间窗格中，选择“空白应用(通用 Windows)”  。 随后将项目命名为 HelloWorld，并选择“确定”   。

   ![Visual Studio IDE 中“新建项目”对话框中的 Windows 通用项目模板](media/new-project-csharp-uwp-helloworld.png)

   > [!NOTE]
   > 如果没有看到“空白应用(通用 Windows)”项目模板，请单击“新建项目”对话框左侧窗格中的“打开 Visual Studio 安装程序”链接    。<br><br>![单击“新建项目”对话框中的“打开 Visual Studio 安装程序”链接](../../ide/media/vb-open-visual-studio-installer-hello-world.png)<br><br>Visual Studio 安装程序启动。 选择“通用 Windows 平台开发”工作负载，然后选择“修改”   。<br><br>![Visual Studio 安装程序中的通用 Windows 平台开发工作负载](media/uwp-dev-workload.png)

1. 接接受“新式通用 Windows 平台项目”对话框中的默认目标版本和最小版本设置受“新式通用 Windows 平台项目”  对话框中的默认目标版本  和最小版本  设置。

   ![接受“新式通用 Windows 平台项目”对话框中的默认目标版本和最小版本设置](media/new-uwp-project-target-minver-dialog.png)
::: moniker-end

::: moniker range=">=vs-2019"
1. 打开 Visual Studio，然后在“启动”窗口上，选择“创建新项目”  。

1. 在“创建新项目”  屏幕上，在搜索框中输入“通用 Windows”  ，选择“空白应用(通用 Windows)”对应的 C# 模板  ，然后选择“下一步”  。

   ![创建新项目屏幕的屏幕截图](media/vs-2019/uwp-create-new-project.png)

   > [!NOTE]
   > 如果没有看到“空白应用(通用 Windows)”  项目模板，请单击“安装多个工具和功能”  链接。<br><br>![单击“安装多个工具和功能”链接](media/vs-2019/uwp-not-finding.png)<br><br>Visual Studio 安装程序启动。 选择“通用 Windows 平台开发”工作负载，然后选择“修改”   。<br><br>![Visual Studio 安装程序中的通用 Windows 平台开发工作负载](media/uwp-dev-workload.png)

1. 为项目提供名称“HelloWorld”，然后选择“创建”   。

   ![配置项目屏幕](media/vs-2019/uwp-configure-your-project.png)

1. 接接受“新式通用 Windows 平台项目”对话框中的默认目标版本和最小版本设置受“新式通用 Windows 平台项目”  对话框中的默认目标版本  和最小版本  设置。

   ![接受“新式通用 Windows 平台项目”对话框中的默认目标版本和最小版本设置](media/vs-2019/new-uwp-project-target-minver-dialog.png)
::: moniker-end

   > [!NOTE]
   > 如果你是第一次使用 Visual Studio 创建 UWP 应用，则可能会出现“设置”对话框  。 选择“开发人员模式”，然后选择“是”   。<br><br>
   > ![在“UWP 设置”对话框中启用开发人员模式](media/enable-developer-mode.png)<br><br>Visual Studio 会为你安装其他开发人员模式包。 包安装完成时，请关闭“设置”对话框  。

## <a name="create-the-application"></a>创建应用程序

现在开始开发吧。 你可以添加按钮控件，向按钮添加操作，然后启用"Hello World"应用查看效果。

### <a name="add-a-button-to-the-design-canvas"></a>向设计画布添加按钮

1. 在解决方案资源管理器中双击“MainPage.xaml”，打开拆分视图   。

   ::: moniker range="vs-2017"
   ![在解决方案资源管理器中，打开 MainPage.xaml ](media/uwp-solution-explorer-MainPage-xaml.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![在解决方案资源管理器中，打开 MainPage.xaml](media/vs-2019/uwp-solution-explorer-mainpage-xaml.png)
   ::: moniker-end

   出现两个窗格：一个是“XAML 设计器”，其中包含设计画布；另一个是“XAML 编辑器”，可用于添加或更改代码   。

   ![XAML 编辑器中的“XAML 设计器”窗格](media/uwp-xaml-editor.png)

1. 选择“工具箱”，打开“工具箱”弹出窗口  。

   ![单击“工具箱”，打开“工具箱”弹出窗口](media/uwp-toolbox.png)

   （如果看不到“工具箱”选项，可从菜单栏打开  。 为此，请选择“视图” > “工具箱”   。 或按 Ctrl+Alt+X。）   

1. 单击“固定”图标，固定“工具箱”窗口  。

   ![单击“固定”图标，固定“工具箱”窗口](media/uwp-toolbox-autohide.png)

1. 单击“按钮”控件，然后将其拖到设计画布上  。

   ![单击“按钮”控件并将其拖到设计画布上](media/uwp-toolbox-add-button-control.png)

   如果在 XAML 编辑器中查看代码，就会看到该按钮也已添加到此处  ：

   ![单击“按钮”控件并将其拖到设计画布上](media/uwp-xaml-control-code-window.png)

### <a name="add-a-label-to-the-button"></a>向按钮添加标签

1.  在 XAML 编辑器中，将按钮内容的值从“按钮”更改为"Hello World!"

   ![将按钮内容的值更改为 Hello World](media/uwp-change-button-text-in-xaml-code-window.png)

1. 请注意 XAML 设计器中的按钮也会随之更改  。

   ![设计画布上的按钮更改为 Hello World](media/uwp-button-text-change-in-design-canvas.png)

### <a name="add-an-event-handler"></a>添加事件处理程序

“事件处理程序”听起来复杂，但只不过是事件发生时，被调用代码的另一种名称。 在本例中，事件处理程序会将操作添加到"Hello World!" 按钮。

1. 双击设计画布上的按钮控件。

1. 在 MainPage.xaml.cs（代码隐藏页）中编辑事件处理程序代码  。

   现在，有趣的事情发生了。 默认事件处理程序如下所示：

   ![默认 Button_Click 事件处理程序 ](media/uwp-button-click-code.png)

   在我们更改后，该事件处理程序如下所示：

   ![新的异步 Button_Click 事件处理程序 ](media/uwp-add-hello-world-async-code.png)

   以下是可用于复制和粘贴的代码：

   ```C#
   private async void Button_Click(object sender, RoutedEventArgs e)
         {
             MediaElement mediaElement = new MediaElement();
             var synth = new Windows.Media.SpeechSynthesis.SpeechSynthesizer();
             Windows.Media.SpeechSynthesis.SpeechSynthesisStream stream = await synth.SynthesizeTextToStreamAsync("Hello, World!");
             mediaElement.SetSource(stream, stream.ContentType);
             mediaElement.Play();
         }
   ```

#### <a name="what-did-we-just-do"></a>我们刚才做了什么？

代码使用某些 Windows API 创建语音合成对象，然后向此对象通过一些文本用于朗读。 （有关使用 `SpeechSynthesis` 的详细信息，请参阅 <xref:System.Speech.Synthesis>。）

## <a name="run-the-application"></a>运行此应用程序


::: moniker range="vs-2017"
该生成、部署和启动“Hello World”UWP 应用了，以了解它的视听效果。 操作方法如下。

1. 使用“播放”按钮（它包含文本“本地计算机”  ）在本地计算机上启动应用程序。

   ![单击“本地计算机”以启动并调试 UWP 应用](media/uwp-start-or-debug.png)

   （或者，也可以从菜单栏中选择“调试”>“启动调试”或按 F5 启动应用   。）

1. 应用在初始屏幕消失后不久出现，请查看该应用。 此应用应类似于以下所示：

   ![UWP“Hello World”应用](media/uwp-hello-world-app.png)

1. 单击“Hello world”按钮  。

   Windows 10 设备将直接说“Hello, World!”

1. 要关闭应用，请在工具栏中单击“停止调试”按钮  （或者，从菜单栏中选择“调试”   > “停止调试”  或按 Shift+F5。）

::: moniker-end
::: moniker range=">=vs-2019"
该生成、部署和启动“Hello World”UWP 应用了，以了解它的视听效果。 操作方法如下。

1. 使用“播放”按钮（它包含文本“本地计算机”  ）在本地计算机上启动应用程序。

   ![单击“本地计算机”以启动并调试 UWP 应用](media/uwp-start-or-debug.png)

   （或者，也可以从菜单栏中选择“调试”>“启动调试”或按 F5 启动应用   。）

1. 应用在初始屏幕消失后不久出现，请查看该应用。 此应用应类似于以下所示：

   ![UWP“Hello World”应用](media/vs-2019/uwp-hello-world-app.png)

1. 单击“Hello world”按钮  。

   Windows 10 设备将直接说“Hello, World!”

1. 要关闭应用，请在工具栏中单击“停止调试”按钮  （或者，从菜单栏中选择“调试”   > “停止调试”  或按 Shift+F5。）

::: moniker-end

## <a name="next-steps"></a>后续步骤

恭喜你完成本教程！ 我们希望你能了解一些与 UWP 和 Visual Studio IDE 有关的基础知识。 要更加深入地了解，请继续学习下面的教程：

> [!div class="nextstepaction"]
> [创建用户界面](/windows/uwp/design/basics/xaml-basics-ui)

## <a name="see-also"></a>请参阅

- [UWP 概述](/windows/uwp/get-started/universal-application-platform-guide)
- [获取 UWP 应用示例](/windows/uwp/get-started/get-uwp-app-samples)