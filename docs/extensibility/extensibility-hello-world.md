---
title: Hello World 扩展教程 | Microsoft Docs
ms.date: 03/14/2019
ms.topic: tutorial
ms.assetid: f74e1ad1-1ee5-4360-9bd5-d82467b884ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 796cb53ea5124662c695cce55241794802f042c0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85905932"
---
# <a name="tutorial---create-your-first-extension-hello-world"></a>教程 - 编写自己的第一个扩展：Hello World

此 Hello World 示例将引导你完成为 Visual Studio 创建第一个扩展。 本教程介绍如何向 Visual Studio 添加新命令。

在此过程中，你将了解如何执行以下操作：

* [创建扩展性项目](#create-an-extensibility-project)
* [添加自定义命令](#add-a-custom-command)
* [修改源代码](#modify-the-source-code)
* **[运行脚本](#run-it)**

在本示例中，你将使用 Visual C# 添加名为“Say Hello World!”的自定义菜单按钮， 如下所示：

![Hello World 命令](media/hello-world-say-hello-world.png)

> [!NOTE]
> 本文适用于 Windows 上的 Visual Studio。 对于 Visual Studio for Mac，请参阅 [Visual Studio for Mac 中的扩展性演练](/visualstudio/mac/extending-visual-studio-mac-walkthrough)。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保已安装 Visual Studio 扩展开发工作负载，包括所需的 VSIX 模板和示例代码。

> [!NOTE]
> 可以使用任何版本的 Visual Studio（Community、Professional 或 Enterprise）来创建 Visual Studio 扩展性项目。

## <a name="create-an-extensibility-project"></a>创建扩展性项目

::: moniker range="vs-2017"

步骤 1。 从“文件”菜单中选择“新建” > “项目”  。

步骤 2. 在右上角的搜索框中，键入“vsix”，然后选择 Visual C#“VSIX 项目”。 在对话框底部，输入“HelloWorld”作为“名称”，然后选择“确定” 。

![新建项目](media/hello-world-new-project.png)

现在，你应该会看到“入门”页和一些示例资源。

如果你需要退出本教程然后再返回，可以在起始页上的“最近使用”部分找到你的新 HelloWorld 项目 。

::: moniker-end

::: moniker range=">=vs-2019"

步骤 1。 从“文件”菜单中选择“新建” > “项目”  。 搜索“vsix”并选择 Visual C#“VSIX 项目”，然后选择“下一步” 。

步骤 2. 输入“HelloWorld”作为“项目名称”，然后选择“创建” 。

![新建项目](media/hello-world-new-project-2019.png)

现在，你应该能够在“解决方案资源管理器”中看到 HelloWorld 项目。

::: moniker-end

## <a name="add-a-custom-command"></a>添加自定义命令

步骤 1。 如果选择 .vsixmanifest 清单文件，可以查看哪些选项可更改，例如描述、作者和版本。

步骤 2. 右键单击项目（而非解决方案）。 在上下文菜单上，选择“添加”，然后选择“新建项” 。

步骤 3. 选择“扩展性”部分，然后选择“命令” 。

步骤 4. 在底部的“名称”字段中，输入文件名，如 Command.cs。

![自定义命令](media/hello-world-vsix-command.png)

你的新命令文件将显示在“解决方案资源管理器”中。 在“资源”节点下，你将找到与命令相关的其他文件。 例如，你可以通过此处的 PNG 文件修改图像。

## <a name="modify-the-source-code"></a>修改源代码

此时，命令和按钮文本是自动生成的，比较生硬。 如果要进行更改，可以修改 VSCT 文件和 CS 文件。

* 你可以在 VSCT 文件中对命令进行重命名以及定义这些命令在 Visual Studio 命令系统中的位置。 当你浏览 VSCT 文件时，会注意到注释，其中解释了 VSCT 代码的每个部分所控制的内容。

* 你可以在 CS 文件中定义操作，如单击处理程序。

::: moniker range="vs-2017"

步骤 1。 在“解决方案资源管理器”中，找到新命令的 VSCT 文件。 在本例中，为 CommandPackage.vsct。

![命令包 vsct](media/hello-world-command-package-vsct.png)

::: moniker-end

::: moniker range=">=vs-2019"

步骤 1。 在“解决方案资源管理器”中，找到扩展 VS 包的 VSCT 文件。 在本例中，为 HelloWorldPackage.vsct。

::: moniker-end

步骤 2. 将 `ButtonText` 参数更改为 `Say Hello World!`。

```xml
  ...
  <Button guid="guidCommandPackageCmdSet" id="CommandId" priority="0x0100" type="Button">
     <Parent guid="guidCommandPackageCmdSet" id="MyMenuGroup" />
     <Icon guid="guidImages" id="bmpPic1" />
     <Strings>
        <ButtonText>Say Hello World!</ButtonText>
     </Strings>
  </Button>
  ...
```

步骤 3. 返回到“解决方案资源管理器”，找到 Command.cs 文件。 在 `Execute` 方法中，将字符串 `message` 从 `string.Format(..)` 更改为 `Hello World!`。

```csharp
  ...
  private void Execute(object sender, EventArgs e)
  {
    ThreadHelper.ThrowIfNotOnUIThread();
    string message = "Hello World!";
    string title = "Command";

    // Show a message box to prove we were here
    VsShellUtilities.ShowMessageBox(
        this.ServiceProvider,
        message,
        title,
        OLEMSGICON.OLEMSGICON_INFO,
        OLEMSGBUTTON.OLEMSGBUTTON_OK,
        OLEMSGDEFBUTTON.OLEMSGDEFBUTTON_FIRST);
  }
  ...
```

确保保存对每个文件所做的更改。

## <a name="run-it"></a>运行脚本

现在，你可以在 Visual Studio 试验实例中运行源代码。

步骤 1。 按 F5 运行“启动调试”命令 。 此命令将生成项目并启动调试器，启动名为“试验实例”的 Visual Studio 新实例。

::: moniker range="vs-2017"

你将在 Visual Studio 标题栏中看到文字“试验实例”。

![试验实例标题栏](media/hello-world-exp-instance.png)

::: moniker-end

步骤 2. 在“试验实例”的“工具”菜单上，单击“Say Hello World!”  。

![最终结果](media/hello-world-final-result.png)

你应该会看到新自定义命令的输出，在本例中，屏幕中央将显示“Hello World!”对话框。 。

## <a name="next-steps"></a>后续步骤

现在你已了解使用 Visual Studio 扩展性的基本知识，可以在此处了解更多信息：

* [开始开发 Visual Studio 示例](starting-to-develop-visual-studio-extensions.md) - 示例、教程。 和发布扩展
* [Visual Studio 2017 SDK 中的新增功能](what-s-new-in-the-visual-studio-2017-sdk.md) - Visual Studio 2017 中的新扩展性功能
* [Visual Studio 2019 SDK 中的新增功能](whats-new-visual-studio-2019-sdk.md) - Visual Studio 2019 中的新扩展性功能
* [在 Visual Studio SDK 内](internals/inside-the-visual-studio-sdk.md) - 了解 Visual Studio 扩展性的详细信息
