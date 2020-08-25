---
title: 教程：创建一个简单的 C# 控制台应用程序
description: 了解如何在 Visual Studio 中分步创建 C# 控制台应用程序。
ms.custom: seodec18, get-started
ms.date: 02/18/2020
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: ornellaalt
ms.author: ornella
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 691e6c3b994649a9f0fa2d0e92a990f317a16208
ms.sourcegitcommit: 8e5b0106061bb43247373df33d0850ae68457f5e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/18/2020
ms.locfileid: "88508173"
---
# <a name="tutorial-create-a-simple-c-console-app-in-visual-studio"></a>教程：在 Visual Studio 中创建一个简单的 C# 控制台应用程序

在本 C# 教程中，你将使用 Visual Studio 创建和运行控制台应用程序，并在此过程中了解 Visual Studio 集成开发环境 (IDE) 的部分功能。

::: moniker range="vs-2017"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)页免费安装。

::: moniker-end

::: moniker range="vs-2019"

如果尚未安装 Visual Studio，请转到 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads)页免费安装。

::: moniker-end

## <a name="create-a-project"></a>创建项目

创建 C# 应用程序项目。 项目类型随附了所需的全部模板文件，无需添加任何内容！

::: moniker range="vs-2017"

1. 打开 Visual Studio 2017。

2. 从顶部菜单栏中选择“文件” > “新建” > “项目”。
   （或者，按 Ctrl+Shift+N）  。

3. 在“新建项目”对话框的左侧窗格中，展开“C#”，然后选择“.NET Core”  。 在中间窗格中，选择“控制台应用(.NET Core)”。 然后，将文件命名为“计算器”。

   ![Visual Studio IDE 中“新建项目”对话框中的控制台应用 (.NET Core) 项目模板](./media/new-project-csharp-calculator-console-app.png)

### <a name="add-a-workload-optional"></a>添加工作负载（可选）

如果未显示“控制台应用(.NET Core)”项目模板，可通过添加“.NET Core 跨平台开发”工作负载获取它。 操作方法如下。

#### <a name="option-1-use-the-new-project-dialog-box"></a>选项 1：使用“新建项目”对话框

1. 选择“新建项目”对话框左侧窗格中的“打开 Visual Studio 安装程序”链接。

   ![选择“新建项目”对话框中的“打开 Visual Studio 安装程序”链接](./media/csharp-open-visual-studio-installer-generic-dark.png)

1. Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改” 。

   ![Visual Studio 安装程序中的 .NET Core 跨平台开发工作负荷](./media/dot-net-core-xplat-dev-workload.png)

#### <a name="option-2-use-the-tools-menu-bar"></a>选项 2：使用“工具”菜单栏

1. 取消“新建项目”对话框，再从顶部菜单栏中选择“工具”>“获取工具和功能”  。

1. Visual Studio 安装程序启动。 选择“.NET Core 跨平台开发”工作负载，然后选择“修改” 。

::: moniker-end

::: moniker range="vs-2019"

1. 打开 Visual Studio 2019。

1. 在“开始”窗口上，选择“创建新项目”。

   ![查看“创建新项目”窗口](../../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. 在“创建新项目”窗口的搜索框中输入或键入“控制台”。 接下来，从“语言”列表中选择 C#，然后从“平台”列表中选择 Windows 。 

   应用语言和平台筛选器之后，选择“控制台应用(.NET Core)”模板，然后选择“下一步” 。

   ![为“控制台应用(.NET Framework)”选择 C# 模板](./media/vs-2019/csharp-create-new-project-search-console-net-core-filtered.png)

   > [!NOTE]
   > 如果未看到“控制台应用(.NET Core)”模板，则可以通过“创建新项目”窗口安装该模板 。 在“找不到所需内容?”消息中，选择“安装更多工具和功能”链接 。
   >
   > ![“创建新项目”窗口内“找不到所需内容”消息中的“安装更多工具和功能”链接](../../get-started/media/vs-2019/not-finding-what-looking-for.png) 
   > 
   > 然后，在 Visual Studio 安装程序中，选择“.NET Core 跨平台开发”工作负载。
   >
   > ![Visual Studio 安装程序中的 .NET Core 跨平台开发工作负荷](./media/dot-net-core-xplat-dev-workload.png)
   >
   > 之后，在 Visual Studio 安装程序中选择“修改”按钮。 系统可能会提示你保存所有内容；如果出现提示，请按照指示进行操作。 接下来，选择“继续”，以安装工作负载。 然后，返回到“[创建项目](#create-a-project)”过程中的步骤 2。

1. 在“配置新项目”窗口中，在“项目名称”框中键入或输入“Calculator”。 然后，选择“创建”。

   ![在“配置新项目”窗口中，将项目命名为“Calculator”](./media/vs-2019/csharp-name-your-calculator-project.png)

   Visual Studio 随即打开新项目，其中包含默认的“Hello World”代码。
   
::: moniker-end

## <a name="create-the-app"></a>创建应用

首先，我们将探讨 C# 中的一些基础整数数学运算。 然后，我们将添加代码，创建基础计算器。 之后，调试应用，查找并修复错误。 最后，优化代码，使其更高效。

### <a name="explore-integer-math"></a>探索整数数学运算

现在开始在 C# 中进行一些基础整数数学运算。

1. 在代码编辑器中，删除默认“Hello World”代码。

    ![从新的计算器应用中删除默认 Hello World 代码](./media/csharp-console-calculator-deletehelloworld.png)

   具体而言，删除显示 `Console.WriteLine("Hello World!");` 的行。

1. 在其原位置，键入以下代码：

    ```csharp
            int a = 42;
            int b = 119;
            int c = a + b;
            Console.WriteLine(c);
            Console.ReadKey();
    ```

    请注意，执行此操作时，Visual Studio 中的 IntelliSense 功能会提供自动完成该项的选项。

    > [!NOTE]
    > 以下动画并非旨在复制前面的代码。 它仅用于显示自动完成功能的工作方式。

    ![显示 Visual Studio IDE 中 IntelliSense 自动完成功能的整数数学运算代码动画](./media/integer-math-intellisense.gif)

1. 选择“计算器”旁的绿色“开始”按钮以生成并运行程序，或按“F5”。

   ![选择工具栏中的“计算器”按钮以运行应用程序](./media/csharp-console-calculator-button.png)

   随即会打开控制台窗口，显示 42 + 119 的总和，即 161。

    ![显示整数数学运算的结果的控制台窗口](./media/csharp-console-integer-math.png)

1. （可选）可以更改运算符来更改结果。 例如，可以将 `int c = a + b;` 代码行中的 `+` 运算符更改为 `-` 进行减法运算，更改为 `*` 进行乘法运算，或更改为 `/` 进行除法运算。 然后，运行该程序时，结果也会改变。

1. 关闭控制台窗口。

### <a name="add-code-to-create-a-calculator"></a>添加代码以创建计算器

现在向项目添加一组更复杂的计算器代码以继续。

1. 删除在代码编辑器中看到的所有代码。

1. 在代码编辑器中，输入或粘贴以下新的代码：

    ```csharp
    using System;

    namespace Calculator
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Declare variables and then initialize to zero.
                int num1 = 0; int num2 = 0;

                // Display title as the C# console calculator app.
                Console.WriteLine("Console Calculator in C#\r");
                Console.WriteLine("------------------------\n");

                // Ask the user to type the first number.
                Console.WriteLine("Type a number, and then press Enter");
                num1 = Convert.ToInt32(Console.ReadLine());

                // Ask the user to type the second number.
                Console.WriteLine("Type another number, and then press Enter");
                num2 = Convert.ToInt32(Console.ReadLine());

                // Ask the user to choose an option.
                Console.WriteLine("Choose an option from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                // Use a switch statement to do the math.
                switch (Console.ReadLine())
                {
                    case "a":
                        Console.WriteLine($"Your result: {num1} + {num2} = " + (num1 + num2));
                        break;
                    case "s":
                        Console.WriteLine($"Your result: {num1} - {num2} = " + (num1 - num2));
                        break;
                    case "m":
                        Console.WriteLine($"Your result: {num1} * {num2} = " + (num1 * num2));
                        break;
                    case "d":
                        Console.WriteLine($"Your result: {num1} / {num2} = " + (num1 / num2));
                        break;
                }
                // Wait for the user to respond before closing.
                Console.Write("Press any key to close the Calculator console app...");
                Console.ReadKey();
            }
        }
    }
    ```

1. 选择“计算器”或按“F5”，以运行程序。

   ![选择工具栏中的“计算器”按钮以运行应用程序](./media/csharp-console-calculator-button.png)

   控制台窗口即会打开。

1. 在控制台窗口中，查看应用，然后按照提示添加数字 42 和 119 。

   应用应如以下屏幕快照所示：

    ![显示“计算器”应用的控制台窗口，其中包括要执行的操作的相应提示](./media/csharp-console-calculator.png)

### <a name="add-functionality-to-the-calculator"></a>向计算器添加功能

调整代码，添加更多功能。

### <a name="add-decimals"></a>添加小数

计算器应用当前接受并返回整数。 但如果添加接受十进制的代码，会更精确。

如下面截图所示，如果运行应用，用数字 42 除以数字 119，结果为 0（零），这并不准确。

![“控制台”窗口显示“计算器”应用，该应用不返回带小数的数字](./media/csharp-console-calculator-nodecimal.png)

现在来修正代码，使其能够处理小数。

1. 按“Ctrl + H”，打开“查找和替换”控件  。

1. 将 `int` 变量的每个实例更改为 `float`。

   请确保在“查找和替换”控件中切换“大小写匹配”(Alt+C) 和“全字匹配”(Alt+W)      。

    ![展示如何将 int 变量更改为 float 的“查找和替换”控件动画](./media/find-replace-control-animation.gif)

1. 再次运行计算器应用，用数字 42 除以数字 119 。

   注意，应用现在返回的是带小数的数字，而不是零。

    ![“控制台”窗口显示“计算器”应用，该应用现在返回一个带小数的数值](./media/csharp-console-calculator-decimal.png)

但是，应用现在只是能够生成带小数的结果。 让我们对代码做一些调整，以便应用可以计算小数。

1. 使用“查找和替换”控件 (Ctrl + H) 将 `float` 变量的每个实例都更改为 `double`，并将 `Convert.ToInt32` 方法的每个实例都更改为 `Convert.ToDouble`  。

1. 运行计算器应用，用数字 42.5 除数字 119.75 。

   注意，应用现在能够接受小数值，并返回具有更多小数位的数值。

    ![“控制台”窗口显示“计算器”应用，该应用现在接受小数，并返回具有更多小数位的数值](./media/csharp-console-calculator-usedecimals.png)

    （我们将在[修改代码](#revise-the-code)部分中固定小数位数。）

## <a name="debug-the-app"></a>调试应用

我们对基础计算器应用进行了改进，但它还不具备可应对异常（如用户输入错误）的故障保护机制。

例如，如果尝试用数字除以 0，或者在应用需要数字字符时输入 alpha 字符（反之亦然），则应用可能会停止工作、返回错误或返回意外的非数值结果。

现在来演练一些常见的用户输入错误，在调试程序中找到它们（若其出现），并在代码中修复它们。

> [!TIP]
> 有关调试器及其工作原理的详细信息，请参阅[初步了解 Visual Studio 调试器](../../debugger/debugger-feature-tour.md)页面。

### <a name="fix-the-divide-by-zero-error"></a>修复“被零除”错误

尝试用数字除以零时，控制台应用可能会冻结，并在代码编辑器中显示错误的内容。

   ![Visual Studio 代码编辑器显示“被零除”错误](./media/csharp-console-calculator-dividebyzero-error.png)

> [!NOTE]
> 有时，应用不会冻结且调试程序不会显示被零除错误。 相反，应用可能会返回意外的非数字结果，如无穷符号。 以下代码修复仍然适用。

现在更改代码以解决此错误。

1. 删除直接出现在 `case "d":` 和注释（内容为 `// Wait for the user to respond before closing`）之间的代码。

1. 将其替换为以下代码：

   ```csharp
            // Ask the user to enter a non-zero divisor until they do so.
                while (num2 == 0)
                {
                    Console.WriteLine("Enter a non-zero divisor: ");
                    num2 = Convert.ToInt32(Console.ReadLine());
                }
                Console.WriteLine($"Your result: {num1} / {num2} = " + (num1 / num2));
                break;
        }
    ```

   添加代码后，带有 `switch` 语句的部分应如以下屏幕截图所示：

   ![Visual Studio 代码编辑器中修改后的“switch”部分](./media/csharp-console-calculator-switch-code.png)

现在，当用任何数字除以 0 时，应用会请求除以另一个数字。 更好的是：应用不会停止请求，直到提供非零数字。

   ![Visual Studio 代码编辑器显示“被零除”错误](./media/csharp-console-calculator-dividebyzero.png)

### <a name="fix-the-format-error"></a>修复“格式”错误

如果在应用需要数字字符时输入 Alpha 字符，控制台应用就会冻结，反之亦然。 然后 Visual Studio 会显示代码编辑器中的错误。

   ![Visual Studio 代码编辑器显示格式错误](./media/csharp-console-calculator-format-error.png)

若要修复这个错误，必须重构之前输入的代码。

#### <a name="revise-the-code"></a>修改代码

我们将应用分为两个类：`Calculator` 和 `Program`，而不是仅依赖于 `program` 类来处理所有代码。

`Calculator` 类处理大部分计算工作，`Program` 类处理用户界面和错误捕获工作。

让我们开始吧。

1. 删除 `Calculator` 命名空间左大括号和右大括号之间的所有内容：

    ```csharp
    using System;

    namespace Calculator
    {
        
    }
    ```

1. 接下来，添加新的 `Calculator` 类，如下所示：

    ```csharp
    class Calculator
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

    ```

1. 然后，添加新的 `Program` 类，如下所示：

    ```csharp
    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            while (!endApp)
            {
                // Declare variables and set to empty.
                string numInput1 = "";
                string numInput2 = "";
                double result = 0;

                // Ask the user to type the first number.
                Console.Write("Type a number, and then press Enter: ");
                numInput1 = Console.ReadLine();

                double cleanNum1 = 0;
                while (!double.TryParse(numInput1, out cleanNum1))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput1 = Console.ReadLine();
                }

                // Ask the user to type the second number.
                Console.Write("Type another number, and then press Enter: ");
                numInput2 = Console.ReadLine();

                double cleanNum2 = 0;
                while (!double.TryParse(numInput2, out cleanNum2))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput2 = Console.ReadLine();
                }

                // Ask the user to choose an operator.
                Console.WriteLine("Choose an operator from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                string op = Console.ReadLine();

                try
                {
                    result = Calculator.DoOperation(cleanNum1, cleanNum2, op);
                    if (double.IsNaN(result))
                    {
                        Console.WriteLine("This operation will result in a mathematical error.\n");
                    }
                    else Console.WriteLine("Your result: {0:0.##}\n", result);
                }
                catch (Exception e)
                {
                    Console.WriteLine("Oh no! An exception occurred trying to do the math.\n - Details: " + e.Message);
                }

                Console.WriteLine("------------------------\n");

                // Wait for the user to respond before closing.
                Console.Write("Press 'n' and Enter to close the app, or press any other key and Enter to continue: ");
                if (Console.ReadLine() == "n") endApp = true;

                Console.WriteLine("\n"); // Friendly linespacing.
            }
            return;
        }
    }
    ```

1. 选择“计算器”或按“F5”，以运行程序。

1. 按照提示，用数字 42 除以数字 119 。 应用应如以下屏幕快照所示：

    ![“控制台”窗口显示重构后的“计算器”应用，其中包括要执行的操作的相应提示和针对错误输入的错误处理措施](./media/csharp-console-calculator-refactored.png)

    注意，在选择关闭控制台应用之前，可以选择输入更多等式。 而且，我们还减少了结果中小数位的位数。

## <a name="close-the-app"></a>关闭应用程序

1. 如果还没有这样做，请关闭计算器应用。

1. 关闭 Visual Studio 中的输出窗格。

   ![关闭 Visual Studio 中的输出窗格](./media/csharp-calculator-close-output-pane.png)

1. 在 Visual Studio 中，按 Ctrl+S 保存应用 。

1. 关闭 Visual Studio。

## <a name="code-complete"></a>代码完成

在本次教程中，我们对计算器应用进行了许多更改。 应用现在可以更有效地处理计算资源，以及处理大多数的用户输入错误。

以下是完整代码，全部显示在同一个位置：

```csharp

using System;

namespace Calculator
{
    class Calculator
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

    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            while (!endApp)
            {
                // Declare variables and set to empty.
                string numInput1 = "";
                string numInput2 = "";
                double result = 0;

                // Ask the user to type the first number.
                Console.Write("Type a number, and then press Enter: ");
                numInput1 = Console.ReadLine();

                double cleanNum1 = 0;
                while (!double.TryParse(numInput1, out cleanNum1))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput1 = Console.ReadLine();
                }

                // Ask the user to type the second number.
                Console.Write("Type another number, and then press Enter: ");
                numInput2 = Console.ReadLine();

                double cleanNum2 = 0;
                while (!double.TryParse(numInput2, out cleanNum2))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput2 = Console.ReadLine();
                }

                // Ask the user to choose an operator.
                Console.WriteLine("Choose an operator from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                string op = Console.ReadLine();

                try
                {
                    result = Calculator.DoOperation(cleanNum1, cleanNum2, op);
                    if (double.IsNaN(result))
                    {
                        Console.WriteLine("This operation will result in a mathematical error.\n");
                    }
                    else Console.WriteLine("Your result: {0:0.##}\n", result);
                }
                catch (Exception e)
                {
                    Console.WriteLine("Oh no! An exception occurred trying to do the math.\n - Details: " + e.Message);
                }

                Console.WriteLine("------------------------\n");

                // Wait for the user to respond before closing.
                Console.Write("Press 'n' and Enter to close the app, or press any other key and Enter to continue: ");
                if (Console.ReadLine() == "n") endApp = true;

                Console.WriteLine("\n"); // Friendly linespacing.
            }
            return;
        }
    }
}

```

## <a name="next-steps"></a>后续步骤

继续学习本教程的第二部分：

> [!div class="nextstepaction"]
> [继续学习第 2 部分](tutorial-console-part-2.md)

## <a name="see-also"></a>请参阅

* [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
* [了解如何在 Visual Studio 中调试 C# 代码](tutorial-debugger.md)
