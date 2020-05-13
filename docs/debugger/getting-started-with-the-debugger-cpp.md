---
title: 教程：调试 C++ 代码
description: 了解如何启动 Visual Studio 调试器、单步执行代码以及检查数据。
ms.custom: debug-experiment, seodec18, get-started
ms.date: 02/04/2020
ms.technology: vs-ide-debug
ms.topic: tutorial
dev_langs:
- C++
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 47b1a031a6c4e4e823a1fcc12aba228750aee27e
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "77091803"
---
# <a name="tutorial-learn-to-debug-c-code-using-visual-studio"></a>教程：了解如何使用 Visual Studio 调试 C++ 代码

本文通过分步演练介绍了 Visual Studio 调试器的功能。 如果需要更加深入地了解调试器功能，请参阅[初探调试器](../debugger/debugger-feature-tour.md)。 当你调试应用时，通常意味着运行附带有调试器的应用程序  。 执行此操作时，调试器在运行过程中可提供许多方法让你查看代码的情况。 你可以逐步浏览代码、查看变量中存储的值、设置对变量的监视以查看值何时改变、检查代码的执行路径、查看代码分支是否正在运行等等。 如果这是你第一次尝试调试代码，可能需要在浏览本文之前阅读[零基础调试](../debugger/debugging-absolute-beginners.md)。

虽然演示应用为 C++，但大多数功能都适用于 C#、Visual Basic、F#、Python、JavaScript 和 Visual Studio 支持的其他语言（F# 不支持“编辑并继续”。 F# 和 JavaScript 不支持“自动”窗口  ）。 屏幕截图为 C++。

在本教程中，你将：

> [!div class="checklist"]
> * 启动调试器并命中断点。
> * 了解在调试器中逐步执行代码的命令
> * 检查数据提示和调试器窗口中的变量
> * 检查调用堆栈

## <a name="prerequisites"></a>先决条件

::: moniker range=">=vs-2019"

须安装 Visual Studio 2019 且具有“使用 C++ 的桌面开发”工作负载  。

::: moniker-end
::: moniker range="vs-2017"

须安装 Visual Studio 2017 且具有“C++ 桌面开发”工作负载  。

::: moniker-end

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

如果需要安装工作负载但已有 Visual Studio，请转到“工具”   > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 Visual Studio 安装程序启动。 选择“使用 C++ 的桌面开发”工作负载，然后选择“修改”按钮   。

## <a name="create-a-project"></a>创建项目

首先，创建 C++ 控制台应用程序项目。 项目类型随附了所需的全部模板文件，无需添加任何内容！

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

2. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

3. 在“新建项目”对话框左侧的窗格中，展开“Visual C++”，然后选择“Windows 桌面”    。 在中间窗格中，选择“Windows 控制台应用程序”  。 然后将项目命名为 get-started-debugging  。

     如果没有看到“控制台应用”项目模板，请选择“新建项目”对话框左侧窗格中的“打开 Visual Studio 安装程序”链接    。 Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改”   。

4. 单击 **“确定”** 。

   此时，Visual Studio 将打开新项目。

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio 2019。

   如果开始窗口未打开，请选择“文件”>“开始窗口”   。

1. 在“开始”窗口上，选择“创建新项目”  。

1. 在“创建新项目”窗口的搜索框中输入或键入“控制台”   。 接下来，从“语言”列表中选择“C++”，然后从“平台”列表中选择“Windows”   。 

   应用语言和平台筛选器之后，选择“控制台应用”模板，然后选择“下一步”   。

   ![为“控制台应用”选择 C++ 模板](../debugger/media/vs-2019/get-started-create-console-project-cpp.png)

   > [!NOTE]
   > 如果未看到“控制台应用”模板，则可以通过“创建新项目”窗口安装该模板   。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。 然后，在 Visual Studio 安装程序中，选择“使用 C++ 的桌面开发”工作负载  。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“get-started-debugging”    。 然后，选择“创建”  。

   此时，Visual Studio 将打开新项目。

::: moniker-end

## <a name="create-the-application"></a>创建应用程序

1. 在 get-started-debugging.cpp 中，使用以下代码替换所有默认代码  ：

    ```cpp
    #include <string>
    #include <vector>
    #include <iostream>

    void SendMessage(const std::wstring& name, int msg)
    {
        std::wcout << L"Hello, " << name << L"! Count to " << msg << std::endl;
    }

    int main()
    {
        std::vector<wchar_t> letters = { L'f', L'r', L'e', L'd', L' ', L's', L'm', L'i', L't', L'h' };
        std::wstring name = L"";
        std::vector<int> a(10);
        std::wstring key = L"";

        for (int i = 0; i < letters.size(); i++)
        {
            name += letters[i];
            a[i] = i + 1;
            SendMessage(name, a[i]);
        }
        std::wcin >> key;
        return 0;
    }
    ```

## <a name="start-the-debugger"></a>启动调试器！

1. 按 F5  （“调试”>“开始调试”  ）或调试工具栏中的“开始调试”  按钮![开始调试](../debugger/media/dbg-tour-start-debugging.png "开始调试")。

     通过 **F5** 启动应用时，调试器会附加到应用进程，但现在我们还未执行任何特殊操作来检查代码。 因此应用只会加载，控制台输出如你所见。

    ```cmd
    Hello, f! Count to 1
    Hello, fr! Count to 2
    Hello, fre! Count to 3
    Hello, fred! Count to 4
    Hello, fred ! Count to 5
    Hello, fred s! Count to 6
    Hello, fred sm! Count to 7
    Hello, fred smi! Count to 8
    Hello, fred smit! Count to 9
    Hello, fred smith! Count to 10
    ```

     在本教程中，我们将使用调试器仔细查看此应用，并查看调试器功能。

2. 按红色的停止![停止调试](../debugger/media/dbg-tour-stop-debugging.png "停止调试")按钮 (Shift + F5) 来停止调试器   。

3. 在控制台窗口中，按某个键和 Enter 来关闭控制台窗口  。

## <a name="set-a-breakpoint-and-start-the-debugger"></a>设置断点并启动调试器

1. 在 `main` 函数的 `for` 循环中，通过单击以下代码行的左边距来设置断点：

    `name += letters[i];`

    设置断点的位置会出现一个红色圆圈的![断点](../debugger/media/dbg-breakpoint.png "断点")。

    断点是可靠调试的最基本和最重要的功能之一。 断点指示 Visual Studio 应在哪个位置挂起你的运行代码，以使你可以查看变量的值或内存的行为，或确定代码的分支是否运行。

2. 按“F5”  或“开始调试”  按钮![开始调试](../debugger/media/dbg-tour-start-debugging.png "开始调试")，应用随即启动，调试器将运行到你设置断点的代码行。

    ![设置并命中断点](../debugger/media/get-started-set-breakpoint-cpp.png)

    黄色箭头表示调试器暂停处的语句，它还在同一点上暂停应用执行（此语句尚未执行）。

     如果应用尚未运行，则按 F5 会启动调试器并在第一个断点处停止  。 否则，按 F5 将继续运行应用至下一个断点  。

    当你知道要详细检查的代码行或代码段时，断点功能非常有用。 有关可设置的不同类型断点（如条件断点）的信息，请参阅[使用断点](../debugger/using-breakpoints.md)。

## <a name="navigate-code-in-the-debugger-using-step-commands"></a>使用单步执行命令在调试器中导航代码

大多数情况下，我们使用键盘快捷方式，因为这是在调试器中快速执行应用的好方法（括号中显示了等效的命令，如菜单命令）。

1. 在 `main` 方法中的 `for` 循环中暂停时，按两次 F11（或选择“调试”>“单步执行”）前进到 `SendMessage` 方法调用   。

     按两次 F11 后，应位于以下代码行  ：

     `SendMessage(name, a[i]);`

1. 再按一次 F11 单步执行到 `SendMessage` 方法  。

     黄色指针会前进到 `SendMessage` 方法。

     ![使用 F11 单步执行代码](../debugger/media/get-started-f11-cpp.png "F10 单步执行")

     F11 是“单步执行”命令，每按一次，应用就执行下一个语句  。 F11 是一种以最详尽方式检查执行流的好方法。 （为了更快地浏览代码，我们还向你展示一些其他选项。）默认情况下，调试器会跳过非用户代码（如果需要更多详细信息，请参阅[仅我的代码](../debugger/just-my-code.md)）。

     假设你已完成了对 `SendMessage` 方法的检查，并且希望退出该方法但保持位于调试器中。 可使用“单步跳出”命令执行此操作  。

1. 按 Shift + F11（或“调试”>“单步跳出”）    。

     此命令将恢复应用执行（并使调试器前进），直到当前方法或函数返回。

     你应当回到 `main` 方法的 `for` 循环，在 `SendMessage` 方法调用处暂停。

1. 多按几次 F11，直到再次返回到 `SendMessage` 方法调用  。

1. 在方法调用处暂停时，按一次 F10（或选择“调试”>“单步跳过”）   。

     ![使用 F10 单步跳过代码](../debugger/media/get-started-step-over-cpp.png "F10 单步跳过")

     请注意，这次调试器不会单步执行 `SendMessage` 方法。 按 F10 将使调试器前进，但不会单步执行应用代码中的函数或方法（代码仍将执行）  。 通过在进行 `SendMessage` 方法调用时按“F10”（而不是“F11”），我们跳过了 `SendMessage` 的实现代码（我们现在可能对此不感兴趣）   。 有关在代码中进行移动的不同方法的详细信息，请参阅[浏览调试器中的代码](../debugger/navigating-through-code-with-the-debugger.md)。

## <a name="navigate-code-using-run-to-click"></a>使用“运行时单击”导航代码

1. 按 F5 前进到断点  。

1. 在代码编辑器中，向下滚动并将鼠标悬停在 `SendMessage` 方法中的 `std::wcout` 函数上，直到左侧出现绿色的“运行时单击”按钮![运行时单击](../debugger/media/dbg-tour-run-to-click.png "运行时单击")  。 按钮的工具提示显示“将执行运行到此处”。

     ![使用“运行时单击”功能](../debugger/media/get-started-run-to-click-cpp.png "运行时单击")

   > [!NOTE]
   > “运行时单击”是 [!include[vs_dev15](../misc/includes/vs_dev15_md.md)] 中的新增按钮  。 （如果未看到绿色箭头按钮，请在此示例中改为使用 F11 以使调试器前进到正确的位置。  ）

2. 单击“运行时单击”  按钮![运行时单击](../debugger/media/dbg-tour-run-to-click.png "运行时单击")。

    调试器会前进到 `std::wcout` 函数。

    使用此按钮类似于设置临时断点。 “运行时单击”对于快速到达应用代码的可见区域十分方便（你可在任何打开的文件中单击）  。

## <a name="restart-your-app-quickly"></a>快速重启应用

单击调试工具栏中的“重启”![重启应用](../debugger/media/dbg-tour-restart.png "重启应用")按钮 (Ctrl + Shift + F5)     。

当你按下“重启”时，与停止应用并重启调试器相比，它节省了时间  。 调试器在执行代码命中的第一个断点处暂停。

调试器再次在你之前在 `for` 循环上设置的断点处停止。

## <a name="inspect-variables-with-data-tips"></a>使用数据提示检查变量

允许你检查变量的功能是调试器最有用的功能之一，并且有不同的方法来执行此操作。 通常，当尝试调试问题时，你试图找出变量是否存储了你期望它们在特定时间具有的值。

1. 在 `name += letters[i]` 语句上暂停时，将鼠标悬停在 `letters` 变量上，会看到其默认值 `size={10}`。

1. 展开 `letters` 变量，查看其属性，其中包括变量包含的所有元素。

1. 接下来，将鼠标悬停在 `name` 变量上，会看到其当前值为空字符串。

1. 多按几次 F5（或“调试” > “继续”），通过 `for` 循环执行多次循环访问，再次在断点处暂停，每次都将鼠标悬停在 `name` 变量上以检查其值    。

     ![查看数据提示](../debugger/media/get-started-data-tip-cpp.png "查看数据提示")

     变量的值随 `for` 循环的每次迭代而更改，显示的值依次为 `f`、`fr`、`fre`，依此类推。

     通常情况下，在调试时，需要快速检查变量的属性值，以查看它们是否存储了你希望它们存储的值，可根据数据提示执行此操作。

## <a name="inspect-variables-with-the-autos-and-locals-windows"></a>使用“自动”和“局部变量”窗口检查变量

1. 查看代码编辑器底部的“自动”窗口  。

    如果已关闭，请依次选择“调试” > “Windows” > “自动”，在调试器中暂停时将其打开    。

    在“自动”窗口中，可看到变量及其当前值  。 “自动”窗口显示当前行或前一行使用的所有变量（检查文档中特定于语言的行为）  。

1. 接下来，我们来看看“自动”窗口旁边的选项卡中的“局部变量”窗口   。

1. 展开 `letters` 变量以显示其包含的元素。

     ![检查局部变量窗口中的变量](../debugger/media/get-started-locals-window-cpp.png "“局部变量”窗口")

    “局部变量”窗口显示当前[作用域](https://www.wikipedia.org/wiki/Scope_(computer_science))中的变量，即当前执行上下文  。

## <a name="set-a-watch"></a>设置监视

1. 在主代码编辑器窗口中，右键单击 `name` 变量，然后选择“添加监视”  。

    “监视”窗口将在代码编辑器的底部打开  。 可使用“监视”窗口指定要关注的变量（或表达式）  。

    现在，你在 `name` 变量上设置好了监视，当你在调试器中移动时，可看到其值发生变化。 与其他变量窗口不同，“监视”窗口始终显示你正在监视的变量（当超出作用域时，它们会变灰）  。

## <a name="examine-the-call-stack"></a>检查调用堆栈

1. 在 `for` 循环中暂停时，单击“调用堆栈”窗口，默认情况下，该窗口在右下方窗格中打开  。

    如果已关闭，请依次选择“调试” > “Windows” > “调用堆栈”，在调试器中暂停时将其打开    。

2. 单击多次 F11，直至看到调试器在 `SendMessage` 方法中暂停  。 查看“调用堆栈”窗口  。

    ![检查调用堆栈](../debugger/media/get-started-call-stack-cpp.png "检查调用堆栈")

    “调用堆栈”窗口显示方法和函数被调用的顺序  。 最上面一行显示当前函数（此应用中的 `SendMessage` 方法）。 第二行显示 `SendMessage` 是从 `main` 方法调用的，依此类推。

   > [!NOTE]
   > “调用堆栈”窗口类似于某些 IDE（如 Eclipse）中的调试透视图  。

    调用堆栈是检查和理解应用执行流的好方法。

    可双击代码行来查看该源代码，这也会更改调试器正在检查的当前作用域。 此操作不会使调试器前进。

    还可使用“调用堆栈”窗口中的右键单击菜单执行其他操作  。 例如，你可将断点插入到指定的函数中，使用“运行到光标处”推进调试器，然后检查源代码  。 有关详细信息，请参阅[如何：检查调用堆栈](../debugger/how-to-use-the-call-stack-window.md)。

## <a name="change-the-execution-flow"></a>更改执行流

1. 按两次 F11 以运行 `std::wcout` 函数  。

1. 在 `SendMessage` 方法调用中暂停调试器后，使用鼠标抓住左侧的黄色箭头（执行指针），将黄色箭头向上移动一行，返回到 `std::wcout`。

1. 按下 F11  。

    调试器将重新运行 `std::wcout` 函数（你会在控制台窗口输出中看到）。

    通过更改执行流，你可以进行测试不同代码执行路径或重新运行代码等操作，而无需重启调试器。

    > [!WARNING]
    > 通常你需要小心使用此功能，工具提示中会出现警告。 你也可能会看到其他警告。 移动指针无法将应用程序还原到更早的应用状态。

1. 按 F5 继续运行应用  。

    恭喜你完成本教程！

## <a name="next-steps"></a>后续步骤

在本教程中，你已了解了如何启动调试器、逐步执行代码以及检查变量。 你可能会希望更深入地了解调试器功能以及查看指向更多信息的链接。

> [!div class="nextstepaction"]
> [初探调试器](../debugger/debugger-feature-tour.md)

