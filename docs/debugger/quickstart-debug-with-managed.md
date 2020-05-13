---
title: 调试托管代码 | Microsoft Docs
description: 使用 Visual Studio 调试器调试 C# 或 Visual Basic
ms.custom: mvc
ms.date: 03/18/2018
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: f4cea2e1-08dc-47ac-aba2-3b8c338e607f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: e5495bb1f531db00d43e04cce9f5f771c88cc1a7
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "65679203"
---
# <a name="quickstart-debug-with-c-or-visual-basic-using-the-visual-studio-debugger"></a>快速入门：使用 Visual Studio 调试器调试 C# 或 Visual Basic

Visual Studio 调试器提供了许多强大的功能以帮助调试应用。 本主题提供了一种快速了解部分基本功能的方法。

## <a name="create-a-new-project"></a>创建新项目

1. 打开 Visual Studio 并创建一个新项目。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口  。 键入 Ctrl+Q 以打开搜索框，键入“控制台”，选择“模板”，然后选择“创建新的控制台应用(.NET Core)项目”     。 在出现的对话框中，选择“创建”  。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件”   > “新建”   > “项目”  。 在“新建项目”对话框的左窗格中，在“Visual C#”下，选择“.NET Core”，然后在中间窗格中选择“控制台应用(.NET Core)”     。 然后，键入名称（如 MyDbgApp），然后单击  “确定”  。
    ::: moniker-end

     如果没有看到“控制台应用 (.NET Core)”项目模板，请转到   “工具” > “获取工具和功能...”  ，这会打开 Visual Studio 安装程序。 选择“.NET 桌面开发”和“.NET Core”工作负载，然后选择“修改”    。

    Visual Studio 随即创建项目。

1. 在“Program.cs”或“Module1.vb”中，替换以下代码  

    ```csharp
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
    ```

    ```vb
    Module Module1
        Sub Main()
        End Sub
    End Module
    ```

    替换为此代码：

    ```csharp
    class Program
    {
        private static void doWork()
        {
            LinkedList<int> c1 = new LinkedList<int>();

            c1.AddLast(10);
            c1.AddLast(20);

            LinkedList<int> c2 = new LinkedList<int>(c1);
            int i = c2.First.Value;
            int j = c2.First.Value;
            Console.Write("The first element is ");
            Console.Write(i);
            Console.Write("\n");
            Console.Write("The second element is ");
            Console.Write(j);
            Console.Write("\n");

        }

        static int Main()
        {
            // using namespace std;
            doWork();
            return 0;

        }
    }
    ```

    ```vb
    Imports System.Collections.Generic

    Namespace MyDbgApp
        Class Program
            Private Shared Sub doWork()
                Dim c1 As New LinkedList(Of Integer)()

                c1.AddLast(10)
                c1.AddLast(20)

                Dim c2 As New LinkedList(Of Integer)(c1)
                Dim i As Integer = c2.First.Value
                Dim j As Integer = c2.First.Value
                Console.Write("The first element is ")
                Console.Write(i)
                Console.Write(vbLf)
                Console.Write("The second element is ")
                Console.Write(j)
                Console.Write(vbLf)

            End Sub

            Public Shared Function Main() As Integer
                ' using namespace std;
                doWork()
                Return 0

            End Function
        End Class
    End Namespace
    ```

    > [!NOTE]
    > 在 Visual Basic 中，确保将启动对象设置为 `Sub Main`（“属性”>“应用程序”>“启动对象”  ）。

## <a name="set-a-breakpoint"></a>设置断点

断点是一个标记，指示 Visual Studio 应在哪个位置挂起运行的代码，以查看变量的值或内存的行为，或确定代码的分支是否运行  。 它是调试中最基本的功能。

1. 若要设置断点，请单击 `doWork` 函数调用左侧的滚动条槽（或选择代码行，然后按 F9）  。

    ![设置断点](../debugger/media/dbg-qs-set-breakpoint-csharp.png "设置断点")

2. 现在，按 F5（或选择“调试”>“开始调试”）   。

    ![命中断点](../debugger/media/dbg-qs-hit-breakpoint-csharp.png "命中断点")

    调试器会在设置断点的位置暂停。 调试器和应用程序在该处暂停的语句由黄色箭头指示。 具有 `doWork` 函数调用的行尚未执行。

    > [!TIP]
    > 如果循环或递归中存在断点，或者如果有许多频繁单步执行的断点，请使用[条件断点](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)以确保代码仅在满足特定条件时挂起。 条件断点可以节省时间，也可以更容易地调试难以重现的问题。

## <a name="navigate-code"></a>导航代码

有不同的命令来指示调试器继续。 我们将演示自 Visual Studio 2017 开始新增的一个有用的代码导航命令。

在断点处暂停时，将鼠标悬停在 `c1.AddLast(20)` 语句上，直至绿色的“运行到单击处”  按钮 ![运行到单击处](../debugger/media/dbg-tour-run-to-click.png "运行时单击") 出现，然后按“运行到单击处”按钮  。

![运行到单击处](../debugger/media/dbg-qs-run-to-click-csharp.png "运行到单击处")

应用将继续执行，调用 `doWork`，并于你在其中单击按钮的代码行上暂停。

用于单步执行代码的常见键盘命令包括 F10 和 F11   。 如需获取更多详尽介绍，请参阅[初探调试器](../debugger/debugger-feature-tour.md)。

## <a name="inspect-variables-in-a-datatip"></a>检查数据提示中的变量

1. 在当前代码行中（由黄色执行指针标记），将鼠标悬停在 `c1` 对象上以显示数据提示。

    ![查看数据提示](../debugger/media/dbg-qs-data-tip-csharp.png "查看数据提示")

    数据提示显示 `c1` 变量的当前值且允许检查其属性。 调试时，如果出现意外值，则表示在前一代码行或调用的代码行上出现 bug。

2. 展开数据提示以查看 `c1` 对象的当前属性值。

3. 如果要固定数据提示，以便在执行代码时可以继续查看 `c1` 的值，请单击小图钉图标。 （可将固定的数据提示移动到方便的位置。）

## <a name="edit-code-and-continue-debugging"></a>编辑代码并继续调试

如果在调试会话期间发现一个要在代码中测试的更改，则也可以执行此操作。

1. 单击 `c2.First.Value` 的第二个实例且将 `c2.First.Value` 更改为 `c2.Last.Value`。

2. 多次按 F10（或“调试”>“单步跳过”），向前移动调试器并执行已编辑的代码   。

    ![编辑并继续](../debugger/media/dbg-qs-edit-and-continue-csharp.gif "编辑并继续")

    F10  一次使调试器前进一个语句，但是是跳过函数而不是单步执行它们（跳过的代码仍然执行）。

有关使用编辑并继续以及功能限制的详细信息，请参阅[编辑并继续](../debugger/edit-and-continue.md)。

## <a name="next-steps"></a>后续步骤

在本教程中，你已了解了如何启动调试器、逐步执行代码以及检查变量。 你可能会希望更深入地了解调试器功能以及查看指向更多信息的链接。

> [!div class="nextstepaction"]
> [初探调试器](../debugger/debugger-feature-tour.md)
