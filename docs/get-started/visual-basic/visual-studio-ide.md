---
title: 面向 Visual Basic 开发人员的概述
ms.date: 11/15/2018
ms.technology: vs-ide-general
ms.custom: get-started
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 7dfcc4a01dfd5e9b63dc16afa0c2b3286419c193
ms.sourcegitcommit: 51dad3e11d7580567673e0d426ab3b0a17584319
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/10/2019
ms.locfileid: "66820655"
---
# <a name="welcome-to-the-visual-studio-ide--visual-basic"></a>欢迎使用 Visual Studio IDE | Visual Basic

Visual Studio 集成开发环境是一种创新启动板，可用于编辑、调试并生成代码，然后发布应用  。 集成开发环境 (IDE) 是一个功能丰富的程序，可用于软件开发的许多方面。 除了大多数 IDE 提供的标准编辑器和调试器之外，Visual Studio 还包括编译器、代码完成工具、图形设计器和许多其他功能，以简化软件开发过程。

::: moniker range="vs-2017"

![Visual Studio IDE](../media/visual-studio-ide.png)

::: moniker-end

::: moniker range=">=vs-2019"

[![Visual Studio 2019 IDE](media/vs-2019/ide-overview.png)](media/vs-2019/ide-overview.png#lightbox)

::: moniker-end

此图像显示 Visual Studio 具有一个打开的项目和若干可能会使用的关键工具窗口：

- 可通过[解决方案资源管理器](../../ide/solutions-and-projects-in-visual-studio.md)（右上方）查看、导航和管理代码文件。 解决方案资源管理器可将代码文件分组为[解决方案和项目](tutorial-projects-solutions.md)，从而帮助整理代码  。

- [编辑器窗口](../../ide/writing-code-in-the-code-and-text-editor.md)（中心）用于显示文件内容，你可能会在该窗口花费大部分时间。 可在该窗口编辑代码或设计用户界面，例如带有按钮和文本框的窗口。

- [“输出”窗口](../../ide/reference/output-window.md)（底部中心）是 Visual Studio 发送通知（例如，调试和错误消息、编译器警告、发布状态消息等）的位置。 每个消息源都有自己的选项卡。

- 利用版本控制技术（如 [Git](https://git-scm.com/) 和 [Team Foundation 版本控制 (TFVC)](/azure/devops/repos/tfvc/overview?view=vsts)），[团队资源管理器](/azure/devops/user-guide/work-team-explorer?view=vsts)（右下方）可让你跟踪工作项并与他人共享代码。

## <a name="editions"></a>版本

Visual Studio 适用于 Windows 和 Mac。 [Visual Studio for Mac](/visualstudio/mac/) 的许多功能与 Visual Studio 2017 相同，并针对开发跨平台应用和移动应用进行了优化。 本文重点介绍 Visual Studio 2017 的 Windows 版本。

Visual Studio 2017 有三个版本：社区版、专业版和企业版。 请参阅[比较 Visual Studio 2017 IDE](https://visualstudio.microsoft.com/vs/compare/)，了解各个版本支持哪些功能。

## <a name="popular-productivity-features"></a>高效性方面的常用功能

Visual Studio 中的一些常用功能可帮助你在开发软件时提高工作效率，这些功能包括：

- 波形曲线和[快速操作](../../ide/quick-actions.md)

   波形曲线是波浪形下划线，它可以在键入时对代码中的错误或潜在问题发出警报。 这些可视线索使你能立即修复问题，而无需等待在生成期间或运行程序时发现错误。 如果将鼠标悬停在波形曲线上，将看到关于此错误的其他信息。 左边距中也可能会出现一个灯泡，提供修复此错误的“快速操作”建议。

   ::: moniker range="vs-2017"

   ![Visual Studio 中的波形曲线](media/squiggles-error.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio 中的波形曲线](media/vs-2019/squiggles-error.png)

   ::: moniker-end

- [重构](../../ide/refactoring-in-visual-studio.md)

   重构包括智能重命名变量、将一个或多个代码行提取到新方法中、更改方法参数的顺序等操作。

   ::: moniker range="vs-2017"

   ![在 Visual Studio 中重构菜单](media/refactoring-menu.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![在 Visual Studio 中重构菜单](media/vs-2019/refactorings-menu.png)

   ::: moniker-end

- [IntelliSense](../../ide/using-intellisense.md)

   IntelliSense 由一组功能构成，它可用于在编辑器中直接显示代码相关信息，还能在某些情况下编写小段代码。 如同在编辑器中拥有了基本文档内联，从而节省了在其他位置查看类型信息的时间。 IntelliSense 功能因语言而异。 有关详细信息，请参阅 [C# IntelliSense](../../ide/visual-csharp-intellisense.md)、[Visual C++ IntelliSense](../../ide/visual-cpp-intellisense.md)、[JavaScript IntelliSense](../../ide/javascript-intellisense.md) 和 [Visual Basic IntelliSense](../../ide/visual-basic-specific-intellisense.md)。 下图显示了 IntelliSense 如何显示类型的成员列表：

   ::: moniker range="vs-2017"

   ![Visual Studio 成员列表](media/intellisense-list-members.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio 成员列表](media/vs-2019/intellisense-list-members.png)

   ::: moniker-end

- 搜索框

   visual Studio 有时会因为有如此多的菜单、选项和属性而让人不知所措。 使用搜索框可以在 Visual Studio 中快速找到所需内容。 开始键入要查找内容的名称时，Visual Studio 会列出结果，这些结果可以准确地将你导向目标位置。 如果需要向 Visual Studio 添加功能，例如添加对其他编程语言的支持，可使用搜索框提供的结果打开 Visual Studio 安装程序以安装工作负载或单个组件。

   > [!TIP]
   > 按 Ctrl+Q 作为启动搜索框的快捷方式   。

   ::: moniker range="vs-2017"

   ![Visual Studio 2017 中的“快速启动”搜索框](../media/quick-launch-nuget.png)

   有关详细信息，请参阅[快速启动](../../ide/reference/quick-launch-environment-options-dialog-box.md)。

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 中的搜索框](media/vs-2019/quick-launch.png)

   ::: moniker-end

- [Live Share](/visualstudio/liveshare/)

   与他人实时协作编辑和调试，无需考虑应用类型或编程语言。 可以即时且安全地共享项目，并根据需要调试会话、终端实例、localhost Web 应用和语音呼叫等。

- [调用层次结构](../../ide/reference/call-hierarchy.md)

   “调用层次结构”窗口显示调用所选方法的方法  。 考虑更改或删除方法时，或者尝试追踪 bug 时，这可能是有用的信息。

   ::: moniker range="vs-2017"

   ![Visual Studio 中的“调用层次结构”窗口](media/call-hierarchy.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio 中的“调用层次结构”窗口](media/vs-2019/call-hierarchy.png)

   ::: moniker-end

- [CodeLens](../../ide/find-code-changes-and-other-history-with-codelens.md)

   CodeLens 可帮助查找代码引用、代码更改、链接错误、工作项、代码评审和单元测试，所有操作都在编辑器上进行。

   ::: moniker range="vs-2017"

   ![Visual Studio 中的 CodeLens](media/codelens.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio 中的 CodeLens](media/vs-2019/codelens.png)

   ::: moniker-end

- [转到定义](../../ide/go-to-and-peek-definition.md)

   “转到定义”功能可将你直接带到定义函数或类型的位置。

   ::: moniker range="vs-2017"

   ![Visual Studio 2017 中的“转到定义”](media/go-to-definition-menu.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 中的“转到定义”](media/vs-2019/go-to-definition-menu.png)

   ::: moniker-end

- [查看定义](../../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)

   “速览定义”窗口显示方法或类型的定义，而无需实际打开一个单独的文件  。

   ::: moniker range="vs-2017"

   ![Visual Studio 中的“速览定义”](media/peek-definition.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Visual Studio 中的“速览定义”](media/vs-2019/peek-definition.png)

   ::: moniker-end

## <a name="install-the-visual-studio-ide"></a>安装 Visual Studio IDE

在本部分中，你将创建一个简单的项目来尝试可在 Visual Studio 中执行的一些操作。 你将更改颜色主题，使用 [IntelliSense](../../ide/using-intellisense.md) 作为编码辅助，并调试应用，以便在程序执行期间查看变量的值。

::: moniker range="vs-2017"

首先，请[下载 Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) 并将其安装到你的系统上。 通过模块化安装程序，可以选择和安装工作负荷。工作负荷是你习惯使用的编程语言或平台所需的一些功能  。 若要执行[创建程序](#create-a-program)所需的步骤，请务必在安装过程中选择“.NET Core 跨平台开发”工作负载  。

::: moniker-end

::: moniker range=">=vs-2019"

首先，请[下载 Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019) 并将其安装到你的系统上。 通过模块化安装程序，可以选择和安装工作负荷。工作负荷是你习惯使用的编程语言或平台所需的一些功能  。 若要执行[创建程序](#create-a-program)所需的步骤，请务必在安装过程中选择“.NET Core 跨平台开发”工作负载  。

::: moniker-end

![Visual Studio 安装程序中的 .NET Core 跨平台开发工作负载](../media/dotnet-core-cross-platform-workload.png)

首次打开 Visual Studio 时，可选择使用 Microsoft 帐户或者工作或学校帐户[登录](../../ide/signing-in-to-visual-studio.md)。

## <a name="customize-visual-studio"></a>自定义 Visual Studio

可个性化设置 Visual Studio 用户界面，包括更改默认颜色主题。

### <a name="change-the-color-theme"></a>更改颜色主题

更改为“深色”主题  ：

::: moniker range="vs-2017"

1. 打开 Visual Studio。

::: moniker-end

::: moniker range=">=vs-2019"

1. 打开 Visual Studio。 在“启动”窗口中，选择“继续但无需代码”  。

   ![Visual Studio 2019 中的“启动”窗口](media/vs-2019/continue-without-code.png)

   IDE 将随即打开。

::: moniker-end

2. 在菜单栏中，选择“工具” > “选项”，打开“选项”对话框    。

3. 在“环境” > “常规”选项页上，将选择的“颜色主题”更改为“深色”，然后选择“确定”      。

   ![将 Visual Studio 中的“颜色主题”更改为“深色”](media/change-color-theme.png)

   此时，整个 IDE 的颜色主题更改为“深色”  。

   ::: moniker range="vs-2017"

   ![深色主题中的 Visual Studio](../../ide/media/quickstart-personalize-dark-theme.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![深色主题中的 Visual Studio](media/vs-2019/dark-theme.png)

   ::: moniker-end

### <a name="select-environment-settings"></a>选择环境设置

接下来，我们将把 Visual Studio 配置为，使用可满足 Visual Basic 开发人员需求的环境设置。

1. 在菜单栏上，选择“工具” > “导入和导出设置”   。

2. 在“导入和导出设置向导”  中，依次选择第一页上的“重置所有设置”  和“下一步”  。

3. 在“保存当前设置”  页上，依次选择确定是否保存当前设置的选项和“下一步”  。 （如果尚未自定义任何设置，请选择“不，只重置设置，同时覆盖我的当前设置”  。）

4. 在“选择默认设置集合”  页上，依次选择“Visual Basic”  和“完成”  。

5. 在“重置完成”  页上，选择“关闭”  。

若要了解有关 IDE 个性化设置的其他方法，请参阅[个性化设置 Visual Studio](../../ide/personalizing-the-visual-studio-ide.md)。

## <a name="create-a-program"></a>创建程序

现在我们来深入了解并创建一个简单的程序。

::: moniker range="vs-2017"

1. 在 Visual Studio 菜单栏上，依次选择 **“文件”** >“新建项目”  。

   ![菜单栏上的“文件”>“新建项目”](media/file-new-project-menu.png)

   “新建项目”  对话框中会显示几个项目模板  。 模板包含给定项目类型所需的基本文件和设置。

1. 依次选择“Visual Basic”  下的“.NET Core”  类别和“控制台应用(.NET Core)”  模板。 在“名称”文本框中，键入“HelloWorld”，然后选择“确定”按钮    。

   ![.NET Core 应用模板](media/overview-npd.png)

   > [!NOTE]
   > 如果未看到“.NET Core”类别，则需要安装“.NET Core 跨平台开发”工作负载   。 为此，选择“新建项目”  对话框左下角的“打开 Visual Studio 安装程序”  链接。 “Visual Studio 安装程序”打开后，向下滚动并选择“.NET Core 跨平台开发”工作负载，然后选择“修改”   。

   Visual Studio 随即创建项目。 它是简单的“Hello World”应用程序，可调用 <xref:System.Console.WriteLine?displayProperty=nameWithType> 方法在控制台窗口中 显示文本字符串“Hello World!”。

   稍后，将看到类似于以下的内容：

   ![Visual Studio IDE](media/overview-ide-console-app.png)

   应用的 Visual Basic 代码会显示在编辑窗口中，占据大部分空间。 请注意，文本已自动着色，用于指示代码的不同方面，如关键字或类型。 此外，代码中的垂直短虚线指示哪两个大括号相匹配，行号能够帮助你在以后查找代码。 可以通过选择带减号的小方形来折叠或展开代码块。 此代码大纲功能可以隐藏不需要的代码，最大程度地减少屏幕混乱。 右侧名为“解决方案资源管理器”的窗口中列出了项目文件  。

   ![具有红色框的 Visual Studio IDE](media/overview-ide-console-app-red-boxes.png)

   还提供了一些其他的菜单和工具窗口，但是现在我们继续下一步操作。

1. 现在启动该应用。 可从菜单栏的“调试”菜单中选择“开始执行(不调试)”，以执行此操作   。 还可按 Ctrl+F5   。

   ![“调试”>“开始执行(不调试)”菜单](../media/overview-start-without-debugging.png)

   Visual Studio 生成应用，控制台窗口随即打开并显示消息“Hello World!”  。 现在你拥有了一个正在运行的应用！

   ![控制台窗口](../media/overview-console-window.png)

1. 要关闭控制台窗口，请在键盘上按任意键。

1. 接下来，向应用添加一些附加代码。 在 `Console.WriteLine("Hello World!")` 行前面添加以下 Visual Basic 代码：

   ```vb
   Console.WriteLine("What is your name?")
   Dim name = Console.ReadLine()
   ```

   此代码在控制台窗口中显示“What is your name?”，然后等待用户输入文本并按 Enter 键   。

1. 将显示 `Console.WriteLine("Hello World!")` 的行更改为以下代码：

   ```vb
   Console.WriteLine("Hello " + name + "!")
   ```

1. 按“Ctrl  +F5  ”，以重新运行应用。

   Visual Studio 重新生成应用，控制台窗口随即打开，并提示输入姓名。

1. 在控制台窗口中输入姓名，并按 Enter  。

   ![控制台窗口输入](../media/overview-console-input.png)

1. 按任意键关闭控制台窗口，并停止正在运行的程序。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在 Visual Studio 菜单栏上，依次选择 **“文件”** >“新建项目”  。

   ![菜单栏上的“文件”>“新建项目”](media/vs-2019/file-new-project.png)

   随即打开“创建新项目”  窗口，并显示几个项目模板  。 模板包含给定项目类型所需的基本文件和设置。

1. 若要查找所需的模板，请在搜索框中键入或输入“.Net Core 控制台”  。 系统会自动根据输入的关键字筛选可用模板列表。 可以通过从“语言”  下拉列表选择“Visual Basic”  进一步筛选模板结果。

1. 选择“控制台应用 (.NET Core)”  模板，然后选择“下一步”  。

   ![在 Visual Studio 中创建新项目](media/vs-2019/create-new-project.png)

1. 在“配置新项目”  窗口中，在“项目名称”  框中输入“HelloWorld”  ，根据需要更改项目文件的目录位置，然后选择“创建”  。

   ![在 Visual Studio 中配置新项目](media/vs-2019/configure-new-project.png)

   Visual Studio 随即创建项目。 它是简单的“Hello World”应用程序，可调用 <xref:System.Console.WriteLine?displayProperty=nameWithType> 方法在控制台窗口中 显示文本字符串“Hello World!”。

   稍后，将看到类似于以下的内容：

   ![Visual Studio IDE](media/overview-ide-console-app.png)

   应用的 Visual Basic 代码会显示在编辑窗口中，占据大部分空间。 请注意，文本已自动着色，用于指示代码的不同方面，如关键字或类型。 此外，代码中的垂直短虚线指示哪两个大括号相匹配，行号能够帮助你在以后查找代码。 可以通过选择带减号的小方形来折叠或展开代码块。 此代码大纲功能可以隐藏不需要的代码，最大程度地减少屏幕混乱。 右侧名为“解决方案资源管理器”的窗口中列出了项目文件  。

   ![具有红色框的 Visual Studio IDE](media/overview-ide-console-app-red-boxes.png)

   还提供了一些其他的菜单和工具窗口，但是现在我们继续下一步操作。

1. 现在启动该应用。 可从菜单栏的“调试”菜单中选择“开始执行(不调试)”，以执行此操作   。 还可按 Ctrl+F5   。

   ![“调试”>“开始执行(不调试)”菜单](media/vs-2019/start-without-debugging.png)

   Visual Studio 生成应用，控制台窗口随即打开并显示消息“Hello World!”  。 现在你拥有了一个正在运行的应用！

   ![控制台窗口](../media/vs-2019/overview-console-window.png)

1. 要关闭控制台窗口，请在键盘上按任意键。

1. 接下来，向应用添加一些附加代码。 在 `Console.WriteLine("Hello World!")` 行前面添加以下 Visual Basic 代码：

   ```vb
   Console.WriteLine("What is your name?")
   Dim name = Console.ReadLine()
   ```

   此代码在控制台窗口中显示“What is your name?”，然后等待用户输入文本并按 Enter 键   。

1. 将显示 `Console.WriteLine("Hello World!")` 的行更改为以下代码：

   ```vb
   Console.WriteLine("Hello " + name + "!")
   ```

1. 按“Ctrl  +F5  ”，以重新运行应用。

   Visual Studio 重新生成应用，控制台窗口随即打开，并提示输入姓名。

1. 在控制台窗口中输入姓名，并按 Enter  。

   ![控制台窗口](../media/vs-2019/overview-console-input.png)

1. 按任意键关闭控制台窗口，并停止正在运行的程序。

::: moniker-end

## <a name="use-refactoring-and-intellisense"></a>使用重构和 IntelliSense

让我们了解一下如何借助[重构](../../ide/refactoring-in-visual-studio.md)和[IntelliSense](../../ide/using-intellisense.md) 更有效地进行编码。

首先，重命名 `name` 变量：

1. 双击 `name` 变量将其选中。

2. 为变量 username 键入新名称  。

   请注意，变量周围将显示灰色框且边距中会出现灯泡。

3. 选择灯泡图标，显示可用的[快速操作](../../ide/quick-actions.md)。 选择“将 'name' 重命名为 'username'”  。

   ![Visual Studio 中的重命名操作](media/rename-quick-action.png)

   该变量会在整个项目中进行重命名，本例中只有两处。

4. 接下来介绍 IntelliSense。 在 `Console.WriteLine("Hello " + username + "!")` 行下方，键入以下代码片段：

    ```vb
   Dim now = Date.
   ```

   此时，框中显示 <xref:System.DateTime> 类的成员。 另外，当前所选成员的说明会显示在单独的框中。

   ![Visual Studio 中的 IntelliSense 列表成员](media/intellisense-list-members.png)

5. 通过双击选择成员“Now”  （类属性），或通过使用向上箭头或向下箭头并按 Tab  键来选择此成员。

6. 在它的下方，键入或粘贴以下代码行：

   ```vb
   Dim dayOfYear = now.DayOfYear
   Console.Write("Day of year: ")
   Console.WriteLine(dayOfYear)
   ```

   > [!TIP]
   > <xref:System.Console.Write%2A?displayProperty=nameWithType> 与 <xref:System.Console.WriteLine%2A?displayProperty=nameWithType> 稍有不同，它在打印后不会添加行终止符。 这意味着发送到输出的下一段文本将打印在同一行上。 将鼠标悬停在代码中的每个方法上，即可查看其说明。

7. 接下来，我们将再次使用重构来使代码更加简洁。 单击 `Dim now = Date.Now` 行中的 `now` 变量。

   请注意，该行的边距中会显示一个小螺丝刀图标。

8. 单击螺丝刀图标，查看 Visual Studio 提供的建议。 在此示例中，它显示的是[内联临时变量](../../ide/reference/inline-temporary-variable.md)重构，可在不更改整体代码行为的情况下删除代码行：

   ![Visual Studio 中的内联临时变量重构](media/inline-temporary-variable-refactoring.png)

9. 单击“内联临时变量”，重构代码  。

::: moniker range="vs-2017"

10. 按 Ctrl+F5 重新运行程序   。 输出的内容与以下类似：

    ![显示程序输出的控制台窗口](../media/overview-console-final.png)

::: moniker-end

::: moniker range=">=vs-2019"

10. 按 Ctrl+F5 重新运行程序   。 输出的内容与以下类似：

    ![显示程序输出的控制台窗口](../media/vs-2019/overview-console-final.png)

::: moniker-end

## <a name="debug-code"></a>调试代码

编写代码时，需要运行并测试该代码是否存在 bug。 可通过 Visual Studio 的调试系统逐句执行代码，一次执行一条语句，逐步检查变量。 可设置停止在特定行执行代码的断点  。 可观察变量的值如何随代码运行而更改等。

通过设置断点，可查看程序处于飞行模式时 `username` 变量的值。

1. 查找显示 `Console.WriteLine("Hello " + username + "!")` 的代码行。 要在此代码行上设置一个断点，即让程序在该行暂停执行，请单击编辑器的最左侧边距。 还可单击代码行上的任意位置，然后按 F9  。

   此时，最左侧边距中将显示一个红圈，代码突出显示为红色。

   ![Visual Studio 中代码行上的断点](media/breakpoint.png)

1. 选择“调试” > “启动调试”或按 F5，开始调试    。

1. 控制台窗口出现并询问姓名时，请键入姓名，然后按 Enter  。

   Visual Studio 代码编辑器重新获得焦点，有断点的代码行突出显示为黄色。 这表示它是程序将执行的下一个代码行。

1. 将鼠标悬停在 `username` 变量上，即可查看它的值。 或者，可以右键单击 `username` 并选择“添加监视”，将变量添加到监视窗口，这样也可查看它的值   。

   ![在 Visual Studio 中进行调试时的变量值](media/debugging-variable-value.png)

1. 若要让程序运行至结束，请再次按 F5  。

有关在 Visual Studio 中进行调试的详细信息，请参阅[调试器功能简介](../../debugger/debugger-feature-tour.md)。

## <a name="next-steps"></a>后续步骤

查看下述一篇介绍性的文章，进一步了解 Visual Studio：

> [!div class="nextstepaction"]
> [了解如何使用代码编辑器](tutorial-editor.md)

> [!div class="nextstepaction"]
> [了解项目和解决方案](tutorial-projects-solutions.md)

## <a name="see-also"></a>请参阅

- 发现[更多 Visual Studio 功能](../../ide/advanced-feature-overview.md)
- 访问 [visualstudio.microsoft.com](https://visualstudio.microsoft.com/vs/)
- 阅读 [Visual Studio 博客](https://devblogs.microsoft.com/visualstudio/)