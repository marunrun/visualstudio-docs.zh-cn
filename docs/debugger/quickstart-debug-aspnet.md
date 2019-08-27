---
title: 调试 ASP.NET
description: 使用 Visual Studio 调试器调试 ASP.NET
ms.custom: mvc
ms.date: 08/06/2018
ms.topic: quickstart
helpviewer_keywords:
- debugger
ms.assetid: f4cea2e1-08dc-47ac-aba2-3b8c338e607f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- aspnet
ms.openlocfilehash: 932c8331b7b706b783868a52e47afc5ead25ef9c
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65679249"
---
# <a name="quickstart-debug-aspnet-with-the-visual-studio-debugger"></a>快速入门：使用 Visual Studio 调试器调试 ASP.NET

Visual Studio 调试器提供了许多强大的功能以帮助调试应用。 本主题提供了一种快速了解部分基本功能的方法。

## <a name="create-a-new-project"></a>创建新项目

1. 打开 Visual Studio。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口。 键入 Ctrl+Q 以打开搜索框，键入“asp.net”，选择“模板”，然后选择“创建新的 ASP.NET Core Web 应用程序”。 在出现的对话框中，选择“创建”。
    ::: moniker-end
    ::: moniker range="vs-2017"
    在顶部菜单栏，依次选择“文件” > “新建” > “项目”。 在“新建项目”对话框的左窗格中，在“Visual C#”下，选择“Web”，然后在中间窗格中选择“ASP.NET Core Web 应用程序”。 键入名称（例如“MyDbgApp”），单击“确定”。

    在显示的对话框中，选择中间窗格中的“Web 应用程序”，然后单击“确定”。

    ![选择 Web 应用程序](../debugger/media/dbg-qs-aspnet-choose-web-app.png)
    ::: moniker-end

    如果没有看到“ASP.NET Core Web 应用程序”项目模板，请转到“工具” > “获取工具和功能...”，这会打开 Visual Studio 安装程序。 选择“ASP.NET 和 web 开发”工作负载，然后选择“修改”。

    Visual Studio 随即创建项目。

1. 在解决方案资源管理器中打开 About.cshtml.cs（在 Pages/About.cshtml 下）并替换以下代码

    ```csharp
    public void OnGet()
    {
        Message = "Your application description page.";
    }
    ```

    替换为此代码：

    ```csharp
    public void OnGet()
    {
        LinkedList<int> result = doWork();
        Message = "Result of work: " + result.First.Value + ", " + result.First.Value;
    }

    private static LinkedList<int> doWork()
    {
        LinkedList<int> c1 = new LinkedList<int>();

        c1.AddLast(10);
        c1.AddLast(20);

        LinkedList<int> c2 = new LinkedList<int>(c1);

        return c2;

    }
    ```

## <a name="set-a-breakpoint"></a>设置断点

断点是一个标记，指示 Visual Studio 应在哪个位置挂起运行的代码，以查看变量的值或内存的行为，或确定代码的分支是否运行。 它是调试中最基本的功能。

1. 若要设置断点，请单击 `doWork` 函数左侧的滚动条槽（或选择代码行，然后按 F9）。

    ![设置断点](../debugger/media/dbg-qs-set-breakpoint-aspnet.png)

    断点设置在左大括号的左侧 (`{`)。

1. 现在，按 F5（或选择“调试”>“开始调试”）。

1. 加载网页时，请单击网页顶部的“关于”链接。

    调试器会在设置断点的位置暂停。 调试器和应用程序在该处暂停的语句由黄色箭头指示。 尚未执行 `doWork` 函数声明之后的带有左大括号 (`{`) 的行。

    ![命中断点](../debugger/media/dbg-qs-hit-breakpoint-aspnet.png)

    > [!TIP]
    > 如果循环或递归中存在断点，或者如果有许多频繁单步执行的断点，请使用[条件断点](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression)以确保代码仅在满足特定条件时挂起。 条件断点可以节省时间，还可以更容易地调试难以重现的问题。

## <a name="navigate-code"></a>导航代码

有不同的命令来指示调试器继续。 我们将演示自 Visual Studio 2017 开始新增的一个有用的代码导航命令。

在断点处暂停时，将鼠标悬停在 `return c2` 语句上，直至绿色的“运行到单击处”按钮 ![运行到单击处](../debugger/media/dbg-tour-run-to-click.png) 出现，然后按“运行到单击处”按钮。

![运行到单击处](../debugger/media/dbg-qs-run-to-click-aspnet.png)

应用将继续执行，并于你在其中单击按钮的代码行上暂停。

用于单步执行代码的常见键盘命令包括 F10 和 F11。 如需获取更多详尽介绍，请参阅[初探调试器](../debugger/debugger-feature-tour.md)。

## <a name="inspect-variables-in-a-datatip"></a>检查数据提示中的变量

1. 在当前代码行中（由黄色执行指针标记），将鼠标悬停在 `c2` 对象上以显示数据提示。

    ![查看数据提示](../debugger/media/dbg-qs-data-tip-aspnet.png)

    数据提示显示 `c2` 变量的当前值且允许检查其属性。 调试时，如果出现意外值，则表示在前一代码行或调用的代码行上出现 bug。

2. 展开数据提示以查看 `c2` 对象的当前属性值。

3. 如果要固定数据提示，以便在执行代码时可以继续查看 `c2` 的值，请单击小图钉图标。 （可将固定的数据提示移动到方便的位置。）

## <a name="edit-code-and-continue-debugging"></a>编辑代码并继续调试

如果在调试会话期间发现一个要在代码中测试的更改，则也可以执行此操作。

1. 在 `OnGet` 方法中，单击 `result.First.Value` 的第二个实例且将 `result.First.Value` 更改为 `result.Last.Value`。

1. 多次按 F10（或“调试”>“单步跳过”），向前移动调试器并执行已编辑的代码。

    ![编辑并继续](../debugger/media/dbg-qs-edit-and-continue-aspnet.png "Edit and continue")

    F10 一次使调试器前进一个语句，但是是跳过函数而不是单步执行它们（跳过的代码仍然执行）。

有关使用编辑并继续以及功能限制的详细信息，请参阅[编辑并继续](../debugger/edit-and-continue.md)。

## <a name="next-steps"></a>后续步骤

在本教程中，你已了解了如何启动调试器、逐步执行代码以及检查变量。 你可能会希望更深入地了解调试器功能以及查看指向更多信息的链接。

> [!div class="nextstepaction"]
> [初探调试器](../debugger/debugger-feature-tour.md)
