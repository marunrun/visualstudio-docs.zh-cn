---
title: 教程：调试 C# 和 C++ 代码（混合模式）
description: 了解如何使用混合模式调试来调试 .NET Core 或 .NET Framework 应用中的本机 DLL
ms.custom: seodec18
ms.date: 11/02/2018
ms.topic: tutorial
dev_langs:
- CSharp
- C++
helpviewer_keywords:
- mixed mode debugging
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
- cplusplus
ms.openlocfilehash: 9f3fd94f8c294dce81bc69011e7d6f5fdd505325
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84182633"
---
# <a name="tutorial-debug-c-and-c-in-the-same-debugging-session"></a>教程：在同一个调试会话中调试 C# 和 C++

Visual Studio 允许你在调试会话中启用多个调试器类型，这名为混合模式调试。 在本教程中，将了解如何在单一调试会话中调试托管代码和本机代码。

本教程展示如何在托管应用内调试本机代码，但你也可以[在本机应用内调试托管代码](../debugger/how-to-debug-in-mixed-mode.md)。 调试器还支持其他混合模式调试类型，如调试 [Python 和本机代码](../python/debugging-mixed-mode-c-cpp-python-in-visual-studio.md)以及在应用类型（如 ASP.NET）中使用脚本调试器。

在本教程中，你将：

> [!div class="checklist"]
> * 创建简单的本机 DLL
> * 创建简单 .NET Core 或 .NET Framework 应用以调用 DLL
> * 配置混合模式调试
> * 启动调试器
> * 命中托管应用中的断点
> * 单步执行本机代码

## <a name="prerequisites"></a>先决条件

必须安装 Visual Studio 并具有下列工作负荷：
- 使用 C++ 的桌面开发
- .NET 桌面开发或 .NET Core 跨平台开发，具体取决于你想要创建哪种应用类型。

如果未安装 Visual Studio，请转到  [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/) 页面，进行免费安装。

如果已安装 Visual Studio，但没有所需工作负荷，请选择 Visual Studio“新建项目”对话框左窗格中的“打开 Visual Studio 安装程序” 。 在 Visual Studio 安装程序中，选择所需工作负荷，然后选择“修改”。

## <a name="create-a-simple-native-dll"></a>创建简单的本机 DLL

**创建 DLL 项目的文件：**

1. 打开 Visual Studio 并创建一个项目。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口。 键入 Ctrl+Q 以打开搜索框，键入“空项目”，选择“模板”，然后选择“空项目”(C++)   。 在出现的对话框中，选择“创建”。 然后，键入名称（如“Mixed_Mode_Debugging”）并单击“创建” 。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件” > “新建” > “项目”。 在“新建项目”对话框的左窗格中，在“Visual C++”下，选择“其他”，然后在中间窗格中选择“空项目”   。 然后，键入名称（如“Mixed_Mode_Debugging”）并单击“确定” 。
    ::: moniker-end

    如果没有看到“空项目”项目模板，请转到“工具” > “获取工具和功能...”，这会打开 Visual Studio 安装程序  。 Visual Studio 安装程序启动。 选择“使用 C++ 的桌面开发”工作负载，然后选择“修改”按钮 。

    Visual Studio 随即创建项目。

1. 在“解决方案资源管理器”中选择“源文件”，然后选择“项目” > “添加新建项”   。 或者，右键单击“源文件”，然后选择“添加” > “新项”  。

1. 在“新项”对话框中，选择“C++ 文件(.cpp)” 。 在“名称”字段中键入“Mixed_Mode.cpp”，然后选择“添加”  。

    Visual Studio 将新 C++ 文件添加到“解决方案资源管理器”。

1. 将下列代码复制到“Mixed_Mode.cpp”：

    ```cpp
    #include "Mixed_Mode.h"
    ```

1. 在“解决方案资源管理器”中选择“头文件”，然后选择“项目” > “添加新项”   。 或者，右键单击“头文件”，然后选择“添加” > “新项”  。

1. 在“新项”对话框中，选择“头文件(.h)” 。 在“名称”字段中键入“Mixed_Mode.h”，然后选择“添加”  。

   Visual Studio 将新的头文件添加到“解决方案资源管理器”。

1. 将下列代码复制到“Mixed_Mode.h”：

    ```cpp
    #ifndef MIXED_MODE_MULTIPLY_HPP
    #define MIXED_MODE_MULTIPLY_HPP

    extern "C"
    {
      __declspec(dllexport) int __stdcall mixed_mode_multiply(int a, int b) {
        return a * b;
      }
    }
    #endif
    ```

1. 选择“文件” > “保存全部”，或按 Ctrl+Shift+S 保存文件    。

**配置并生成 DLL 项目：**

1. 在 Visual Studio 工具栏中，选择“调试”配置以及“x86”或“x64”平台  。 如果调用的应用将是始终在 64 位模式下运行的 .NET Core，请选择“x64”作为平台。

1. 在“解决方案资源管理器”中，选择“Mixed_Mode_Debugging”项目节点并选择“属性”图标，或右键单击项目节点并选择“属性”   。

1. 在“属性”窗格的顶部，请确保将“配置”设置为“活动(调试)”以及将“平台”设为与你在工具栏中所设置的相同：“x64”或“Win32”（适用于 x86 平台）     。

   > [!IMPORTANT]
   > 如果将平台从“x86”切换到“x64”，或相反，则必须为新平台重新配置属性 。

1. 在左窗格的“配置属性”下方选择“链接器” > “高级”，并在“无入口点”旁边的下拉列表中选择“否”    。 如果必须将其更改为“否”，请选择“应用” 。

1. 在“配置属性”下方选择“常规”，并在“配置类型”旁边的下拉列表中选择“动态库(.dll)”   。 选择“应用”，然后选择“确定” 。

   ![切换到本机 DLL](../debugger/media/mixed-mode-set-as-native-dll.png)

1. 在“解决方案资源管理器”中选择项目，然后选择“生成” > “生成解决方案”，按 F7 或右键单击该项目并选择“生成”    。

   该项目应顺利生成，没有错误。

## <a name="create-a-simple-managed-app-to-call-the-dll"></a>创建简单的托管应用以调用 DLL

1. 打开 Visual Studio 并创建一个新项目。

    ::: moniker range=">=vs-2019"
    按 Esc 关闭启动窗口。 键入 Ctrl+Q 以打开搜索框，键入“控制台”，选择“模板”，然后选择“控制台应用 (.NET Core)”或“控制台应用 (.NET ramework)”(C#)    。 在出现的对话框中，选择“创建”。

    然后，键入名称（如“Mixed_Mode_Calling_App”）并单击“创建” 。
    ::: moniker-end
    ::: moniker range="vs-2017"
    从顶部菜单栏中选择“文件” > “新建” > “项目”。 在“新建项目”对话框的左窗格中，在“Visual C#”下，选择“Windows 桌面”，然后在中间窗格中选择“控制台应用(.NET Framework)”或“控制台应用(.NET Core)”    。

    然后，键入名称（如“Mixed_Mode_Calling_App”）并单击“确定” 。
    ::: moniker-end

    如果没有看到“控制台应用”项目模板，请转到“工具” > “获取工具和功能...”，这会打开 Visual Studio 安装程序  。 选择“.NET 桌面开发”工作负载，然后选择“修改” 。

    > [!NOTE]
    > 还可以将新的托管项目添加到现有 C++ 解决方案。 我们将在新的解决方案中创建项目，以提高混合模式调试任务的难度。

   Visual Studio 创建空项目并在“解决方案资源管理器”中显示该项目。

1. 使用下列代码替换“Program.cs”中的所有代码：

    ```csharp
    using System;
    using System.Runtime.InteropServices;

    namespace Mixed_Mode_Calling_App
    {
        public class Program
        {
            // Replace the file path shown here with the
            // file path on your computer. For .NET Core, the typical (default) path
            // for a 64-bit DLL might look like this:
            // C:\Users\username\source\repos\Mixed_Mode_Debugging\x64\Debug\Mixed_Mode_Debugging.dll
            // Here, we show a typical path for a DLL targeting the **x86** option.
            [DllImport(@"C:\Users\username\source\repos\Mixed_Mode_Debugging\Debug\Mixed_Mode_Debugging.dll", EntryPoint =
            "mixed_mode_multiply", CallingConvention = CallingConvention.StdCall)]
            public static extern int Multiply(int x, int y);
            public static void Main(string[] args)
            {
                int result = Multiply(7, 7);
                Console.WriteLine("The answer is {0}", result);
                Console.ReadKey();
            }
        }
    }
    ```

1. 在新代码中，使用刚创建的“Mixed_Mode_Debugging.dll”的文件路径替换 `[DllImport]` 中的文件路径。 有关提示，请参阅代码注释。 确保替换 username 占位符。

1. 选择“文件” > “保存 Program.cs”或按 Ctrl+S 以保存文件   。

## <a name="configure-mixed-mode-debugging"></a>配置混合模式调试

### <a name="to-configure-mixed-mode-debugging-for-a-net-framework-app"></a>为 .NET Framework 应用配置混合模式调试

1. 在“解决方案资源管理器”中，选择“Mixed_Mode_Calling_App”项目节点并选择“属性”图标，或右键单击项目节点并选择“属性”   。

1. 选择左窗格中的“调试”，再选中“启用本机代码调试”复选框，然后关闭属性页以保存更改 。

    ![启用混合模式调试](../debugger/media/mixed-mode-enable-native-code-debugging.png)

### <a name="to-configure-mixed-mode-debugging-for-a-net-core-app"></a>为 .NET Core 应用配置混合模式调试

从 Visual Studio 2017 开始，在 Visual Studio 的大多数版本中，必须使用 launchSettings.json 文件（而非项目属性）在 .NET Core 应用中为本机代码启用混合模式调试。 要跟踪本功能的 UI 更新，请查看 [GitHub 问题](https://github.com/dotnet/project-system/issues/1125)。

1. 在“解决方案资源管理器”中展开“属性”，然后打开 launchSettings.json 文件 。

   >[!NOTE]
   >默认情况下，launchSettings.json 位于 C:\Users\username\source\repos\Mixed_Mode_Calling_App\Properties 。 如果 launchSettings.json 不存在，请在“解决方案资源管理器”中选择“Mixed_Mode_Calling_App”项目，然后选择“属性”图标，或右键点击该项目并选择“属性”   。 在“调试”选项卡进行临时更改并生成项目。 将创建 launchSettings.json 文件。 还原“调试”选项卡中所作更改。

1. 在 launchsettings.json 文件中添加下列行：

    ```csharp
    "nativeDebugging": true
    ```

    完整文件将类似于下例：

    ```csharp
    {
      "profiles": {
        "Mixed_Mode_Calling_App": {
          "commandName": "Project",
          "nativeDebugging": true
        }
      }
    }
    ```

## <a name="set-a-breakpoint-and-start-debugging"></a>设置断点并开始调试

1. 在 C# 项目中，打开“Program.cs”。 在下列代码行中设置断点，方法是点击最左侧边缘并选择该行再按 F9，或右键单击该行并选择“断点” > “插入断点”  。

    ```csharp
    int result = Multiply(7, 7);
    ```

    一个红圈将出现在设置断点的左边缘中。

1. 按 F5 并选择 Visual Studio 工具栏内的绿色箭头，或选择“调试” > “开始调试”来开始调试  。

   调试器在所设断点处暂停。 黄色箭头指示调试器当前的暂停位置。

## <a name="step-in-and-out-of-native-code"></a>单步执行和单步跳出本机代码

1. 托管应用中的调试暂停时按 F11，或选择“调试” > “单步执行”  。

   “Mixed_Mode.h”本机头文件打开，在调试器暂停位置看到黄色箭头。

   ![单步执行本机代码](../debugger/media/mixed-mode-step-into-native-code.png)

1. 现在，可以设置并命中断点以及检查本机代码或托管代码中的变量。

   - 将鼠标悬停在源代码中的变量上，查看变量值。

   - 在“自动”和“局部变量”窗口查看变量和变量值 。

   - 在调试器中暂停时，还可以使用“监视”窗口和“调用堆栈”窗口 。

1. 再按 F11，将调试器推进一行。

1. 按 Shift+F11 或选择“调试” > “单步跳出”，在托管应用中继续执行并再次暂停   。

1. 按 F5 或选择绿色箭头继续调试应用。

祝贺你！ 你已完成混合模式调试的教程。

## <a name="next-step"></a>下一步

在本教程中，学习了如何通过启用混合模式调试在托管应用中调试本机代码。 有关其他调试器功能的概述，请参阅：

> [!div class="nextstepaction"]
> [初探调试器](../debugger/debugger-feature-tour.md)
