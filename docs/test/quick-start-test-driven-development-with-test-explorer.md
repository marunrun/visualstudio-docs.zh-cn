---
title: 测试驱动开发演练
ms.date: 07/24/2019
ms.topic: conceptual
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 17ee82630e75e0b0ea8b4a069249c2dccad9010e
ms.sourcegitcommit: 9fc8b144d4ed1c46aba87c0b7e1d24454e0eea9d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68493165"
---
# <a name="walkthrough-test-driven-development-using-test-explorer"></a>演练：通过测试资源管理器进行测试驱动开发

创建单元测试，以通过增量代码更改来帮助保持代码正常工作。 你可以使用几个框架来编写单元测试，包括第三方开发的一些框架。 某些测试框架专用于不同语言或平台中的测试。 “测试资源管理器”为其中任意框架中的单元测试提供了一个接口。 有关测试资源管理器的详细信息，请参阅[使用测试资源管理器运行单元测试](run-unit-tests-with-test-explorer.md)和[测试资源管理器常见问题解答](test-explorer-faq.md)  。

本演练演示如何使用 Microsoft 测试框架 (MSTest) 开发 C# 语言的受测试方法。 你可以将其轻松改写为其他语言，也可加以调整以使用其他测试框架，例如 NUnit。 有关详细信息，请参阅[安装第三方单元测试框架](install-third-party-unit-test-frameworks.md)。

## <a name="create-a-test-and-generate-code"></a>创建测试并生成代码

1. 选择 C#“类库(.NET Standard)”项目  。 此项目将包含我们要测试的代码。 将项目命名为 MyMath  。

2. 在同一解决方案中，添加一个新的“MSTest 测试项目(.NET Core)”项目  。 将该测试项目命名为 MathTests  。

   ![新建代码和测试项目](../test/media/test-driven-development-ide.png)

3. 编写一个简单的测试方法，用于验证针对特定输入获得的结果。 将下面的代码添加到 `UnitTest1` 类中:

   ```csharp
   [TestMethod]
   public void BasicRooterTest()
   {
     // Create an instance to test:
     Rooter rooter = new Rooter();
     // Define a test input and output value:
     double expectedResult = 2.0;
     double input = expectedResult * expectedResult;
     // Run the method under test:
     double actualResult = rooter.SquareRoot(input);
     // Verify the result:
     Assert.AreEqual(expectedResult, actualResult, delta: expectedResult / 100);
   }
   ```

4. 从测试代码生成类型。

   1. 将光标放在 `Rooter` 上，然后在灯泡菜单中，选择“生成类型 Rooter” > “生成新类型”   。

      ![生成新类型快速操作](media/test-driven-development-generate-new-type.png)

   2. 在“生成类型”对话框中，将“项目”设置为 MyMath，并选择类库项目，然后选择“确定”     。

      ![Visual Studio 2019 中的“生成类型”对话框](media/test-driven-development-generate-type-dialog.png)

5. 从测试代码生成方法。 将光标放在 `SquareRoot` 上，然后在灯泡菜单中，选择“生成方法 Rooter.SquareRoot”  。

6. 运行单元测试。

   1. 要打开“测试资源管理器”，请在“测试”菜单中，依次选择“Windows” > “测试资源管理器”     。

   2. 在“测试资源管理器”中，选择“全部运行”按钮运行测试   。

   解决方案生成，测试运行但失败。

7. 选择测试名称。

   “测试详细信息摘要”窗格中将显示测试的详细信息  。

   ![测试资源管理器中的测试详细信息摘要](media/test-driven-development-test-detail-summary.png)

8. 选择“堆栈跟踪”下的顶部链接，跳到测试失败的位置  。

此时，你已创建了测试和存根，在此基础上进行修改以使测试通过。

## <a name="verify-a-code-change"></a>验证代码更改

1. 在 Class1.cs 文件中，改进 `SquareRoot` 的代码  ：

    ```csharp
    public double SquareRoot(double input)
    {
        return input / 2;
    }
    ```

2. 在“测试资源管理器”  中，选择“全部运行”  。

   解决方案生成，测试运行并通过。

   ![显示通过的测试的测试资源管理器](../test/media/test-driven-development-passed-test.png)

## <a name="extend-the-range-of-inputs"></a>扩展输入的范围

要提高代码在所有情况下均正常运行的概率，请添加扩大输入值范围的测试。

> [!TIP]
> 避免修改已通过的现有测试。 相反，请添加新测试。 仅当用户需求变化时更改现有测试。 此策略有助于确保在扩展代码时不丢失现有功能。

1. 在测试类中，添加以下测试，其中涉及到一系列输入值：

    ```csharp
    [TestMethod]
    public void RooterValueRange()
    {
        // Create an instance to test.
        Rooter rooter = new Rooter();

        // Try a range of values.
        for (double expected = 1e-8; expected < 1e+8; expected *= 3.2)
        {
            RooterOneValue(rooter, expected);
        }
    }

    private void RooterOneValue(Rooter rooter, double expectedResult)
    {
        double input = expectedResult * expectedResult;
        double actualResult = rooter.SquareRoot(input);
        Assert.AreEqual(expectedResult, actualResult, delta: expectedResult / 1000);
    }
    ```

2. 在“测试资源管理器”  中，选择“全部运行”  。

   新测试失败（但第一个测试仍然通过）。 要查找失败位置，请选择失败的测试，然后在“测试详细信息摘要”窗格中查看详细信息  。

3. 检查所测试的方法，以查明可能出错的地方。 按如下所示更改 `SquareRoot` 代码：

    ```csharp
    public double SquareRoot(double input)
    {
      double result = input;
      double previousResult = -input;
      while (Math.Abs(previousResult - result) > result / 1000)
      {
        previousResult = result;
        result = result - (result * result - input) / (2 * result);
      }
      return result;
    }
    ```

4. 在“测试资源管理器”  中，选择“全部运行”  。

   现在两个测试均通过。

## <a name="add-tests-for-exceptional-cases"></a>为异常用例添加测试

1. 为负输入添加新测试：

    ```csharp
    [TestMethod]
    public void RooterTestNegativeInputx()
    {
        Rooter rooter = new Rooter();
        try
        {
            rooter.SquareRoot(-10);
        }
        catch (System.ArgumentOutOfRangeException)
        {
            return;
        }
        Assert.Fail();
    }
    ```

2. 在“测试资源管理器”  中，选择“全部运行”  。

   所测试的方法形成循环，必须手动取消。

3. 在“测试资源管理器”的工具栏上选择“取消”   。

   测试将停止执行。

4. 通过在方法的开头添加以下 `if` 语句来修复 `SquareRoot` 代码：

    ```csharp
    public double SquareRoot(double input)
    {
        if (input <= 0.0)
        {
            throw new ArgumentOutOfRangeException();
        }
        ...
    ```

5. 在“测试资源管理器”  中，选择“全部运行”  。

   所有测试均通过。

## <a name="refactor-the-code-under-test"></a>重构所测试的代码

重构代码，但不要更改测试。

> [!TIP]
> 重构是旨在提高代码性能或易理解性的更改  。 其目的不在于更改代码的行为，因此不更改测试。
>
> 我们建议你分开进行功能扩展和重构步骤。 保持测试不变，就能有信心在重构时不意外引入 bug。

1. 按如下所示更改在 `SquareRoot` 方法中计算 `result` 的行：

    ```csharp
    public double SquareRoot(double input)
    {
        if (input <= 0.0)
        {
            throw new ArgumentOutOfRangeException();
        }

        double result = input;
        double previousResult = -input;
        while (Math.Abs(previousResult - result) > result / 1000)
        {
            previousResult = result;
            result = (result + input / result) / 2;
            //was: result = result - (result * result - input) / (2*result);
        }
        return result;
    }
    ```

2. 选择“全部运行”，并验证所有测试是否仍然通过  。

   ![显示 3 个通过的测试的测试资源管理器](../test/media/test-driven-development-three-passed-tests.png)
