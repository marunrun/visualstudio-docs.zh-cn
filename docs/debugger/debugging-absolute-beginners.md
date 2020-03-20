---
title: 零基础调试代码
description: 如果是第一次进行调试，请了解一些原则，以帮助你使用 Visual Studio 在调试模式下运行应用
ms.date: 02/14/2020
ms.topic: tutorial
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5c3cf9d5e4d72ed316344d1bda930d0416e9efe5
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "77416389"
---
# <a name="how-to-debug-for-absolute-beginners"></a>零基础调试的方法

毫无疑问，软件开发人员编写的代码并不总是按照预期行事。 有时它执行一些完全不同的操作！ 发生这种情况时，下一个任务是找出原因。尽管我们可能会一直盯着代码看几个小时，但使用调试工具或调试程序会更轻松且更高效。

遗憾的是，调试程序无法神奇地揭示代码中的所有问题或“bug”。 调试意味着在 Visual Studio 等调试工具中逐步运行代码，以找到导致编程错误的确切位置  。 那么就可以了解代码中所需的更正，并且调试工具通常允许进行临时更改，以便可以继续运行该程序。

有效地使用调试程序也是一项需要时间和实践来学习的技能，但从根本上来说这是每个软件开发人员的一项基本任务。 本文随后将介绍调试的核心原则并提供入门提示。

## <a name="clarify-the-problem-by-asking-yourself-the-right-questions"></a>通过问自己正确的问题来澄清问题

在尝试修复之前，这有助于阐明遇到的问题。 我们预计代码已出现了问题，否则你不会试图弄清楚对其进行调试的方法！ 因此，开始调试之前，请确保你已确定要解决的问题：

* 期望代码可执行哪些操作？

* 相反，发生了什么？

    如果运行应用时遇到了错误（异常），这可能是一件好事！ 异常是运行代码时遇到的意外事件，通常是某种错误。 调试工具有助于找到代码中发生异常的确切位置并且帮助调查可能的修复方法。

    如果发生了其他情况，问题的症状是什么？ 是否已经怀疑代码中出现此问题的位置？ 例如，如果代码显示了某些文本，但文本不正确，则你知道数据已损坏或设置显示文本的代码存在某种 bug。 通过逐步调试调试程序中的代码，可以检查变量的每个更改，以准确地发现分配时间以及分配不正确值的方式。

## <a name="examine-your-assumptions"></a>检查假设

在调查 bug 或错误之前，请考虑你期望获得某个结果的假设。 即使正在查看调试程序中问题的成因，隐藏或未知的假设也可能妨碍识别问题。 可能有一长串可能的假设！ 以下是要询问的一些问题，以质疑你的假设。

* 是否使用正确的 API（即正确的对象、函数、方法或属性）？ 正在使用的 API 可能无法按照你的想法执行操作。 （在调试程序中检查 API 调用之后，解决此问题可能需要转至文档以帮助识别正确的 API。）

* 是否正确地使用了 API？ 也许使用了正确的 API，但方法不正确。

* 代码是否包含任何拼写错误？ 很难发现某些拼写错误（例如变量名的简单拼写错误），尤其是在使用不需要在使用变量之前声明变量的语言时。

* 是否对代码进行了更改，并假设它与所看到的问题无关？

* 是否期望对象或变量包含与实际情况不同的特定值（或某种类型的值）？

* 是否知道代码的含义？ 调试其他人的代码通常更加困难。 如果不是你的代码，则可能需要花时间准确地了解代码的作用，然后才能有效地进行调试。

    > [!TIP]
    > 编写代码时，从小型代码开始，从有效的代码开始！ （优秀的示例代码在此处很有用。）有时，通过从演示尝试实现的核心任务的一小段代码开始，可以更轻松地修复大型或复杂的代码集。 然后，可以以增量方式来修改或添加代码，从而在每个点测试错误。

通过质疑假设，可以减少在代码中查找问题所需的时间。 此外可缩短解决问题所需的时间。

## <a name="step-through-your-code-in-debugging-mode-to-find-where-the-problem-occurred"></a>在调试模式中单步调试代码以查找问题发生的位置

正常运行应用时，仅在代码运行后才能看到错误和不正确的结果。 程序也可能会意外终止而不告知原因。

在调试程序中运行应用（也称为“调试模式”），这意味着调试程序会主动监视程序运行时发生的所有事情  。 此外允许在任何时候暂停应用以检查其状态，然后逐行单步调试代码以查看发生的每个细节。

在 Visual Studio 中，通过使用调试工具栏中的 F5（或“调试” > “开始调试”菜单按钮或“开始调试”按钮![开始调试](../debugger/media/dbg-tour-start-debugging.png "开始调试")来进入调试模式）     。 如果发生任何异常，则 Visual Studio 的异常帮助程序会找到发生异常的确切位置，并提供其他有用信息。 有关如何在代码中处理异常的详细信息，请参阅[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)。

如果未收到异常，则你可能清楚在代码中查找问题的位置。 可在此处结合使用断点  和调试器，这样便有机会更仔细地检查代码。 断点是可靠调试的最基本和最重要的功能。 断点指示 Visual Studio 应在何处暂停正在运行的代码，以查看变量的值或内存的行为，或代码运行的顺序。

在 Visual Studio 中，可通过单击代码行旁边的左边距来快速设置断点。 或将光标置于行并按 F9  。

为了帮助说明这些概念，我们将介绍一些已经存在多个 bug 的示例代码。 我们将使用 C#，但调试功能适用于 Visual Basic、C++、JavaScript、Python 和其他受支持的语言。

### <a name="create-a-sample-app-with-some-bugs"></a>创建示例应用（有一些 bug）

接下来，我们将创建具有几个 bug 的应用程序。

1. 必须已安装 Visual Studio 以及“NET 桌面开发”工作负载或“.NET Core 跨平台开发”工作负载，具体取决于要创建的应用类型   。

    如果尚未安装 Visual Studio，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/) 页免费安装。

    如果需要安装工作负载但已安装 Visual Studio，请单击“工具” > “获取工具和功能”   。 Visual Studio 安装程序启动。 选择“.NET Core 桌面开发”或“.NET Core 跨平台开发”工作负载，然后选择“修改”    。

1. 打开 Visual Studio。

    ::: moniker range=">=vs-2019"
    在“开始”窗口上，选择“创建新项目”  。 在搜索框中键入“控制台”，然后选择“控制台应用(.NET Core)”或“控制台应用(.NET Framework)”    。 选择“下一步”  。 键入项目名称（如 ConsoleApp FirstApp），然后单击“创建”   。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左窗格中，在“Visual C#”下，选择“控制台应用”，然后在中间窗格中选择“控制台应用(.NET Framework)”或“控制台应用(.NET Core)”      。 键入名称（如 ConsoleApp-FirstApp），然后单击“确定”   。
    ::: moniker-end

    如果没有看到“控制台应用(.NET Framework)”或“控制台应用(.NET Core)”项目模板，请转到“工具” > “获取工具和功能”，这会打开 Visual Studio 安装程序     。 选择“.NET Core 跨平台开发”或“.NET 桌面开发”工作负载，然后选择“修改”    。

    Visual Studio 创建控制台项目，该项目显示在右窗格的“解决方案资源管理器”中。

1. 在 Program.cs 中，使用以下代码替换所有默认代码  ：

    ```csharp
    using System;
    using System.Collections.Generic;

    namespace ConsoleApp_FirstApp
    {
        class Program
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Welcome to Galaxy News!");
                IterateThroughList();
                Console.ReadKey();
            }

            private static void IterateThroughList()
            {
                var theGalaxies = new List<Galaxy>
            {
                new Galaxy() { Name="Tadpole", MegaLightYears=400, GalaxyType=new GType('S')},
                new Galaxy() { Name="Pinwheel", MegaLightYears=25, GalaxyType=new GType('S')},
                new Galaxy() { Name="Cartwheel", MegaLightYears=500, GalaxyType=new GType('L')},
                new Galaxy() { Name="Small Magellanic Cloud", MegaLightYears=.2, GalaxyType=new GType('I')},
                new Galaxy() { Name="Andromeda", MegaLightYears=3, GalaxyType=new GType('S')},
                new Galaxy() { Name="Maffei 1", MegaLightYears=11, GalaxyType=new GType('E')}
            };

                foreach (Galaxy theGalaxy in theGalaxies)
                {
                    Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears + ",  " + theGalaxy.GalaxyType);
                }

                // Expected Output:
                //  Tadpole  400,  Spiral
                //  Pinwheel  25,  Spiral
                //  Cartwheel, 500,  Lenticular
                //  Small Magellanic Cloud .2,  Irregular
                //  Andromeda  3,  Spiral
                //  Maffei 1,  11,  Elliptical
            }
        }

        public class Galaxy
        {
            public string Name { get; set; }

            public double MegaLightYears { get; set; }
            public object GalaxyType { get; set; }

        }

        public class GType
        {
            public GType(char type)
            {
                switch(type)
                {
                    case 'S':
                        MyGType = Type.Spiral;
                        break;
                    case 'E':
                        MyGType = Type.Elliptical;
                        break;
                    case 'l':
                        MyGType = Type.Irregular;
                        break;
                    case 'L':
                        MyGType = Type.Lenticular;
                        break;
                    default:
                        break;
                }
            }
            public object MyGType { get; set; }
            private enum Type { Spiral, Elliptical, Irregular, Lenticular}
        }
    }
    ```

    我们使用此代码的目的是在列表中显示星系名称、与星系的距离以及星系类型。 若要进行调试，了解代码的含义非常重要。 以下是要在输出中显示的列表中某行的格式：

    星系名称、距离和星系类型    。

### <a name="run-the-app"></a>运行应用

1. 按 F5 或位于代码编辑器上方的调试工具栏中的“开始调试”按钮![开始调试](../debugger/media/dbg-tour-start-debugging.png "开始调试")   。

    应用启动，调试程序未显示异常。 但是，在控制台窗口中看到的输出非预期结果。 下面是预期的输出：

    ```
    Tadpole  400,  Spiral
    Pinwheel  25,  Spiral
    Cartwheel, 500,  Lenticular
    Small Magellanic Cloud .2,  Irregular
    Andromeda  3,  Spiral
    Maffei 1,  Elliptical
    ```

    但是，相反我们看到的是：

    ```
    Tadpole  400,  ConsoleApp_FirstApp.GType
    Pinwheel  25,  ConsoleApp_FirstApp.GType
    Cartwheel, 500,  ConsoleApp_FirstApp.GType
    Small Magellanic Cloud .2,  ConsoleApp_FirstApp.GType
    Andromeda  3,  ConsoleApp_FirstApp.GType
    Maffei 1, 11,  ConsoleApp_FirstApp.GType
    ```

    查看输出和代码，我们知道 `GType` 是存储星系类型的类的名称。 我们试图显示实际的星系类型（如“螺旋”），而不是类名！

### <a name="debug-the-app"></a>调试应用

1. 在应用仍在运行的情况下，通过单击此代码行中 `Console.WriteLine` 方法调用旁边的左边距来设置断点。

    ```csharp
    foreach (Galaxy theGalaxy in theGalaxies)
    {
        Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears + ",  " + theGalaxy.GalaxyType);
    }
    ```

    设置断点时，左边距会显示红点。

    由于在输出中发现问题，因此将通过查看前面在调试程序中设置输出的代码来开始进行调试。

1. 单击调试工具栏中的“重启”![重启应用](../debugger/media/dbg-tour-restart.png "重启应用")按钮 (Ctrl + Shift + F5)     。

    应用会在设置的断点处暂停。 黄色突出显示指示调试程序暂停的位置（黄色代码行尚未执行）。

1. 将鼠标悬停在右侧的 `GalaxyType` 变量上，然后在扳手图标的左侧展开 `theGalaxy.GalaxyType`。 可以看到 `GalaxyType` 包含属性 `MyGType`，并且属性值设置为 `Spiral`。

    ![检查变量](../debugger/media/beginners-inspect-variable.png)

    “螺旋”实际上是想要打印到控制台的正确值！ 因此，运行应用时，可以在此代码中访问此值，这是一个良好的开端。 在这种情况下，我们使用的 API 不正确。 在调试程序中运行代码时，我们将查看是否可解决此问题。

1. 在相同的代码中进行调试时，将光标放在 `theGalaxy.GalaxyType` 的末尾并将其更改为 `theGalaxy.GalaxyType.MyGType`。 虽然可进行此更改，但代码编辑器会显示一条错误，指示无法编译此代码。

    ![语法错误](../debugger/media/beginners-edit.png)

1. 单击“编辑并继续”消息框中的“编辑”   。 现在在“错误列表”窗口中出现一条错误消息  。 该错误表示 `'object'` 不包含 `MyGType` 的定义。

    ![语法错误](../debugger/media/beginners-no-definition.png)

    即使我们使用类型为 `GType` 的对象（具有 `MyGType` 属性）来设置每个星系，调试程序也不会将 `theGalaxy` 对象识别成类型为 `GType` 的对象。 这是怎么回事？ 想查看设置星系类型的任何代码。 执行此操作时，你会发现 `GType` 类肯定具有 `MyGType` 的属性，但某些内容不正确。 关于 `object` 的错误消息证明是线索；对于语言解释器，类型似乎是类型为 `object` 的对象，而不是类型为 `GType` 的对象。

1. 查看与设置星系类型相关的代码，则会发现 `Galaxy` 类的 `GalaxyType` 属性指定为 `object` 而不是 `GType`。

    ```csharp
    public object GalaxyType { get; set; }
    ```

1. 将前面的代码更改为：

    ```csharp
    public GType GalaxyType { get; set; }
    ```

1. 单击调试工具栏中的“重启”![重启应用](../debugger/media/dbg-tour-restart.png "重启应用")按钮 (Ctrl + Shift + F5) 以重新编译代码并重启     。

    现在，当调试程序在 `Console.WriteLine` 上暂停时，可以将鼠标悬停在 `theGalaxy.GalaxyType.MyGType` 上，并看到该值已正确设置。

1. 通过单击左边距中的断点圆（或右键单击并选择“断点” > “删除断点”）来删除断点，然后按 F5 以继续操作    。

    该应用运行并显示输出。 它现在看起来很不错，但请注意一点；预期的小麦哲伦星系在控制台输出中显示为不规则星系，但它根本没有显示星系类型。

    ```
    Tadpole  400,  Spiral
    Pinwheel  25,  Spiral
    Cartwheel, 500,  Lenticular
    Small Magellanic Cloud .2,
    Andromeda  3,  Spiral
    Maffei 1,  Elliptical
    ```

1. 在此代码行上设置断点。

    ```csharp
    public GType(char type)
    ```

    此代码是设置星系类型的位置，因此，我们想要更详细地介绍它。

1. 单击调试工具栏中的“重启”![重启应用](../debugger/media/dbg-tour-restart.png "重启应用")按钮 (Ctrl + Shift + F5) 进行重启     。

    调试程序在设置断点的代码行上暂停。

1. 将鼠标悬停在 `type` 变量上。 随即看到 `S` 的值（字符代码后面）。 你对 `I` 的值感兴趣，因为你知道这是不规则的星系类型。

1. 按 F5 并再次将鼠标悬停在 `type` 变量上  。 重复此步骤，直到在 `type` 变量中看到 `I` 的值。

    ![检查变量](../debugger/media/beginners-inspecting-data.png)

1. 现在，请按 F11（“调试” > “单步执行”或调试工具栏上的“单步执行”按钮）。    

    F11 一次调试一个语句（并执行代码）  。 F10（“单步跳过”）是类似的命令，在学习如何使用调试程序时两者都非常有用   。

1. 按 F11，直到 `switch` 语句中的代码行的值为“I”时停止  。 此处，你将看到拼写错误导致的明显问题。 预期代码转到其 `MyGType` 设置为不规则星系类型的位置，但调试程序会完全跳过此代码并在 `switch` 语句的 `default` 部分上暂停。

    ![查找拼写错误](../debugger/media/beginners-typo.png)

    查看代码，会在 `case 'l'` 语句中看到拼写错误。 它应为 `case 'I'`。

1. 单击 `case 'l'` 的代码并将其替换为 `case 'I'`。

1. 删除断点，然后单击“重启”按钮以重启该应用  。

    现在已修复 bug，你会看到期望的输出！

    按任意键以完成应用。

## <a name="summary"></a>总结

发现问题时，请使用调试程序和如 F10 和 F11 等[单步执行命令](../debugger/navigating-through-code-with-the-debugger.md)来查找出现问题的代码区域   。

> [!NOTE]
> 如果难以确定出现问题的代码区域，请在出现问题之前运行的代码中设置断点，然后使用单步执行命令，直到看到问题清单。 此外可以使用[跟踪点](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints)来将消息记录到“输出”窗口  。 通过查看记录的消息（并注意哪些消息尚未记录！），通常可以将代码区域与问题隔离开来。 可能需要多次重复此过程才能缩小范围。

找到出现问题的代码区域时，请使用调试程序进行调查。 若要查找问题的成因，请在调试程序中运行应用时检查问题代码：

* [检查变量](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)并检查其是否包含应包含的值类型。 如果发现错误值，请找出设置错误值的位置（要查找设置值的位置，可能需要重启调试程序和/或查看[调用堆栈](../debugger/how-to-use-the-call-stack-window.md)）。

* 检查应用程序是否正在执行预期的代码。 （例如，在示例应用程序中，我们预期 switch 语句的代码将星系类型设置为不规则，但是由于拼写错误，应用跳过了代码。）

> [!TIP]
> 使用调试程序来帮助查找 bug。 仅在知道代码含义的情况下，调试工具才能查找 bug  。 如果你（开发人员）表达了该含义，则工具只能知道代码的含义。 编写[单元测试](../test/improve-code-quality.md)就是这样做的。

## <a name="next-steps"></a>后续步骤

在本文中，你已了解一些常规的调试概念。 接下来可以开始了解有关调试器的更多信息。

> [!div class="nextstepaction"]
> [初探调试器](../debugger/debugger-feature-tour.md)
