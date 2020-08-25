---
title: Visual Studio for Mac 测试工具
ms.date: 08/03/2020
ms.topic: conceptual
helpviewer_keywords:
- testing tools [Visual Studio for Mac]
- unit tests [Visual Studio for Mac]
ms.author: jomatthi
author: jmatthiesen
ms.openlocfilehash: acf34677e8d9b477512763be3c43bb9df0c53c46
ms.sourcegitcommit: 935e1388281df0f04147802606b5cb7f513d45ed
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "88201779"
---
# <a name="testing-tools-in-visual-studio-for-mac"></a>Visual Studio for Mac 中的测试工具

Visual Studio for Mac 测试工具可帮助你和你的团队达到并保持高标准的代码卓越性。 可以使用 Microsoft 单元测试框架 (MSTest)、xUnit 或 NUnit 编写和运行单元测试。

## <a name="creating-tests"></a>创建测试
要开始测试，可以通过右键单击解决方案并选择“添加”>“新建项目...”菜单，在解决方案中创建新的测试项目。 然后，选择对话框左侧的一个“测试”类别（例如“Web 和控制台”>“测试”类别）。 选择要创建的测试项目的类型，然后单击“下一步”。 按照显示的对话框中的说明进行操作，系统会将新的测试项目添加到解决方案中。

![已选中“Web 和控制台”>“测试”部分的“新建项目”对话框，其中显示了 xUnit、MSTest 和 NUnit 项目](media/create-new-test-project.PNG)

> [!NOTE]
> 有关如何对 .NET Core 应用程序进行单元测试并选择单元测试框架的详细信息，请参阅 [.NET Core 和 .NET Standard 中的单元测试](https://docs.microsoft.com/dotnet/core/testing/?pivots=xunit)文档。

## <a name="running-tests"></a>运行测试
“单元测试”窗口用于运行单元测试，并通过“视图”>“面板”>“单元测试”菜单打开 。 解决方案中的单元测试将自动发现并显示在此窗口中，你可以在其中运行所有测试或已选中的一组测试。

![“测试窗口”显示单元测试列表，以及用于运行或停止测试的工具栏。](media/test-window.PNG)

在编辑包含单元测试的 C# 类时，可以通过右键单击测试类或测试方法，然后选择“运行测试”或“调试测试”菜单来运行测试 。 选择“运行测试”菜单项将在“测试窗口”中运行测试，选择“调试测试”菜单将执行相同操作并附加调试程序，以便对代码进行故障排除 。

![包含“运行测试”和“调试测试”选项的编辑器右键单击菜单](media/run-tests-context-menu.PNG)

测试运行时，系统会显示一个“测试结果”窗口，以便你可以查看成功或失败的测试以及运行这些测试的输出。

![“测试结果”窗口显示 1 个失败的测试以及 21 个通过的测试和 1 个失败的测试的计数。](media/test-results-window.PNG)

## <a name="see-also"></a>另请参阅

- [.NET Core 和 .NET Standard 中的单元测试](/dotnet/core/testing)
- [单元测试入门（Windows 版 Visual Studio）](/visualstudio/test/getting-started-with-unit-testing)
- [单元测试基础知识（Windows 版 Visual Studio）](/visualstudio/test/unit-test-basics)
