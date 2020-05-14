---
title: 你好世界扩展教程 |微软文档
ms.date: 03/14/2019
ms.topic: conceptual
ms.assetid: f74e1ad1-1ee5-4360-9bd5-d82467b884ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c66f48a4b3c5948393e10f34810f3cb87c78c924
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711666"
---
# <a name="create-your-first-extension-hello-world"></a>创建您的第一个扩展：你好世界

此 Hello World 示例引导您为 Visual Studio 创建第一个扩展。 本教程演示如何向 Visual Studio 添加新命令。

在此过程中，您将学习如何：

* **[创建扩展性项目](#create-an-extensibility-project)**
* **[添加自定义命令](#add-a-custom-command)**
* **[修改源代码](#modify-the-source-code)**
* **[运行脚本](#run-it)**

在此示例中，您将使用 Visual C# 添加名为"问好世界！ 如下所示：

![你好世界命令](media/hello-world-say-hello-world.png)

> [!NOTE]
> 本文适用于 Windows 上的可视化工作室。 有关 Mac 的可视化工作室，请参阅[Mac 视觉工作室中的扩展性演练](/visualstudio/mac/extending-visual-studio-mac-walkthrough)。

## <a name="prerequisites"></a>先决条件

在开始之前，请确保已安装**Visual Studio 扩展开发**工作负荷，其中包括您需要的 VSIX 模板和示例代码。

> [!NOTE]
> 您可以使用任何版本的视觉工作室（社区、专业版或企业版）创建可视化工作室扩展性项目。

## <a name="create-an-extensibility-project"></a>创建扩展性项目

::: moniker range="vs-2017"

步骤 1。 在“文件”**** 菜单中，选择“新建”**** > “项目”****。

步骤 2. 在右上角的搜索框中，键入"vsix"并选择 Visual C# **VSIX 项目**。 在对话框底部输入 **"HelloWorld"，** 然后选择 **"确定**"。

![新建项目](media/hello-world-new-project.png)

现在，您应该会看到"入门"页和一些示例资源。

如果您需要离开本教程并返回本教程，您可以在 **"最近**"部分的 **"开始页面"** 中找到您的新 HelloWorld 项目。

::: moniker-end

::: moniker range=">=vs-2019"

步骤 1。 在“文件”**** 菜单中，选择“新建”**** > “项目”****。 搜索"vsix"，然后选择可视化 C# **VSIX 项目**，然后**选择"下一个**"。

步骤 2. 为**项目名称**输入"HelloWorld"，然后选择 **"创建**"。

![新建项目](media/hello-world-new-project-2019.png)

现在，您应该在**解决方案资源管理器**中看到 HelloWorld 项目。

::: moniker-end

## <a name="add-a-custom-command"></a>添加自定义命令

步骤 1。 如果选择 *.vsix清单清单*文件，您可以看到哪些选项是可更改的，例如说明、作者和版本。

步骤 2. 右键单击项目（不是解决方案）。 在上下文菜单上，选择 **"添加**"，然后**选择"新建项**"。

步骤 3. 选择"**扩展性**"部分，然后选择**命令**。

步骤 4. 在底部的 **"名称"** 字段中，输入文件名，如*Command.cs*。

![自定义命令](media/hello-world-vsix-command.png)

您的新命令文件在**解决方案资源管理器**中可见。 在 **"资源"** 节点下，您将找到与您的命令相关的其他文件。 例如，如果要修改图像，PNG 文件就在这里。

## <a name="modify-the-source-code"></a>修改源代码

此时，命令和按钮文本是自动生成的，不是很有趣。 如果要进行更改，可以修改 VSCT 文件和 CS 文件。

* VSCT 文件是您可以重命名命令以及定义命令在 Visual Studio 命令系统中的位置的位置。 在浏览 VSCT 文件时，您会注意到解释 VSCT 代码的每个部分控件的注释。

* CS 文件是您可以定义操作（如单击处理程序）的位置。

::: moniker range="vs-2017"

步骤 1。 在**解决方案资源管理器**中，查找新命令的 VSCT 文件。 在这种情况下，它将称为*命令包.*

![命令包 vct](media/hello-world-command-package-vsct.png)

::: moniker-end

::: moniker range=">=vs-2019"

步骤 1。 在**解决方案资源管理器**中，查找扩展名 VS 包的 VSCT 文件。 在这种情况下，它将被称为*HelloWorldPackage.vsct。*

::: moniker-end

步骤 2. 将`ButtonText`参数更改为`Say Hello World!`。

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

步骤 3. 返回**解决方案资源管理器**并找到*Command.cs*文件。 在`Execute`方法中，将字符串`message`从`string.Format(..)``Hello World!`更改为 。

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

请确保将更改保存到每个文件中。

## <a name="run-it"></a>运行脚本

您现在可以在可视化工作室实验实例中运行源代码。

步骤 1。 按**F5**以运行 **"开始调试"** 命令。 此命令生成项目并启动调试器，启动称为**实验实例**的 Visual Studio 的新实例。

::: moniker range="vs-2017"

您将在"视觉工作室"标题栏中看到"**实验实例**"一词。

![实验实例标题栏](media/hello-world-exp-instance.png)

::: moniker-end

步骤 2. 在**实验实例****的工具**菜单上，单击 **"打你好世界！"**

![最终结果](media/hello-world-final-result.png)

您应该看到来自新自定义命令的输出，在这种情况下，屏幕中心的对话框将为您提供**Hello World！** 。

## <a name="next-steps"></a>后续步骤

现在，您已经了解了使用 Visual Studio 可扩展性的基础知识，您可以在此处了解详细信息：

* [开始开发可视化工作室扩展](starting-to-develop-visual-studio-extensions.md)- 示例，教程。 并发布您的扩展
* [视觉工作室 2017 SDK 中的新增功能](what-s-new-in-the-visual-studio-2017-sdk.md)- Visual Studio 2017 中新的扩展功能
* [视觉工作室 2019 SDK 中的新增功能](whats-new-visual-studio-2019-sdk.md)- Visual Studio 2019 中新的扩展功能
* [在可视化工作室 SDK 中](internals/inside-the-visual-studio-sdk.md)- 了解可视化工作室可扩展性的详细信息
