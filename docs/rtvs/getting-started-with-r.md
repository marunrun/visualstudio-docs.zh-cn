---
title: R 教程入门
description: 在 Visual Studio 中使用 R 的演练，其中包括项目创建、交互式窗口、代码编辑和调试。
ms.date: 06/29/2017
ms.topic: tutorial
author: kraigb
ms.author: kraigb
manager: jillfra
ms.workload:
- data-science
ms.openlocfilehash: df46a2731f9923d85a16082f96c44947099db592
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "63000493"
---
# <a name="get-started-with-r-tools-for-visual-studio"></a>Visual Studio 中的 R 工具入门

安装了针对 Visual Studio 的 R 工具 (RTVS)（请参阅[安装](installing-r-tools-for-visual-studio.md)）后，很快就能亲身感受这些工具提供的体验。

## <a name="create-an-r-project"></a>创建 R 项目

1. 打开 Visual Studio。
1. 依次选择“文件” **“新建”** “项目” (Ctrl > Shift**N)**  >    +  + 
1. 选择“模板” **“R”**  >   下的“R 项目”，指定项目的名称和位置，然后选择“确定”  ：

   ![Visual Studio 中 R（VS2017 中的 RTVS）的“新建项目”对话框](media/getting-started-01-new-project.png)

1. 创建项目后，将看到以下窗口：

    - 右侧是 Visual Studio 解决方案资源管理器，创建的项目将显示在其中一个包含的解决方案内  。 （解决方案可以包含任意数量不同类型的项目，请参阅[项目](r-projects-in-visual-studio.md)了解详细信息。
    - 左上角是新的 R 文件 (`script.R`)，可在其中使用 Visual Studio 的所有编辑功能编辑源代码。
    - 左下角是“R 交互”  窗口，可在其中以交互方式开发和测试代码。

> [!Note]
> 可以在没有打开任何项目，甚至加载了其他项目类型的情况下使用“R 交互”  窗口。 任何时候都只需选择“R 工具” **“窗口”** “R 交互窗口” >    >   即可。

## <a name="explore-the-interactive-window-and-intellisense"></a>了解交互窗口和 IntelliSense

1. 键入 `3 + 4` 然后按 Enter 查看结果，测试交互窗口是否正常运行  ：

    ![Visual Studio 2017 (VS2017) 中的 R 交互窗口](media/getting-started-02-interactive1.png)

1. 输入稍微复杂一点内容，如 `ds <- c(1.5, 6.7, 8.9) * 1:12`，然后输入 `ds` 查看结果：

    ![Visual Studio 中的 R 的其他交互示例](media/getting-started-03-interactive2.png)

1. 键入 `mean(ds)`，但请注意，键入 `m` 或 `me` 后，Visual Studio IntelliSense 会立即提供自动完成选项。 如果从列表中选择了所需完成选项并按 Tab 将其插入，可以使用箭头键或鼠标更改选定内容  。

    ![IntelliSense 会在输入代码时出现](media/getting-started-04-intellisense1.png)

1. 完成 `mean` 后，键入左括号 `(`，并注意 IntelliSense 如何提供关于函数的内联帮助：

    ![显示函数相关帮助的 IntelliSense](media/getting-started-05-intellisense2.png)

1. 完成行 `mean(ds)`，然后按 Enter 查看结果 (`[1] 39.51667`)。

1. 交互窗口已与帮助集成，因此输入 `?mean` 后，将在 Visual Studio 的“R 帮助”窗口中看到关于该函数的帮助  。 有关详细信息，请参阅[针对 Visual Studio 的 R 工具中的帮助](getting-started-help.md)。

    ![Visual Studio 中的 R 帮助窗口](media/getting-started-06-help.png)

1. 如果无法在交互窗口中直接显示输出，某些命令（如 `plot(1:100)`）将在 Visual Studio 中打开一个新窗口：

    ![Visual Studio 中的绘图显示](media/getting-started-07-plot-window.png)

使用交互窗口，还可查看历史记录、加载和保存工作区、附加到调试器，以及与源代码文件交互，无需复制粘贴操作。 有关详细信息，请参阅 [Working with the R Interactive Window](interactive-repl-for-r-in-visual-studio.md)（使用 R 交互窗口）。

## <a name="experience-code-editing-features"></a>体验代码编辑功能

简短地使用交互窗口可证明 IntelliSense 等基本编辑功能在代码编辑器中也适用。 如果输入与之前相同的代码，将出现相同的自动完成选项和 IntelliSense 提示，但输出并不相同。

通过在 .R  文件中编写代码，可一次性查看所有代码，还可更轻松地进行微小的更改，然后通过在交互窗口中运行代码快速查看结果。 可以根据需要在一个项目中包含任意数量的文件。 如果代码位于文件中，还可以在调试器中进行分步运行（本文稍后讨论）。 如果要通过开发计算算法和编写代码来操作一个或多个数据集（尤其是想要检查所有中间结果时），这些功能都十分有用。

例如，以下步骤将创建一小段代码，用于了解[中心极限定理](https://en.wikipedia.org/wiki/Central_limit_theorem)（维基百科）。 （此示例改编自 Paul Teetor 的 R 指南  。）

1. 在 `script.R` 编辑器中，输入以下代码：

    ```R
    mu <- 50
    stddev <- 1
    N <- 10000
    pop <- rnorm(N, mean = mu, sd = stddev)
    plot(density(pop), main = "Population Density", xlab = "X", ylab = "")
    ```

1. 若要快速查看结果，请选择所有代码 (Ctrl**A)，然后按 Ctrl**Enter，或右键单击并选择“交互执行”+   +   。 所有选定代码都在交互窗口中运行，就像直接键入一样，并且绘图窗口中将显示结果：

    ![Visual Studio 中的绘图显示](media/getting-started-08-plot1.png)

1. 对于单行，可随时通过按 Ctrl**Enter 在交互窗口中运行该行**+  。

> [!Tip]
> 了解编辑模式并按 Ctrl**Enter（或按 Ctrl**A 选择所有内容，然后按 Ctrl+Enter），快速运行代码   +   +  。 此方法比使用鼠标进行相同的操作更高效。
>
> 此外，还可以将绘图窗口拖放到 Visual Studio 框架外，放置在显示器上任何所需位置。 然后，可轻松将绘图窗口调整为所需大小，然后保存到图像或 PDF 文件中。

1. 再添加几行代码，将另一个绘图包括在内：

    ```R
    n <- 30
    samp.means <- rnorm(N, mean = mu, sd = stddev / sqrt(n))
    lines(density(samp.means))
    ```

1. 再次按 Ctrl**A 和 Ctrl**Enter 运行代码，生成以下结果+   +  ：

    ![Visual Studio 中更新后的双重绘图](media/getting-started-09-plot2.png)

1. 问题是第一个绘图确定了垂直刻度，因此无法容纳第二个绘图（使用 `lines`）。 若要纠正此问题，需要对 `ylim` 调用设置 `plot` 参数，但为了正确执行该操作，需要添加代码，计算最大垂直值。 在交互窗口中逐行执行该操作不太方便，因为需要在调用 `samp.means` 前重新排列代码才能使用 `plot`。 然而，在代码文件中，可以轻松执行相应编辑：

    ```R
    mu <- 50
    stddev <- 1
    N <- 10000
    pop <- rnorm(N, mean = mu, sd = stddev)

    n <- 30
    samp.means <- rnorm(N, mean = mu, sd = stddev / sqrt(n))
    max.samp.means <- max(density(samp.means)$y)

    plot(density(pop), main = "Population Density",
        ylim = c(0, max.samp.means),
        xlab = "X", ylab = "")
    lines(density(samp.means))
    ```

1. 再次按 Ctrl**A 和 Ctrl**Enter 可查看结果+   +  ：

    ![Visual Studio 中刻度适当的更新后双重绘图](media/getting-started-10-plot3.png)

在编辑器中还可以执行其他操作。 有关详细信息，请参阅[编辑 R 代码](editing-r-code-in-visual-studio.md)、[IntelliSense](r-intellisense.md) 和[代码片段](code-snippets-for-r.md)。

## <a name="debug-your-code"></a>调试代码

Visual Studio 的一个主要优势就是它的调试 UI。 RTVS 构建于这一坚实的基础之上，并增加了创新的 UI，如[变量资源管理器](variable-explorer.md)。 首先看一下调试。

1. 开始前，请重置当前工作区，使用“R 工具” **“会话”** “重置”菜单命令清除到目前为止完成的所有内容 >    >   。 默认情况下，在交互窗口中执行的所有操作都将累加到当前会话，然后还会供调试器使用。 通过重置会话，可确保调试会话启动时无预先存在的数据。 但是，重置命令不会影响 script.R 源文件，因为该文件在工作区之外进行管理和保存   。

1. 使用上一节中创建的 script.R 文件，在以  *开头的行上设置断点，方法是将插入符号放置于该行中，然后按 F9，或选择“调试”* “切换断点”菜单命令`pop <-`    >   。 或者，只需在该行的左边距（或装订线）处单击，该边距（或装订线）中将出现一个红色断点：

    ![在编辑器中设置断点](media/getting-started-11-debug1.png)

1. 选择工具栏上的“源化启动文件”按钮，选择“调试” *“源化启动文件”菜单项，或按 F5，使用 script.R 中的代码启动调试器*    >    。 Visual Studio 将进入调试模式，并开始运行代码。 但是，将在设置断点的行停止运行：

    ![在 Visual Studio 调试器中的断点处停止](media/getting-started-12-debug2.png)

1. 调试期间，Visual Studio 提供逐行执行代码的功能。 还可以单步执行或单步跳过函数，或者单步跳出函数以转到调用上下文。 可在“调试”  菜单、编辑器的右击上下文菜单和调试工具栏中找到这些功能以及其他功能：

    ![Visual Studio 中的调试工具栏](media/getting-started-13-debug3.png)

1. 如果在断点处停止，可以检查变量值。 找到 Visual Studio 中的“自动”  窗口，并选择底部名为“局部变量”  的选项卡。 “局部变量”  窗口将显示程序中当前位置的局部变量。 如果在之前设置的断点处停止，将看到尚未定义 `pop` 变量。 现在，如果使用“调试” **“逐过程执行”命令 (F10)，将显示**  的值 >    `pop`：

    ![Visual Studio 中的“局部变量”窗口](media/getting-started-14-debug4.png)

1. 若要检查不同范围（包括全局范围和包范围）内的变量，请使用[变量资源管理器](variable-explorer.md)。 变量资源管理器还提供以下功能：切换到含可排序列的表格视图、将数据导出到 CSV 文件。

    ![变量资源管理器的展开视图](media/variable-explorer-expanded-results.png)

1. 可继续逐行逐句执行程序，也可选择“继续”  (F5) 运行程序，直到完成（或下一个断点）  。

若要深入了解，请参阅[调试](debugging-r-in-visual-studio.md)和[变量资源管理器](variable-explorer.md)。

## <a name="next-steps"></a>后续步骤

本演练介绍了 R 项目的基础知识、交互窗口的使用、代码编辑和在 Visual Studio 中进行调试。 若要继续了解更多功能，请参阅以下文章以及目录中显示的文章：

- [示例项目](getting-started-samples.md)
- [编辑代码](editing-r-code-in-visual-studio.md)
- [调试](debugging-r-in-visual-studio.md)
- [工作区](r-workspaces-in-visual-studio.md)
- [可视化数据](visualizing-data-with-r-in-visual-studio.md)
