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
ms.openlocfilehash: 4c3bbafcf138c60b65940bcee73c74f56cf6e2fd
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342863"
---
# <a name="create-your-first-extension-hello-world"></a>创建第一个扩展：Hello World

此 Hello World 示例指导创建适用于 Visual Studio 在第一个扩展。 本教程演示如何将新的命令添加到 Visual Studio。

在此过程中，你将了解如何：

* **[创建可扩展性项目](#create-an-extensibility-project)**
* **[添加自定义命令](#add-a-custom-command)**
* **[修改源代码](#modify-the-source-code)**
* **[运行它](#run-it)**

对于此示例中，您将使用 Visual C# 来添加自定义菜单按钮名为"说 Hello World ！" 如下所示：

![Hello World 命令](media/hello-world-say-hello-world.png)

> [!NOTE]
> 本文适用于 Windows 上的 Visual Studio。 Visual Studio for Mac 中，请参阅[Visual Studio for Mac 中的可扩展性演练](/visualstudio/mac/extending-visual-studio-mac-walkthrough)。

## <a name="prerequisites"></a>系统必备

在开始之前，请确保已安装**Visual Studio 扩展开发**工作负荷中，其中包含 VSIX 模板将需要和示例代码。

> [!NOTE]
> 可以使用任何版本的 Visual Studio （Community、 Professional 或 Enterprise） 若要创建 Visual Studio 扩展性项目。

## <a name="create-an-extensibility-project"></a>创建可扩展性项目

::: moniker range="vs-2017"

步骤 1。 从“文件”菜单中选择“新建” > “项目”。   

步骤 2。 在右上角的搜索框中，键入"vsix"并选择视觉对象C# **VSIX 项目**。 输入"HelloWorld"**名称**对话框并选择底部**确定**。

![新建项目](media/hello-world-new-project.png)

现在应看到的入门页和一些示例资源。

如果你需要将本教程中，再返回到它，您可以在找到新的 HelloWorld 项目**起始页**中**最近**部分。

::: moniker-end

::: moniker range=">=vs-2019"

步骤 1。 从“文件”菜单中选择“新建” > “项目”。    搜索"vsix"并选择视觉对象C# **VSIX 项目**，然后**下一步**。

步骤 2。 输入"HelloWorld"**项目名称**，然后选择**创建**。

![新建项目](media/hello-world-new-project-2019.png)

现在应看到在 HelloWorld 项目**解决方案资源管理器**。

::: moniker-end

## <a name="add-a-custom-command"></a>添加自定义命令

步骤 1。 如果选择 *.vsixmanifest*清单文件中，您可以看到哪些选项可更改，如说明、 作者和版本。

步骤 2。 右键单击项目 （而不是解决方案）。 在上下文菜单中，选择**外**，然后**新项**。

步骤 3。 选择**扩展性**部分中，，然后选择**自定义命令**。

步骤 4。 在中**名称**底部字段中，输入一个文件名，例如*Command.cs*。

![自定义命令](media/hello-world-custom-command.png)

新的命令文件是在可见**解决方案资源管理器**。 下**资源**节点，您会发现与命令相关的其他文件。 例如，如果你想要修改映像，PNG 文件此处。

## <a name="modify-the-source-code"></a>修改源代码

此时，命令和按钮文本是自动生成并不是十分有趣。 如果你想要进行更改，可以修改的 VSCT 文件和 CS 文件。

* VSCT 文件是在其中您可以重命名你的命令，以及定义何处 Visual Studio 命令系统中。 在探索 VSCT 文件，您会注意到其中的注释解释 VSCT 代码控件的哪个每个部分。

* CS 文件是可以在其中定义操作，例如单击处理程序。

::: moniker range="vs-2017"

步骤 1。 在中**解决方案资源管理器**，查找您的新命令的 VSCT 文件。 在这种情况下，将调用*CommandPackage.vsct*。

![命令包 vsct](media/hello-world-command-package-vsct.png)

::: moniker-end

::: moniker range=">=vs-2019"

步骤 1。 在中**解决方案资源管理器**，查找扩展 VS 包的 VSCT 文件。 在这种情况下，将调用*HelloWorldPackage.vsct*。

::: moniker-end

步骤 2。 更改`ButtonText`参数`Say Hello World!`。

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

步骤 3。 返回到**解决方案资源管理器**并找到*Command.cs*文件。 在中`Execute`方法中，更改字符串`message`从`string.Format(..)`到`Hello World!`。

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

请确保将所做的更改保存到每个文件。

## <a name="run-it"></a>运行它

你现在可以在 Visual Studio 实验实例中运行的源代码。

步骤 1。 按**F5**运行**开始调试**命令。 此命令将生成项目并启动调试器，启动 Visual Studio 调用的一个新实例**实验实例**。

::: moniker range="vs-2017"

你将看到单词**实验实例**Visual Studio 标题栏中。

![实验实例标题栏](media/hello-world-exp-instance.png)

::: moniker-end

步骤 2。 上**工具**菜单**实验实例**，单击**Say Hello World ！** 。

![最终结果](media/hello-world-final-result.png)

在新的自定义命令中看到输出中，在此情况下该对话框在屏幕的中心，使您**Hello World ！** 消息。

## <a name="next-steps"></a>后续步骤

现在，了解使用 Visual Studio 扩展性的基础知识，下面是可以从何处了解详细信息：

* [开始开发 Visual Studio 扩展](starting-to-develop-visual-studio-extensions.md)-示例、 教程。 和发布你的扩展
* [什么是 Visual Studio 2017 SDK 中的新增](what-s-new-in-the-visual-studio-2017-sdk.md)-Visual Studio 2017 中的新可扩展性功能
* [什么是 Visual Studio 2019 SDK 中的新增](whats-new-visual-studio-2019-sdk.md)-Visual Studio 2019 中的新可扩展性功能
* [在 Visual Studio SDK](internals/inside-the-visual-studio-sdk.md) -了解 Visual Studio 扩展性的详细信息