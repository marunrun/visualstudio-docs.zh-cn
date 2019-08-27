---
title: C++ 入门
description: ''
ms.custom: mvc
ms.date: 12/04/2017
ms.topic: tutorial
author: corob-msft
ms.author: corob
manager: markl
dev_langs:
- CPP
ms.workload:
- cplusplus
ms.openlocfilehash: 0caebc01e2a1db85a38f967b47226e998cfc69d6
ms.sourcegitcommit: 85d66dc9fea3fa49018263064876b15aeb6f9584
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68461691"
---
# <a name="get-started-with-c-in-visual-studio"></a>Visual Studio 中的 C++ 入门

完成本快速入门后，你会熟悉通过 Visual Studio 用 C++ 语言开发应用程序时可使用的许多工具和对话框。 了解在集成开发环境 (IDE) 中工作的更多知识后，即可创建“Hello, World”风格的控制台应用程序。

## <a name="prerequisites"></a>系统必备

即使不熟悉 C++，你也可完成此快速入门，但你应该要了解一些常规的编程和调试概念。 Visual Studio 文档不会教你如何用 C++ 语言编程。 ISO C++ 网站上的[入门](https://isocpp.org/get-started)页中提供了优质 C++ 学习资源指南。

::: moniker range="vs-2017"

要完成此快速入门，需安装 Visual Studio 2017 的副本，并安装“使用 C++ 的桌面开发”工作负载  。 有关安装的快速指南，请参阅[在 Visual Studio 中安装 C++ 支持](/cpp/build/vscpp-step-0-installation)。

::: moniker-end

::: moniker range=">=vs-2019"

要完成此快速入门，需安装 Visual Studio 2019 的副本，并安装“使用 C++ 的桌面开发”工作负载  。 有关安装的快速指南，请参阅[在 Visual Studio 中安装 C++ 支持](/cpp/build/vscpp-step-0-installation)。

::: moniker-end

## <a name="create-a-console-app"></a>创建控制台应用

如果 Visual Studio 尚未运行，请将其打开。

::: moniker range="vs-2017"

![应用了 Visual C&#43;&#43; 设置的 IDE](../ide/media/get-started-cpp-ide-layout.png)

在你打开 Visual Studio 后，可查看 IDE 的三个基本部分：工具窗口、菜单和工具栏，以及主窗口空间。 工具窗口位于应用窗口的左右两侧。 “快速启动”框、菜单栏和标准工具栏位于顶部  。 窗口的中部包含“起始页”  。 当你打开解决方案或项目时，将在这里显示编辑器和设计器。 开发应用时，大部分时间都花在此中心区域。

::: moniker-end

::: moniker range=">=vs-2019"

打开 Visual Studio 后，随即显示“启动”窗口。 选择“继续但无需代码”打开开发环境  。

将看到 IDE 的三个基本部分：工具窗口、菜单和工具栏，以及主窗口空间。 工具窗口位于应用窗口的左右两侧。 搜索框、菜单栏和标准工具栏位于顶部。 加载解决方案或项目时，编辑器和设计器显示在应用程序窗口中间。 开发应用程序时，大部分时间都将用在此中心区域。

::: moniker-end

Visual Studio 使用项目来组织应用的代码，使用解决方案来组织项目   。 项目包含用于生成应用的所有选项、配置和规则。 它还负责管理所有项目文件和任何外部文件间的关系。 若要创建应用，先创建一个新项目和解决方案。

### <a name="to-create-a-console-app-project"></a>创建控制台应用项目

1. 在菜单栏上，依次选择“文件”>“新建”>“项目”，打开“新建项目”对话框   。

   ![在菜单栏上选择“文件”>“新建”>“项目”](../ide/media/get-started-cpp-file-new-project-menu.png)

1. 如果尚未选中，则在“新建项目”对话框中，选择“已安装”>“Visual C++”   。 在中间窗格中，选择“Windows 控制台应用程序”模板  。 在“名称”编辑框中，输入“HelloApp”   。

   ![使用“新建项目”对话框来创建应用项目](../ide/media/get-started-cpp-new-project-dialog.png)

   对话框可能有不同的选择，具体取决于安装的 Visual Studio 工作负载和组件。 如果看不到 Visual C++ 项目模板，则需再次运行 Visual Studio 安装程序并安装“使用 C++ 的桌面开发”工作负载  。 可直接从“新建项目”对话框操作  。 若要启动安装程序，请选择对话框上的“打开 Visual Studio 安装程序”链接  。

1. 选择“确定”按钮，创建应用项目和解决方案  。

   随后将创建 HelloApp 项目和解决方案及 Windows 控制台应用的基本文件，并自动将其加载到“解决方案资源管理器”中  。 代码编辑器中会打开 HelloApp.cpp 文件  。 “解决方案资源管理器”中会显示这些项  ：

   ![解决方案资源管理器中解决方案的文件](../ide/media/get-started-cpp-solution-explorer.png)

## <a name="add-code-to-the-app"></a>向应用添加代码

接下来，添加代码以在控制台窗口中显示单词“Hello”。

### <a name="to-edit-code-in-the-editor"></a>在编辑器中编辑代码

1. 在 HelloApp.cpp 文件中，在行 `return 0;` 之前输入一个空行，然后输入此代码  ：

   ```cpp
   cout << "Hello\n";
   ```

   红色的波浪线显示在 `cout`下面。 如果将指针悬停在其上方，则会显示错误消息。

   ![cout 错误文本](../ide/media/get-started-cpp-intellisense-error.png)

   错误消息也将出现在“错误列表”  窗口中。 可在菜单栏中选择“视图”>“错误列表”来显示此窗口  。

   ![“错误列表”窗口中的错误](../ide/media/get-started-cpp-error-list.png)

   代码缺少 [std::cout](/cpp/standard-library/iostream) 声明，可在 \<iostream> 标头文件中找到该声明  。

1. 若要添加 iostream 标头，请在 `#include "stdafx.h"` 后输入此代码  ：

   ```cpp
   #include <iostream>
   using namespace std;
   ```

   你可能注意到了，输入代码时出现了一个框。 此框包含针对所输入字符的自动填充建议。 此框是 C++ IntelliSense 的一部分，它提供了编码提示，包括类或接口的成员和参数信息。 你还可以使用代码段，它们是预定义的代码块。 有关详细信息，请参阅[使用 IntelliSense](../ide/using-intellisense.md) 和[代码片段](../ide/code-snippets.md)。

   ![编辑器中修复的代码](../ide/media/get-started-cpp-cout-fix.png)

   修复该错误后， `cout` 下面的红色波浪线将消失。

1. 若要保存对文件所做的更改，请按 Ctrl+S  。

## <a name="build-the-app"></a>生成应用

生成代码十分简单。 在菜单栏上，依次选择“生成”>“生成解决方案”  。 Visual Studio 生成 HelloApp 解决方案，并在“输出”窗口中报告进度  。

   ![生成 HelloApp 解决方案](../ide/media/get-started-cpp-build-solution.gif)

## <a name="debug-and-test-the-app"></a>调试和测试应用

可调试 HelloApp，查看控制台窗口中是否显示单词“Hello”。

### <a name="to-debug-the-app"></a>若要调试应用程序

若要启用调试器，请选择菜单栏上的“调试”>“开始调试”  。

![“调试”菜单上的“启动调试”命令](../ide/media/get-started-cpp-start-debugging-menu.png)

调试器启动并运行代码。 在调试器停止运行时，控制台窗口（类似命令提示符的单独窗口）将显示几秒钟，但是将很快关闭。 若要查看文本，你需要设置一个断点以停止程序执行。

### <a name="to-add-a-breakpoint"></a>要添加一个断点

1. 在编辑器中，将光标置于行 `return 0;` 上。 在菜单栏上，选择“调试”>“切换断点”  。 还可单击左侧边距处来设置断点。

     ![“调试”菜单上的“切换断点”命令](../ide/media/get-started-cpp-toggle-breakpoint-menu.png)

     编辑器窗口最左侧边距中该代码行附近将显示一个红圈。

     ![窗口边距中指示的断点](../ide/media/get-started-cpp-breakpoint-set.png)

1. 若要启用调试，请按 F5  。

   调试器启动，控制台窗口出现并显示单词 **Hello**。

   ![控制台窗口中的文本“Hello”](../ide/media/get-started-cpp-helloapp-window.png)

1. 若要停止调试，请按 Shift+F5  。

有关控制台项目调试的详细信息，请参阅[控制台项目](../debugger/debugging-preparation-console-projects.md)。

## <a name="build-a-release-version-of-the-app"></a>生成应用程序的发布版本

确认一切就绪后，可以准备该应用程序的发布版本。 发布版本省去了调试信息，且使用编译器优化选项来创建更小、更快的代码。

### <a name="to-clean-the-solution-files-and-build-a-release-version"></a>要清理解决方案文件并生成发布版本

1. 在菜单栏上，依次选择“生成”>“清理解决方案”，删除上一生成过程中创建的中间文件和输出文件  。

   ![“生成”菜单上的“清理解决方案”命令](../ide/media/get-started-cpp-clean-solution-menu.png)

1. 若要将 HelloApp 的解决方案配置从“调试”更改为“发布”，请在工具栏中选择“解决方案配置”控件上的下拉菜单，然后选择“发布”    。

   ![生成应用程序的发布版本](../ide/media/get-started-cpp-set-release-configuration.png)

1. 生成解决方案。 在菜单栏上，依次选择“生成”>“生成解决方案”  。

此生成完成后，应用创建完成，可在任何命令提示符窗口中复制和运行该应用。 这个应用的作用可能不大，但这是一个好的开始。

祝贺你完成此快速入门！

## <a name="see-also"></a>请参阅

- [使用 Visual Studio IDE 进行 C++ 桌面开发](/cpp/ide/using-the-visual-studio-ide-for-cpp-desktop-development)
- [演练：使用 C# 或 Visual Basic 创建简单应用程序](../get-started/csharp/tutorial-wpf.md)
- [Visual Studio 中的工作效率功能](../ide/productivity-features.md)
