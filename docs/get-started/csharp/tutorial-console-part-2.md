---
title: 教程：扩展简单的 C# 控制台应用
description: 了解如何在 Visual Studio 中逐步开发 C# 控制台应用。
ms.custom: get-started
ms.date: 07/09/2020
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: ghogen
ms.author: ghogen
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: aae83c43a106fd68b03a83124ad2ddcea4652c8d
ms.sourcegitcommit: c620d59578db1b89f80e64ae04b4898bc4ab292d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87375920"
---
# <a name="tutorial-extend-a-simple-c-console-app"></a>教程：扩展简单的 C# 控制台应用

在本教程中，你将了解如何使用 Visual Studio 来扩展在第一部分中创建的控制台应用。 你将了解 Visual Studio 中可帮助提高开发者工作效率的一些功能，例如使用高级编辑器功能以及调试。

如果你刚刚完成此系列的[第一部分](tutorial-console.md)，则已具备计算器控制台应用。  要跳过第 1 部分，可以首先从 GitHub 存储库打开项目。 C# 计算器应用位于 [vs-tutorial-samples 存储库](https://github.com/MicrosoftDocs/vs-tutorial-samples)中，因此你只需要按照[教程：打开存储库中的项目](../tutorial-open-project-from-repo.md)中的步骤开始操作即可。

## <a name="add-a-new-project"></a>添加新项目

实际代码涉及在一个解决方案中协同工作的多个项目。 现在，让我们将另一个项目添加到计算器应用。 这将是一个提供某些计算器函数的类库。

1. 在 Visual Studio 中，可以使用顶层菜单命令“文件” > “添加” > “新建项目”添加新项目，但也可以右键单击现有项目名称（称为“项目节点”），并打开项目的快捷菜单（或上下文菜单）  。 此快捷菜单包含向项目添加功能的多种方法。 因此，右键单击解决方案资源管理器中的项目节点，然后选择“添加” > “新建项目”  。

1. 选择 C# 项目模板“类库(.NET Standard)”。

   ![类库项目模板选择的屏幕截图](media/vs-2019/calculator2-add-project-dark.png)

1. 键入项目名称 CalculatorLibrary，然后选择“创建” 。 Visual Studio 将创建新项目并将其添加到解决方案中。

   ![添加了 CalculatorLibrary 类库项目的解决方案资源管理器的屏幕截图](media/vs-2019/calculator2-solution-explorer-with-class-library-dark2.png)

1. 重命名文件 CalculatorLibrary.cs，而不是使用 Class1.cs。 可以在解决方案资源管理器中单击该文件的名称对其进行重命名，也可右键单击并选择“重命名”，或按 F2  。

   系统可能会询问你是否要重命名对文件中 `Class1` 的任何引用。 你怎样回答并不重要，因为你将在后续步骤中替换该代码。

1. 现在，我们必须添加项目引用，以便第一个项目可以使用新类库公开的 API。  右键单击第一个项目中的“引用”节点，然后选择“添加项目引用” 。

   ![“添加项目引用”菜单项的屏幕截图](media/vs-2019/calculator2-add-project-reference-dark.png)

   此时将显示“引用管理器”对话框。 利用此对话框，可以添加对其他项目的引用以及项目所需的程序集和 COM DLL。

   ![“引用管理器”对话框的屏幕截图](media/vs-2019/calculator2-ref-manager-dark.png)

1. 在“引用管理器”对话框中，选中 CalculatorLibrary 项目对应的复选框，然后选择“确定”  。  项目引用显示在解决方案资源管理器中的“项目”节点下 。

   ![包含项目引用的解决方案资源管理器的屏幕截图](media/vs-2019/calculator2-solution-explorer-with-project-reference-dark2.png)

1. 在 Program.cs 中，选择 `Calculator` 类及其所有代码，然后按 CTRL+X 将其从 Program.cs 中剪切。 然后，在 CalculatorLibrary 的 CalculatorLibrary.cs 中，将代码粘贴到 `CalculatorLibrary` 命名空间中。 然后，使 Calculator 类 `public` 在库外部公开它。 CalculatorLibrary.cs 中的代码现在应类似于以下代码：

   ```csharp
   using System;

    namespace CalculatorLibrary
    {
        public class Calculator
        {
            public static double DoOperation(double num1, double num2, string op)
            {
                double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

                // Use a switch statement to do the math.
                switch (op)
                {
                    case "a":
                        result = num1 + num2;
                        break;
                    case "s":
                        result = num1 - num2;
                        break;
                    case "m":
                        result = num1 * num2;
                        break;
                    case "d":
                        // Ask the user to enter a non-zero divisor.
                        if (num2 != 0)
                        {
                            result = num1 / num2;
                        }
                        break;
                    // Return text for an incorrect option entry.
                    default:
                        break;
                }
                return result;
            }
        }
    }
   ```

1. 第一个项目包含引用，但你将看到一个错误，显示 Calculator.DoOperation 调用无法解析。 这是因为 CalculatorLibrary 位于不同命名空间中，因此添加了 `CalculatorLibrary` 命名空间以实现完全限定的引用。

   ```csharp
   result = CalculatorLibrary.Calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   改为尝试将 using 指令添加到文件的开头：

   ```csharp
   using CalculatorLibrary;
   ```

   此更改应允许你从调用站点中删除 CalculatorLibrary 命名空间，但现在存在模糊性。 `Calculator` 是否是 CalculatorLibrary 中的类，或 Calculator 是否是命名空间？  为了消除模糊性，请重命名命名空间 `CalculatorProgram`。

   ```csharp
   namespace CalculatorProgram
   ```

## <a name="reference-net-libraries-write-to-a-log"></a>引用 .NET 库：写入日志

1. 假设你现在要添加所有操作的日志，并将其写出到文本文件。 .NET `Trace` 类提供了此功能。 （这也适用于基本的打印调试技术。）Trace 类位于 System.Diagnostics 中，因此请首先添加 using 指令：

   ```csharp
   using System.Diagnostics;
   ```

1. 查看如何使用 Trace 类，你需要保留对文件流的引用，该引用与文件流关联。 这意味着计算器可以作为对象更好地工作，因此，让我们添加一个构造函数。

   ```csharp
   public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculator.log");
            Trace.Listeners.Add(new TextWriterTraceListener(logFile));
            Trace.AutoFlush = true;
            Trace.WriteLine("Starting Calculator Log");
            Trace.WriteLine(String.Format("Started {0}", System.DateTime.Now.ToString()));
        }

    public double DoOperation(double num1, double num2, string op)
        {
   ```

1. 我们需要将静态 `DoOperation` 方法更改为成员方法。  同时，我们还将输出添加到日志的每个计算，以便 DoOperation 如以下代码所示：

   ```csharp
   public double DoOperation(double num1, double num2, string op)
   {
        double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

        // Use a switch statement to do the math.
        switch (op)
        {
            case "a":
                result = num1 + num2;
                Trace.WriteLine(String.Format("{0} + {1} = {2}", num1, num2, result));
                break;
            case "s":
                result = num1 - num2;
                Trace.WriteLine(String.Format("{0} - {1} = {2}", num1, num2, result));
                break;
            case "m":
                result = num1 * num2;
                Trace.WriteLine(String.Format("{0} * {1} = {2}", num1, num2, result));
                break;
            case "d":
                // Ask the user to enter a non-zero divisor.
                if (num2 != 0)
                {
                    result = num1 / num2;
                    Trace.WriteLine(String.Format("{0} / {1} = {2}", num1, num2, result));
                }
                    break;
            // Return text for an incorrect option entry.
            default:
                break;
        }
        return result;
    }
   ```

1. 现在，返回 Program.cs，静态调用标有红色波浪线。 要修复此问题，请通过紧邻 while 循环前方添加以下行来创建一个 `calculator` 变量：

   ```csharp
   Calculator calculator = new Calculator();
   ```

   修改 `DoOperation` 的调用站点，如下所示：

   ```csharp
   result = calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

1. 再次运行程序，完成后，右键单击项目节点，选择“在文件资源管理器中打开文件夹”，然后在文件资源管理器中向下导航到输出文件夹。 它可以是 bin/Debug/netcoreapp3.1，打开 calculator.log 文件 。

    ```output
    Starting Calculator Log
    Started 7/9/2020 1:58:19 PM
    1 + 2 = 3
    3 * 3 = 9
    ```

## <a name="add-a-nuget-package-write-to-a-json-file"></a>添加 NuGet 包：写入 JSON 文件

1. 现在，假设我们想要以 JSON 格式（一种用于存储对象数据的常用可移植格式）输出操作。 要实现此功能，我们需要引用 NuGet 包 Newtonsoft.json。 NuGet 包是用于分发 .NET 类库的主要工具。 在解决方案资源管理器中，右键单击 CalculatorLibrary 项目的“引用”节点，然后选择“管理 NuGet 包”  。

   ![快捷菜单上“管理 NuGet 包”的屏幕截图](media/vs-2019/calculator2-manage-nuget-packages-dark2.png)

   “NuGet 包管理器”随即打开。

   ![NuGet 包管理器的屏幕截图](media/vs-2019/calculator2-nuget-package-manager-dark.png)

1. 搜索 Newtonsoft.Json 包，然后选择“安装”。

   ![Newtonsoft NuGet 包信息的屏幕截图](media/vs-2019/calculator2-nuget-newtonsoft-json-dark2.png)

   下载此包并将其添加到项目中后，解决方案资源管理器的“引用”节点中将显示一个新条目。

1. 在 CalculatorLibrary.cs 的开头为 Newtonsoft.Json 包添加 using 指令。

   ```csharp
   using Newtonsoft.Json;
   ```

1. 现在，使用以下代码替换计算器的构造函数，并创建 JsonWriter 成员对象：

   ```csharp
        JsonWriter writer;

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculatorlog.json");
            logFile.AutoFlush = true;
            writer = new JsonTextWriter(logFile);
            writer.Formatting = Formatting.Indented;
            writer.WriteStartObject();
            writer.WritePropertyName("Operations");
            writer.WriteStartArray();
        }
   ```

1. 修改 `DoOperation` 方法以添加 JSON 编写器代码：

   ```csharp
        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.
            writer.WriteStartObject();
            writer.WritePropertyName("Operand1");
            writer.WriteValue(num1);
            writer.WritePropertyName("Operand2");
            writer.WriteValue(num2);
            writer.WritePropertyName("Operation");
            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    writer.WriteValue("Add");
                    break;
                case "s":
                    result = num1 - num2;
                    writer.WriteValue("Subtract");
                    break;
                case "m":
                    result = num1 * num2;
                    writer.WriteValue("Multiply");
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        writer.WriteValue("Divide");
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            writer.WritePropertyName("Result");
            writer.WriteValue(result);
            writer.WriteEndObject();

            return result;
        }
   ```

1. 用户完成输入操作数据后，你需要添加一种方法来完成 JSON 语法。

   ```csharp
    public void Finish()
    {
        writer.WriteEndArray();
        writer.WriteEndObject();
        writer.Close();
    }
   ```

1. 在 Program.cs 中，在末尾添加对 Finish 的调用。

   ```csharp
            // And call to close the JSON writer before return
            calculator.Finish();
            return;
        }
   ```

1. 生成并运行应用，并在完成输入一些操作后，使用“n”命令正确关闭该应用。  现在，打开 consolelog.json 文件，你应看到如下所示的内容：

   ```json
   {
    "Operations": [
        {
        "Operand1": 2.0,
        "Operand2": 3.0,
        "Operation": "Add",
        "Result": 5.0
        },
        {
        "Operand1": 3.0,
        "Operand2": 4.0,
        "Operation": "Multiply",
        "Result": 12.0
        }
    ]
   }
   ```

## <a name="next-steps"></a>后续步骤

恭喜你完成本教程！ 若要了解详情，请继续学习后续教程。

> [!div class="nextstepaction"]
> [继续学习更多 C# 教程](/dotnet/csharp/tutorials/)

> [!div class="nextstepaction"]
> [继续学习 Visual Studio IDE 概述](/../visual-studio-ide.md)

## <a name="see-also"></a>请参阅

* [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
* [了解如何在 Visual Studio 中调试 C# 代码](tutorial-debugger.md)
