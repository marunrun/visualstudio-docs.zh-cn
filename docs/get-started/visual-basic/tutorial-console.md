---
title: 教程：Visual Basic 入门
description: 了解如何在 Visual Studio 中逐步创建 Visual Basic 控制台应用。
ms.custom: seodec18, get-started
ms.date: 09/11/2019
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: vb
author: ornellaalt
ms.author: ornella
manager: jillfra
dev_langs:
- vb
ms.workload:
- multiple
ms.openlocfilehash: 279bfb00a2466120d21c5c868c0987ec19202acc
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "77579931"
---
# <a name="tutorial-get-started-with-visual-basic-in-visual-studio"></a>教程：Visual Studio 中的 Visual Basic 入门

在本 Visual Basic (VB) 教程中，你将使用 Visual Studio 创建和运行几个不同的控制台应用，并在执行这些操作时了解 [Visual Studio 集成开发环境 (IDE)](visual-studio-ide.md) 的部分功能。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="create-a-project"></a>创建项目

首先，创建一个 Visual Basic 应用程序项目。 项目类型随附了所需的全部模板文件，无需添加任何内容！

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

2. 从顶部菜单栏中选择“文件”>“新建”>“项目”    。

3. 在“新建项目”对话框左侧的窗格中，展开“Visual Basic”，然后选择“.NET Core”    。 在中间窗格中，选择“控制台应用(.NET Core)”  。 随后将项目命名为“WhatIsYourName”  。

   ![Visual Studio IDE 中“新建项目”对话框中的控制台应用 (.NET Core) 项目模板](media/new-project-vb-dotnetcore-whatisyourname-console-app.png)

### <a name="add-a-workload-optional"></a>添加工作负载（可选）

如果未显示“控制台应用(.NET Core)”  项目模板，可通过添加“.NET Core 跨平台开发”  工作负载获取它。 可通过以下两种方式添加此工作负载，具体取决于计算机上安装的 Visual Studio 2017 更新。

#### <a name="option-1-use-the-new-project-dialog-box"></a>选项 1：使用“新建项目”对话框

1. 单击“新建项目”  对话框左窗格中的“打开 Visual Studio 安装程序”  链接。

   ![单击“新建项目”对话框中的“打开 Visual Studio 安装程序”链接](../media/vs-open-visual-studio-installer-generic.png)

1. Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改”   。

   ![Visual Studio 安装程序中的 .NET Core 跨平台开发工作负荷](../media/tutorial-aspnet-workload.png)

#### <a name="option-2-use-the-tools-menu-bar"></a>选项 2：使用“工具”菜单栏

1. 取消“新建项目”对话框，再从顶部菜单栏中选择“工具”>“获取工具和功能”    。

1. Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改”   。

::: moniker-end

::: moniker range="vs-2019"

> [!NOTE]
> 本教程中的部分屏幕截图使用深色主题。 如果没有深色主题但想要使用，请参阅[个性化设置 Visual Studio IDE 和编辑器](../../ide/quickstart-personalize-the-ide.md)页面，了解具体方法。

1. 打开 Visual Studio 2019。

1. 在“开始”窗口上，选择“创建新项目”  。

   ![查看“创建新项目”窗口](../../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. 在“创建新项目”窗口的搜索框中输入或键入“控制台”   。 接下来，从“语言”列表中选择 Visual Basic，然后从“平台”列表中选择“Windows”   。 

   应用语言和平台筛选器之后，选择“控制台应用(.NET Core)”模板，然后选择“下一步”   。

   ![为“控制台应用(.NET Framework)”选择 Visual Basic 模板](./media/vs-2019/vb-create-new-project-search-console-net-core-filtered.png)

   > [!NOTE]
   > 如果未看到“控制台应用(.NET Core)”模板，则可以通过“创建新项目”窗口安装该模板   。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接   。
   >
   > ![“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接](../../get-started/media/vs-2019/not-finding-what-looking-for.png) 
   > 
   > 然后，在 Visual Studio 安装程序中，选择“.NET Core 跨平台开发”工作负载  。
   >
   > ![Visual Studio 安装程序中的 .NET Core 跨平台开发工作负荷](../../get-started/media/dot-net-core-xplat-dev-workload.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮  。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”，以安装工作负载  。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“WhatIsYourName”    。 然后，选择“创建”  。

   ![在“配置新项目”窗口中，将项目命名为“WhatIsYourName”](./media/vs-2019/vb-name-your-project-whatname.png)

   此时，Visual Studio 将打开新项目。

::: moniker-end

## <a name="create-a-what-is-your-name-application"></a>创建一个“What Is Your Name”应用程序

创建一个应用，它会提示你输入名字，然后将名字随日期和时间一起显示。 操作方法如下：

 ::: moniker range="vs-2017"

1. 打开 WhatIsYourName  项目（如果尚未打开）。

1. 立即在 `Sub Main(args As String())` 行后的左括号和 `End Sub` 行之间，输入以下 Visual Basic 代码：

     ```vb
     Console.WriteLine(vbCrLf + "What is your name? ")
     Dim name = Console.ReadLine()
     Dim currentDate = DateTime.Now
     Console.WriteLine($"{vbCrLf}Hello, {name}, on {currentDate:d} at {currentDate:t}")
     Console.Write(vbCrLf + "Press any key to exit... ")
     Console.ReadKey(True)
    ```

    此代码替换现有的 <xref:System.Console.WriteLine%2A>、<xref:System.Console.Write%2A> 和 <xref:System.Console.ReadKey%2A> 语句。

   ![显示“What Is Your Name”代码的代码窗口](./media/vs-2019/vb-codewindow-what-name-dark.png)

1. 使用绿色“开始”  按钮，或按“F5”  生成并运行第一个应用。

1. 控制台窗口打开时，输入名字。 控制台窗口应如以下屏幕快照所示：

   ![显示“What Is Your Name”、时间和日期以及“按任意键继续”消息的控制台窗口](media/vb-console-what-name.png)

1. 按任意键关闭控制台窗口。

::: moniker-end

::: moniker range="vs-2019"

1. 在 WhatIsYourName 项目中，立即在 `Sub Main(args As String())` 行后的左括号和 `End Sub` 行之间，输入以下 Visual Basic 代码  ：

     ```vb
     Console.WriteLine(vbCrLf + "What is your name? ")
     Dim name = Console.ReadLine()
     Dim currentDate = DateTime.Now
     Console.WriteLine($"{vbCrLf}Hello, {name}, on {currentDate:d} at {currentDate:t}!")
     Console.Write(vbCrLf + "Press any key to exit... ")
     Console.ReadKey(True)
    ```

    此代码替换现有的 <xref:System.Console.WriteLine%2A>、<xref:System.Console.Write%2A> 和 <xref:System.Console.ReadKey%2A> 语句。

   ![显示“What Is Your Name”代码的代码窗口](./media/vs-2019/vb-codewindow-what-name-dark.png)

1. 使用绿色“开始”  按钮，或按“F5”  生成并运行第一个应用。

1. 控制台窗口打开时，输入名字。 控制台窗口应如以下屏幕快照所示：

   ![显示“What Is Your Name”、时间和日期以及“按任意键继续”消息的控制台窗口](media/vb-console-what-name.png)

1. 按任意键关闭控制台窗口。

 ::: moniker-end

## <a name="create-a-calculate-this-application"></a>创建“Calculate This”应用程序

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017，然后从顶部菜单栏中，选择“文件”>“新建”>“项目”    。

1. 在“新建项目”对话框左侧的窗格中，展开“Visual Basic”，然后选择“.NET Core”    。 在中间窗格中，选择“控制台应用(.NET Core)”  。 然后将文件命名为 CalculateThis  。

1. 在 `Module Program` 行和 `End Module` 行之间输入以下代码：

   ```vb
   Public num1 As Integer
   Public num2 As Integer
   Public answer As Integer
   Sub Main()
       Console.WriteLine("Type a number and press Enter")
       num1 = Console.ReadLine()
       Console.WriteLine("Type another number to add to it and press Enter")
       num2 = Console.ReadLine()
       answer = num1 + num2
       Console.WriteLine("The answer is " & answer)
       Console.ReadLine()
   End Sub
   ```

   代码窗口应如以下屏幕截图所示：

   ![显示“CalculateThis”代码的代码窗口](media/vb-codewindow-calculate-this.png)

1. 单击“CalculateThis”  运行程序。 控制台窗口应如以下屏幕快照所示：

    ![显示“CalculateThis”应用的控制台窗口，其中提示了要执行的操作。](media/vb-console-calculate-this.png)

::: moniker-end 

::: moniker range="vs-2019"

1. 在“开始”窗口上，选择“创建新项目”  。 

1. 在“创建新项目”窗口的搜索框中输入或键入“控制台”   。 接下来，从“语言”列表中选择 Visual Basic，然后从“平台”列表中选择“Windows”   。 

1. 应用语言和平台筛选器之后，选择“控制台应用(.NET Core)”模板，然后选择“下一步”   。

   然后，在“配置新项目”窗口中，在“项目名称”框中键入或输入“CalculateThis”    。 接下来，选择“创建”  。

1. 在 `Module Program` 行和 `End Module` 行之间输入以下代码：

   ```vb
   Public num1 As Integer
   Public num2 As Integer
   Public answer As Integer
   Sub Main()
       Console.WriteLine("Type a number and press Enter")
       num1 = Console.ReadLine()
       Console.WriteLine("Type another number to add to it and press Enter")
       num2 = Console.ReadLine()
       answer = num1 + num2
       Console.WriteLine("The answer is " & answer)
       Console.ReadLine()
   End Sub
   ```

   代码窗口应如以下屏幕截图所示：

   ![显示“CalculateThis”代码的代码窗口](media/vb-codewindow-calculate-this.png)

1. 单击“CalculateThis”  运行程序。 控制台窗口应如以下屏幕快照所示：

    ![显示“CalculateThis”应用的控制台窗口，其中提示了要执行的操作。](media/vb-console-calculate-this.png)

::: moniker-end

## <a name="quick-answers-faq"></a>快速解答常见问题

下面是一个快速 FAQ，突出介绍了一些关键概念。

### <a name="what-is-visual-basic"></a>什么是 Visual Basic？

Visual Basic 是一种易于学习的类型安全编程语言。 它派生自 BASIC，BASIC 的意指“初学者通用符号指令代码”。

### <a name="what-is-visual-studio"></a>什么是 Visual Studio？

Visual Studio 是适用于开发人员的生产力工具集成开发套件。 可将其视为可用于创建程序和应用程序的程序。

### <a name="what-is-a-console-app"></a>什么是控制台应用？

控制台应用获取输入，在命令行窗口（也称为 控制台）中显示输出。

### <a name="what-is-net-core"></a>.NET Core 是什么？

.NET Core 是 .NET Framework 的进一步演化。 .NET Framework 允许跨编程语言共享代码，而 .NET Core 增加了跨平台共享代码的功能。 此外，它还为开放源。 （.NET Framework 和 .NET Core 都包含预生成功能的库以及公共语言运行时 (CLR)，公共语言运行时充当用于运行代码的虚拟机。）

## <a name="next-steps"></a>后续步骤

恭喜你完成本教程！ 若要更深入地了解，请参阅以下教程。

> [!div class="nextstepaction"]
> [在 Visual Studio 中使用 Visual Basic 和 .NET Core SDK 生成库](/dotnet/core/tutorials/vb-library-with-visual-studio)

## <a name="see-also"></a>请参阅

* [Visual Basic 语言演练](/dotnet/visual-basic/walkthroughs)
* [Visual Basic 语言参考](/dotnet/visual-basic/language-reference/index)
* [Visual Basic 代码文件的 IntelliSense](../../ide/visual-basic-specific-intellisense.md)
