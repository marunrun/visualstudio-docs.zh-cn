---
title: 对 Visual C# 代码进行单元测试
ms.date: 09/27/2019
ms.topic: conceptual
ms.author: jillfra
author: jillre
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 309cf408167cc463db8cde9e39d5c0fe4dbe26d6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72659835"
---
# <a name="unit-test-c-code"></a>单元测试 C# 代码

本文介绍一种在 UWP 应用中创建面向 C# 类的单元测试的方法。

将对 Rooter  类进行测试，此类实现了一个函数，该函数可计算给定数平方根的估算值。

本文演示了测试驱动开发  。 在此方法中，首先编写验证要测试的系统的特定行为的测试，然后编写通过测试的代码。

## <a name="create-the-solution-and-the-unit-test-project"></a>创建解决方案和单元测试项目

1. 在“文件”菜单上，选择“新建” > “项目”    。

2. 搜索并选择“空白应用(通用 Windows)”项目模板  。

3. 将项目命名为“Maths”  。

4. 在“解决方案资源管理器”  中，右键单击解决方案，然后依次选择“添加”   > “新建项目”  。

5. 搜索并选择“单元测试应用(通用 Windows)”项目模板  。

6. 将该测试项目命名为“RooterTests”  。

## <a name="verify-that-the-tests-run-in-test-explorer"></a>验证测试是否在测试资源管理器中运行

1. 在 UnitTest.cs  文件的 TestMethod1  中插入一些测试代码：

   ```csharp
   [TestMethod]
   public void TestMethod1()
   {
       Assert.AreEqual(0, 0);
   }
   ```

   <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> 类提供了几个可以用来验证测试方法结果的静态方法。

::: moniker range="vs-2017"

2. 在“测试”  菜单中，选择“运行”  >“全部测试”  。

::: moniker-end

::: moniker range=">=vs-2019"

2. 在“测试”  菜单中，选择“运行所有测试”  。

::: moniker-end

   将生成并运行测试项目。 请耐心等待，因为这可能需要一些时间。 随即显示测试资源管理器窗口，并且测试在“通过的测试”下列出   。 窗口底部的“摘要”窗格将提供有关所选测试的其他详细信息  。

## <a name="add-the-rooter-class-to-the-maths-project"></a>向 Maths 项目添加 Rooter 类

1. 在“解决方案资源管理器”  中，右键单击“Maths”  项目，然后选择“添加”   > “类”  。

2. 将类文件命名为 Rooter.cs  。

3. 将以下代码添加到 Rooter  类 Rooter.cs  文件中：

   ```csharp
   public Rooter()
   {
   }

   // estimate the square root of a number
   public double SquareRoot(double x)
   {
       return 0.0;
   }
   ```

   Rooter  类声明一个构造函数和 SquareRoot  estimator 方法。 SquareRoot  方法只是一个最小实现，足以为测试设置测试基本结构。

4. 将 `public` 关键字添加到 Rooter  类声明，以便测试代码能够访问它。

   ```csharp
   public class Rooter
   ```

## <a name="add-a-project-reference"></a>添加项目引用

1. 添加从 RooterTests 项目到 Maths 应用的引用。

    1. 在“解决方案资源管理器”  中，右键单击“RooterTests”  项目，然后选择“添加”   > “引用”  。

    2. 在“添加引用 - RooterTests”  对话框中，展开“解决方案”  ，然后选择“项目”  。 选择“Maths”  项目。

        ![添加一个对 Maths 项目的引用](../test/media/ute_cs_windows_addreference.png)

2. 向 UnitTest1.cs  文件添加 `using` 语句：

    1. 打开 UnitTest.cs  。

    2. 在 `using Microsoft.VisualStudio.TestTools.UnitTesting;` 行下添加以下代码：

       ```csharp
       using Maths;
       ```

3. 添加使用 Rooter  函数的测试。 将以下代码添加到 UnitTest.cs  中：

   ```csharp
   [TestMethod]
   public void BasicTest()
   {
       Maths.Rooter rooter = new Rooter();
       double expected = 0.0;
       double actual = rooter.SquareRoot(expected * expected);
       double tolerance = .001;
       Assert.AreEqual(expected, actual, tolerance);
   }
   ```

   新测试将显示在测试资源管理器的“未运行的测试”节点中   。

4. 若要避免“负载包含两个或更多具有相同目标路径的文件”错误，请在“解决方案资源管理器”  中，展开“Maths”  项目下的“属性”  节点，然后删除 Default.rd.xml  文件。

::: moniker range="vs-2017"

6. 在“测试资源管理器”  中，选择“全部运行”  。

   解决方案生成，测试运行并通过。

   ![测试资源管理器中通过的基本测试](../test/media/ute_cpp_testexplorer_basictest.png)

::: moniker-end

::: moniker range=">=vs-2019"

6. 在“测试资源管理器”  中，选择“运行所有测试”  。

   解决方案生成，测试运行并通过。

   ![测试资源管理器中通过的基本测试](../test/media/vs-2019/test-explorer-uwp-app.png)

::: moniker-end

你已设置测试和应用项目，并已验证可运行测试（调用应用项目中的函数）。 现在可以开始编写实际测试和代码。

## <a name="iteratively-augment-the-tests-and-make-them-pass"></a>以迭代方式增加测试并使它们通过

1. 添加一个名为“RangeTest”  的新测试：

   ```csharp
   [TestMethod]
   public void RangeTest()
   {
       Rooter rooter = new Rooter();
       for (double v = 1e-6; v < 1e6; v = v * 3.2)
       {
           double expected = v;
           double actual = rooter.SquareRoot(v*v);
           double tolerance = expected/1000;
           Assert.AreEqual(expected, actual, tolerance);
       }
   }
   ```

   > [!TIP]
   > 建议你不更改已通过的测试。 改为添加新的测试。

2. 运行 RangeTest  测试并验证它是否失败。

   ![RangeTest 未通过](../test/media/ute_cpp_testexplorer_rangetest_fail.png)

   > [!TIP]
   > 编写测试后，请立即运行测试，验证它是否失败。 这有助于避免编写从不失败的测试这一易犯错误。

3. 增强受测代码，以便新测试通过。 将 Rooter.cs  中的 SquareRoot  函数更改为：

   ```csharp
   public double SquareRoot(double x)
   {
       double estimate = x;
       double diff = x;
       while (diff > estimate / 1000)
       {
           double previousEstimate = estimate;
           estimate = estimate - (estimate * estimate - x) / (2 * estimate);
           diff = Math.Abs(previousEstimate - estimate);
       }
       return estimate;
   }
   ```

::: moniker range="vs-2017"

4. 在“测试资源管理器”  中，选择“全部运行”  。

::: moniker-end

::: moniker range=">=vs-2019"

4. 在“测试资源管理器”  中，选择“运行所有测试”  。

::: moniker-end

   现在所有三个测试都将通过。

> [!TIP]
> 通过一次添加一个测试来开发代码。 确保每次迭代后所有的测试都会通过。

## <a name="refactor-the-code"></a>重构代码

在本部分中，将重构应用和测试代码，然后重新运行测试以确保它们仍然通过。

### <a name="simplify-the-square-root-estimation"></a>简化平方根估算

1. 通过更改一行代码，简化 SquareRoot  函数中的集中计算，如下所示：

    ```csharp
    // Old code
    //estimate = estimate - (estimate * estimate - x) / (2 * estimate);

    // New code
    estimate = (estimate + x/estimate) / 2.0;
    ```

2. 运行所有测试，以确保未引入回归。 测试应全部通过。

> [!TIP]
> 一组稳定的优良单元测试可保证你在更改代码时不会引入 Bug。

### <a name="eliminate-duplicated-code"></a>消除重复的代码

RangeTest  方法对传递到 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> 方法的“公差”  变量的分母进行硬编码。 如果计划添加其他使用同一公差计算的测试，则在多个位置使用硬编码的值会导致代码难以维护。

1. 向 UnitTest1  类添加一个私有 helper 方法以计算公差值，然后从 RangeTest  调用该方法。

    ```csharp
    private double ToleranceHelper(double expected)
    {
        return expected / 1000;
    }

    ...

    [TestMethod]
    public void RangeTest()
    {
        ...
        // Old code
        // double tolerance = expected/1000;

        // New code
        double tolerance = ToleranceHelper(expected);
    }
    ...
    ```

2. 运行 RangeTest  ，以确保它仍然通过。

> [!TIP]
> 如果将一个 helper 方法添加到不想在“测试资源管理器”  中出现的测试类中，那么不要向该方法添加 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestMethodAttribute> 属性。

## <a name="see-also"></a>请参阅

- [演练：通过测试资源管理器进行测试驱动开发](quick-start-test-driven-development-with-test-explorer.md)
