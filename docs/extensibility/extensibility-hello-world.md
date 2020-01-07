---
title: Hello World 扩展教程 |Microsoft Docs
ms.date: 03/14/2019
ms.topic: conceptual
ms.assetid: f74e1ad1-1ee5-4360-9bd5-d82467b884ca
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0345d67a4202b8b267d213e0c288847e2774f722
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75404143"
---
# <a name="create-your-first-extension-hello-world"></a>创建第一个扩展： Hello World

本 Hello World 示例逐步讲解如何创建 Visual Studio 的第一个扩展。 本教程介绍如何将新命令添加到 Visual Studio。

在此过程中，您将学习如何：

* **[创建扩展性项目](#create-an-extensibility-project)**
* **[添加自定义命令](#add-a-custom-command)**
* **[修改源代码](#modify-the-source-code)**
* **[运行](#run-it)**

在此示例中，你将使用C#视觉对象来添加名为 "口述 Hello World！" 的自定义菜单按钮 如下所示：

![Hello World 命令](media/hello-world-say-hello-world.png)

> [!NOTE]
> 本文适用于 Windows 上的 Visual Studio。 有关 Visual Studio for Mac，请参阅[Visual Studio for Mac 中的扩展性演练](/visualstudio/mac/extending-visual-studio-mac-walkthrough)。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保已安装**Visual Studio 扩展开发**工作负荷，其中包括所需的 VSIX 模板和示例代码。

> [!NOTE]
> 可以使用任何版本的 Visual Studio （社区版、专业版或企业版）来创建 Visual Studio 扩展性项目。

## <a name="create-an-extensibility-project"></a>创建扩展性项目

::: moniker range="vs-2017"

步骤 1。 从“文件”菜单中选择“新建” > “项目”。

步骤 2。 在右上角的 "搜索" 框中，键入 "vsix" 并选择 Visual C# **vsix 项目**。 在对话框底部输入 "HelloWorld" 作为**名称**，然后选择 **"确定**"。

![新建项目](media/hello-world-new-project.png)

现在应会看到 "入门" 页和一些示例资源。

如果需要离开本教程并返回到该教程，可以在 "**最近**" 部分的 "**起始页**" 中找到新的 HelloWorld 项目。

::: moniker-end

::: moniker range=">=vs-2019"

步骤 1。 从“文件”菜单中选择“新建” > “项目”。 搜索 "vsix" 并选择 Visual C# **vsix 项目**，然后选择 "**下一步**"。

步骤 2。 输入 "HelloWorld" 作为**项目名称**，然后选择 "**创建**"。

![新建项目](media/hello-world-new-project-2019.png)

现在，应会在**解决方案资源管理器**中看到 HelloWorld 项目。

::: moniker-end

## <a name="add-a-custom-command"></a>添加自定义命令

步骤 1。 如果选择 " *source.extension.vsixmanifest* " 清单文件，则可以查看可更改的选项，如 "描述"、"作者" 和 "版本"。

步骤 2。 右键单击项目（而非解决方案）。 在上下文菜单中，选择 "**添加**"，然后选择 "**新建项**"。

步骤 3。 选择 "**扩展性**" 部分，然后选择 "**命令**"。

步骤 4。 在底部的 "**名称**" 字段中，输入文件名，例如*Command.cs*。

![自定义命令](media/hello-world-vsix-command.png)

新命令文件在**解决方案资源管理器**中可见。 在 "**资源**" 节点下，可找到与命令相关的其他文件。 例如，如果想要修改图像，则在此处为 PNG 文件。

## <a name="modify-the-source-code"></a>修改源代码

此时，命令和按钮文本会自动生成，而不是很感兴趣。 如果要进行更改，可以修改 .VSCT 文件和 CS 文件。

* .VSCT 文件是可在其中重命名命令的位置，还可以在 Visual Studio 命令系统中定义这些命令的位置。 浏览 .VSCT 文件时，你会注意到注释，其中说明了 .VSCT 代码控件的每个部分。

* 可以在 CS 文件中定义操作，例如单击处理程序。

::: moniker range="vs-2017"

步骤 1。 在**解决方案资源管理器**中，找到新命令的 .vsct 文件。 在这种情况下，它将被称为*CommandPackage。 .vsct*。

![命令包 .vsct](media/hello-world-command-package-vsct.png)

::: moniker-end

::: moniker range=">=vs-2019"

步骤 1。 在**解决方案资源管理器**中，查找扩展与包的 .vsct 文件。 在这种情况下，它将被称为*HelloWorldPackage。 .vsct*。

::: moniker-end

步骤 2。 将 `ButtonText` 参数更改为 `Say Hello World!`。

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

步骤 3。 返回到**解决方案资源管理器**并找到*Command.cs*文件。 在 `Execute` 方法中，将 `message` 的字符串从 `string.Format(..)` 更改为 `Hello World!`。

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

请确保保存对每个文件所做的更改。

## <a name="run-it"></a>运行脚本

你现在可以在 Visual Studio 实验实例中运行源代码。

步骤 1。 按**F5**运行 "**启动调试**" 命令。 此命令生成项目并启动调试器，并启动名为**实验实例**的新 Visual Studio 实例。

::: moniker range="vs-2017"

Visual Studio 标题栏中会显示 "**试验性实例**" 字样。

![实验实例标题栏](media/hello-world-exp-instance.png)

::: moniker-end

步骤 2。 在**实验实例**的 "**工具**" 菜单上，单击 "**口述 Hello World！** "。

![最终结果](media/hello-world-final-result.png)

你应该会看到新的自定义命令的输出，在这种情况下，屏幕中心的对话框会提供**Hello World！** 消息。

## <a name="next-steps"></a>后续步骤

现在，你已了解了使用 Visual Studio 扩展性的基本知识，接下来可以了解详细信息：

* [开始开发 Visual Studio 扩展](starting-to-develop-visual-studio-extensions.md)-示例、教程。 和发布扩展
* [Visual studio 2017 SDK 的新增](what-s-new-in-the-visual-studio-2017-sdk.md)功能-visual studio 中的新扩展性功能2017
* [Visual studio 2019 SDK 的新增](whats-new-visual-studio-2019-sdk.md)功能-visual studio 中的新扩展性功能2019
* 在[Visual STUDIO SDK 中](internals/inside-the-visual-studio-sdk.md)-了解有关 Visual studio 扩展性的详细信息
