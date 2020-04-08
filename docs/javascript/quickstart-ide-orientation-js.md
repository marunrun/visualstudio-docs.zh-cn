---
title: Visual Studio IDE 教程
titleSuffix: ''
ms.date: 02/05/2019
ms.topic: quickstart
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f7a05f62685509a69fd5dfe8f758b4e5599b9324
ms.sourcegitcommit: 334024a43477290ecc610e70c80a0f772787a7d6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/01/2020
ms.locfileid: "80527942"
---
# <a name="first-look-at-the-visual-studio-ide"></a>初步了解 Visual Studio IDE

在这个 5-10 分钟的 Visual Studio 集成开发环境 (IDE) 简介中，我们将介绍一些窗口、菜单和其他 UI 功能。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

::: moniker range=">=vs-2019"

## <a name="start-window"></a>启动窗口

启动 Visual Studio 后，最先看到的是启动窗口。 启动窗口旨在帮助你更快地“编码”。 它具有以下选项：关闭或签出代码、打开现有项目或解决方案、创建新项目或只打开包含一些代码文件的文件夹。

[![Visual Studio 2019 中的“启动”窗口](media/vs-2019/start-window.png)](media/vs-2019/start-window.png)

如果首次使用 Visual Studio，最近的项目列表将为空。

如果使用基于非 MSBuild 的代码库，则将使用“打开本地文件夹”选项在 Visual Studio 中打开代码。 有关详细信息，请参阅[在 Visual Studio 中开发代码而无需创建项目或解决方案](develop-javascript-code-without-solutions-projects.md)。 否则，可以从源提供程序（如 GitHub 或 Azure DevOps）创建新项目或克隆项目。

“无需代码，即可继续”选项仅打开 Visual Studio 开发环境，而不加载任何特定项目或代码。 可以选择此选项，加入 [Live Share](/visualstudio/liveshare/) 会话或附加到进程以进行调试。 此外可以按“Esc”关闭启动窗口，然后打开 IDE。

::: moniker-end

::: moniker range="vs-2017"

## <a name="start-page"></a>起始页

启动 Visual Studio 之后你最先看到的很可能就是起始页。 起始页设计成一个“中心”，可帮助你更快地找到所需的命令和项目文件。 “最新动态”部分显示你最近处理的项目和文件夹。 在“新建项目”下，可以单击链接转到“新建项目”对话框中，或在“打开”下，可以打开现有代码项目或文件夹。 右侧是最新的开发人员新闻源。

![Visual Studio 中的“起始页”](media/start-page.png)

如果关闭“起始页”并希望再次查看，则可以从“文件”菜单重新打开它。

![Visual Studio 中的“文件”菜单](media/quickstart-IDE-file-menu-large.png)

::: moniker-end

## <a name="create-a-project"></a>创建项目

为继续了解 Visual Studio 的功能，我们将创建一个新项目。

::: moniker range=">=vs-2019"

1. 在“启动”窗口中，选择“创建新项目”，然后在搜索框中键入“javascript”，筛选项目类型列表，以仅显示名称或语言类型中包含“javascript”的项目类型。

   Visual Studio 提供了各种类型的项目模板，帮助你快速开始编写代码。 （或者，如果你是 TypeScript 开发者，则可以使用该语言创建项目。 对于所有编程语言而言，我们将查看的 UI 都是相似的。）

   ![在 Visual Studio 开始窗口上搜索项目模板](media/vs-2019/create-new-project.png)

1. 选择“空白 Node.js Web 应用程序”项目模板并单击“下一步”。

1. 在显示的“配置新项目”对话框中，接受默认的项目名称并选择“创建”。

::: moniker-end

::: moniker range="vs-2017"

1. 在“起始页”上“新建项目”下的搜索框中，键入 javascript，筛选项目类型列表，以仅显示名称或语言类型中包含“javascript”的项目类型。

   ![在 Visual Studio 起始页上搜索项目模板](media/start-page-search-templates.png)

   Visual Studio 提供了各种类型的项目模板，帮助你快速开始编写代码。 选择“空白 Node.js Web 应用程序”项目模板。 （或者，如果你是 TypeScript 开发者，则可以使用该语言创建项目。 对于所有编程语言而言，我们将查看的 UI 都是相似的。）

1. 在显示的“新建项目”对话框中，接受默认的项目名称并选择“确定”。
::: moniker-end

   创建项目，并在“编辑器”窗口中打开名为 server.js 的文件。 编辑器可显示文件的内容，是你在 Visual Studio 中完成大部分编码工作的地方。

   ![Visual Studio 中的编辑器](media/editor.png)

## <a name="solution-explorer"></a>“解决方案资源管理器”

“解决方案资源管理器”（通常位于 Visual Studio 的右侧）可以显示项目、解决方案或代码文件夹中文件和文件夹层次结构的图形表示形式。 你可以浏览层次结构，并导航到“解决方案资源管理器”中的某个文件。

![Visual Studio 中的解决方案资源管理器](media/quickstart-IDE-solution-explorer.png)

## <a name="menus"></a>菜单

Visual Studio 顶部的菜单栏将命令分组成不同的类别。 例如，“项目”菜单包含与你正在处理的项目相关的命令。 在“工具”菜单上，可通过选择“选项”自定义 Visual Studio 的行为方式，或选择“获取工具和功能”向安装程序添加功能。

![Visual Studio 中的菜单栏](media/quickstart-IDE-menu-bar.png)

可通过依次选择“视图”菜单和“错误列表”打开“错误列表”窗口。

## <a name="error-list"></a>错误列表

“错误列表”显示错误、警告以及有关当前代码状态的消息。 如果文件中或项目的任何地方出现错误（例如缺少括号或分号），则会在此处列出。

![Visual Studio 中的错误列表](media/quickstart-IDE-error-list.png)

## <a name="output-window"></a>“输出”窗口

“输出”窗口显示生成项目和源代码管理提供程序中的输出消息。

让我们生成该项目来查看一些生成输出。 从 **“生成”** 菜单中选择 **“生成解决方案”**。 “输出”窗口自动获得焦点并显示成功生成的消息。

![Visual Studio 中的“输出”窗口](media/build-output-minimal.png)

## <a name="search-box"></a>搜索框

搜索框是在 Visual Studio 中执行任何操作的快捷方式。 你可以输入一些与你想要执行的操作相关的文本，它会为你显示一个与文本相关的选项列表。 例如，假设要增加生成输出的详细程度，以显示有关确切生成内容的其他详细信息。 具体操作如下：

1. 在搜索框中键入“详细信息”。 从显示的结果中，选择“选项”类别下的“项目和解决方案”->“生成并运行”。

   ![Visual Studio 中的搜索框](media/quickstart-IDE-quick-launch.png)

   “选项”对话框打开，会显示“生成并运行”选项页。

1. 在“MSBuild 项目生成输出详细信息”下，选择“常规”，然后单击“确定”。

1. 通过右键单击“解决方案资源管理器”中的“NodejsWebApp1”项目，然后从上下文菜单中选择“重新生成”，重新生成项目。

   这次“输出”窗口显示了生成过程中更详细的日志记录，包括在哪里复制哪些文件。

   ![Visual Studio 中的详细生成输出](media/build-output-verbose.png)

## <a name="send-feedback-menu"></a>“发送反馈”菜单

如果在使用 Visual Studio 时遇到任何问题，或者有关于如何改进产品的建议，请使用 Visual Studio 窗口顶部的“发送反馈”菜单。

![Visual Studio 中的“发送反馈”菜单](../ide/media/quickstart-ide-send-feedback.png)

## <a name="next-steps"></a>后续步骤

我们只介绍了 Visual Studio 的一些功能以便熟悉用户界面。 若要进一步了解，请继续：

> [!div class="nextstepaction"]
> [了解代码编辑器](write-and-edit-code.md)

> [!div class="nextstepaction"]
> [了解项目和解决方案](../get-started/tutorial-projects-solutions.md)

## <a name="see-also"></a>另请参阅

- [Visual Studio IDE 概述](../get-started/visual-studio-ide.md)
- [Visual Studio 2017 的更多功能](../ide/advanced-feature-overview.md)
- [更改主题和字体颜色](../ide/quickstart-personalize-the-ide.md)
