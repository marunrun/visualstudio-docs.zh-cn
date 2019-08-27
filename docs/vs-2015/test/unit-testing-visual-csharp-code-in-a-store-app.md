---
title: 对应用商店应用中的 Visual C# 代码进行单元测试 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 23cb0d82-0451-464e-98ea-fa66e7010ead
caps.latest.revision: 21
author: alexhomer1
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 144097837eba5c8feeb5a424134fec887d51befe
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695253"
---
# <a name="unit-testing-visual-c-code-in-a-store-app"></a>对应用商店应用中的 Visual C# 代码进行单元测试
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍了一种在 Windows 应用商店应用中对 Visual C# 类创建单元测试的方法。 Rooter 类通过实现计算给定数的平方根的估计的函数来演示限制计算理论的模糊内存。 Maths 应用程序之后可使用此函数为用户演示可通过 math 完成的有趣操作。  
  
 本主题演示如何使用单元测试作为开发的第一步。 在此方法中，首先编写验证要测试的系统的特定行为的测试方法，然后编写通过测试的代码。 通过按照以下过程的顺序进行更改，您可调转此策略的顺序，即先编写要测试的代码，然后编写单元测试。  
  
 本主题还为单元测试和要测试的 DLL 创建一个 Visual Studio 解决方案和单独的项目。 您还可在 DLL 项目中直接包含单元测试，也可以为单元测试和 DLL 创建不同的解决方案。  
  
> [!NOTE]
> Visual Studio Community、Enterprise. 和 Professional 提供其他适用于单元测试的功能。  
> 
> - 使用已为 Microsoft 测试资源管理器创建附加设备适配器的任何第三方和开放源代码单元测试框架。 还可为测试分析并显示代码覆盖率信息。  
>   - 在每次生成后运行测试。  
>   - VS Enterprise 还包含 Microsoft Fakes（托管代码的隔离框架），通过替换系统和第三方功能的测试代码帮助你将测试集中于自己的代码之上。  
> 
>   有关详细信息，请参阅 MSDN 库中的[使用单元测试验证代码](https://msdn.microsoft.com/library/dd264975.aspx)。  
  
## <a name="BKMK_In_this_topic"></a> 在本主题中  
 [创建解决方案和单元测试项目](#BKMK_Create_the_solution_and_the_unit_test_project)  
  
 [验证测试是否可在资源管理器中运行](#BKMK_Verify_that_the_tests_run_in_Test_Explorer)  
  
 [向 Maths 项目添加 Rooter 类](#BKMK_Add_the_Rooter_class_to_the_Maths_project)  
  
 [将测试项目和应用项目相关联](#BKMK_Couple_the_test_project_to_the_app_project)  
  
 [以迭代方式增加测试并使它们通过](#BKMK_Iteratively_augment_the_tests_and_make_them_pass)  
  
 [调试失败测试](#BKMK_Debug_a_failing_test)  
  
 [重构代码](#BKMK_Refactor_the_code_)  
  
## <a name="BKMK_Create_the_solution_and_the_unit_test_project"></a> 创建解决方案和单元测试项目  
  
1. 在“文件”菜单上选择“新建”，然后选择“新建项目”。  
  
2. 在“新建项目”对话框中，依次展开“已安装”和“Visual C#”，然后选择“Windows 应用商店”。 然后，从项目模板列表中选择“空白应用”。  
  
3. 将项目命名为“`Maths`”，并确保已选中“创建解决方案的目录”。  
  
4. 在“解决方案资源管理器”中，选择解决方案名称，然后从快捷菜单中依次选择“添加”和“新建项目”。  
  
5. 在“新建项目”对话框中，依次展开“已安装”和“Visual C#”，然后选择“Windows 应用商店”。 然后从项目模板列表中选择“单元测试库(Windows 应用商店应用)”。  
  
     ![创建单元测试项目](../test/media/ute-cs-windows-createunittestproject.png "UTE_Cs_windows_CreateUnitTestProject")  
  
6. 在 Visual Studio 编辑器中打开 UnitTest1.cs。  
  
    ```csharp  
  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Text;  
    using Microsoft.VisualStudio.TestPlatform.UnitTestFramework;  
    using Maths;  
  
    namespace RooterTests  
    {  
        [TestClass]  
        public class UnitTest1  
  
            [TestMethod]  
            public void TestMethod1()  
            {  
  
            }  
  
    ```  
  
     请注意：  
  
    1. 每个测试都是使用 `[TestMethod]` 定义的。 测试方法必须返回 void，并且不能具有任何参数。  
  
    2. 测试方法必须位于使用 `[TestClass]` 特性修饰的类中。  
  
         运行测试时，将为每个测试类创建一个实例。 测试方法以未指定的顺序进行调用。  
  
    3. 可以定义在每个模块、类或方法之前和之后调用的特殊方法。 有关详细信息，请参阅 MSDN 库中的[在单元测试中使用 Microsoft.VisualStudio.TestTools.UnitTesting 成员](../test/using-microsoft-visualstudio-testtools-unittesting-members-in-unit-tests.md)。  
  
## <a name="BKMK_Verify_that_the_tests_run_in_Test_Explorer"></a> 验证测试是否可在资源管理器中运行  
  
1. 在 **UnitTest1.cs** 文件的 `TestMethod1` 中插入一些测试代码：  
  
    ```csharp  
  
    [TestMethod]  
    public void TestMethod1()  
    {  
        Assert.AreEqual(0, 0);  
    }  
  
    ```  
  
     请注意， `Assert` 类提供了几个可以用来验证测试方法结果的静态方法。  
  
2. 在“测试”菜单上，选择“运行”，然后选择“全部运行”。  
  
     将生成并运行测试项目。 随即显示“测试资源管理器”窗口，并且测试列出在“通过的测试”下。 窗口底部的“摘要”窗格将提供有关所选测试的其他详细信息。  
  
     ![测试资源管理器](../test/media/ute-cpp-testexplorer-testmethod1.png "UTE_Cpp_TestExplorer_TestMethod1")  
  
## <a name="BKMK_Add_the_Rooter_class_to_the_Maths_project"></a>向 Maths 项目添加 Rooter 类  
  
1. 在“解决方案资源管理器”中，选择“Maths”项目名称。 从快捷菜单中依次选择“添加”和“类”。  
  
2. 将类文件命名为“`Rooter.cs`”  
  
3. 将以下代码添加到 Rooter 类 **Rooter.cs** 文件中：  
  
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
  
     `Rooter` 类声明一个构造函数和 `SqareRoot` estimator 方法。  
  
4. `SqareRoot` 方法只是一个最小实现，足以为测试设置测试基本结构。  
  
## <a name="BKMK_Couple_the_test_project_to_the_app_project"></a>将测试项目和应用项目相关联  
  
1. 将对 Maths 应用程序的引用添加到 RooterTests 项目。  
  
   1. 在“解决方案资源管理器”中，依次选择“RooterTests”项目和快捷菜单中的“添加引用...”。  
  
   2. 在“添加引用 - RooterTests”对话框中，展开“解决方案”，然后选择“项目”。 然后，选择“Maths”项。  
  
        ![添加对 Maths 项目的引用](../test/media/ute-cs-windows-addreference.png "UTE_Cs_windows_AddReference")  
  
2. 向 UnitTest1.cs 文件添加 using 语句：  
  
   1. 打开“UnitTest1.cs”。  
  
   2. 在 `using Microsoft.VisualStudio.TestPlatform.UnitTestFramework;` 行下添加以下代码：  
  
       ```csharp  
       using Maths;  
       ```  
  
3. 添加使用 Rooter 函数的测试。 将以下代码添加到 **UnitTest1.cpp**：  
  
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
  
4. 生成解决方案。  
  
    新测试将显示在测试资源管理器的“未运行的测试”节点中。  
  
5. 在“测试资源管理器”中，选择 **“全部运行”**。  
  
    ![已通过基本测试](../test/media/ute-cpp-testexplorer-basictest.png "UTE_Cpp_TestExplorer_BasicTest")  
  
   你已设置测试和代码项目，并已验证可运行测试（运行测试项目中的函数）。 现在可以开始编写实际测试和代码。  
  
## <a name="BKMK_Iteratively_augment_the_tests_and_make_them_pass"></a> 以迭代方式增加测试并使它们通过  
  
1. 添加新测试：  
  
    ```csharp  
    [TestMethod]  
    public void RangeTest()  
    {  
        Rooter rooter = new Rooter();  
        for (double v = 1e-6; v < 1e6; v = v * 3.2)  
        {  
            double expected = v;  
            double actual = rooter.SquareRoot(v*v);  
            double tolerance = ToleranceHelper(expected);  
            Assert.AreEqual(expected, actual, tolerance);  
        }  
    }  
  
    ```  
  
    > [!TIP]
    > 建议你不更改已通过的测试。 相反，请添加新测试，更新代码，使测试通过，然后添加其他测试，依此类推。  
    >   
    >  当用户更改其要求时，请禁用不再正确的测试。 编写新测试，并以相同的增量方式使他们每次运行一个。  
  
2. 在“测试资源管理器”中，选择 **“全部运行”**。  
  
3. 测试将不会通过。  
  
     ![RangeTest 未通过](../test/media/ute-cpp-testexplorer-rangetest-fail.png "UTE_Cpp_TestExplorer_RangeTest_Fail")  
  
    > [!TIP]
    > 编写测试后，立即验证每个测试是否都将失败。 这有助于避免编写从不失败的测试这一易犯错误。  
  
4. 增强受测代码，以便新测试通过。 将 **Rooter.cs** 中的 `SqareRoot` 函数更改为：  
  
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
  
5. 生成解决方案，然后在测试资源管理器中选择“全部运行” 。  
  
     现在所有三个测试都将通过。  
  
> [!TIP]
> 通过一次添加一个测试来开发代码。 确保每次迭代后所有的测试都会通过。  
  
## <a name="BKMK_Debug_a_failing_test"></a> 调试失败测试  
  
1. 将另一个测试添加到 **UnitTest1.cs** 中：  
  
   ```csharp  
   // Verify that negative inputs throw an exception.  
   [TestMethod]  
   public void NegativeRangeTest()  
   {  
       string message;  
       Rooter rooter = new Rooter();  
       for (double v = -0.1; v > -3.0; v = v - 0.5)  
       {  
           try  
           {  
               // Should raise an exception:  
               double actual = rooter.SquareRoot(v);  
  
               message = String.Format("No exception for input {0}", v);  
               Assert.Fail(message);  
           }  
           catch (ArgumentOutOfRangeException ex)  
           {  
               continue; // Correct exception.  
           }  
           catch (Exception e)  
           {  
               message = String.Format("Incorrect exception for {0}", v);  
               Assert.Fail(message);  
           }  
       }  
   }  
  
   ```  
  
2. 在“测试资源管理器”中，选择 **“全部运行”**。  
  
    测试将不会通过。 在测试资源管理器中选择测试名称。 失败的断言会突出显示。 失败消息会显示在测试资源管理器的详细信息窗格中。  
  
    ![NegativeRangeTests 失败](../test/media/ute-cpp-testexplorer-negativerangetest-fail.png "UTE_Cpp_TestExplorer_NegativeRangeTest_Fail")  
  
3. 若要查看未通过测试的原因，请单步调试函数：  
  
   1. 在 `SquareRoot` 函数的开头设置断点。  
  
   2. 在失败测试的快捷菜单上，选择“调试所选测试” 。  
  
        当在断点处停止运行时，请单步调试代码。  
  
   3. 向 Rooter 方法添加代码以捕获异常：  
  
       ```csharp  
       public double SquareRoot(double x)  
       {  
           if (x < 0.0)  
           {  
               throw new ArgumentOutOfRangeException();  
       }  
  
       ```  
  
   1. 在测试资源管理器中，选择“全部运行”以测试已更正的方法，并确保你未引入回归。  
  
   现在所有测试均通过。  
  
   ![所有测试均通过](../test/media/ute-ult-alltestspass.png "UTE_ULT_AllTestsPass")  
  
## <a name="BKMK_Refactor_the_code_"></a>重构代码  
 **简化 SquareRoot 函数的核心计算。**  
  
1. 更改结果实现  
  
    ```csharp  
    // old code  
    //result = result - (result*result - v)/(2*result);  
    // new code  
    result = (result + v/result) / 2.0;  
  
    ```  
  
2. 选择“全部运行”以测试已重构的方法，并确保你未引入回归。  
  
> [!TIP]
> 一组稳定的优良单元测试可保证你在更改代码时不会引入 Bug。  
  
 **重构测试代码以消除重复代码。**  
  
 请注意，`RangeTest` 方法对 `Assert` 方法中使用的公差变量的分母进行硬编码。 如果您计划添加其他使用同一公差计算的测试，则在多个位置使用硬编码的值可能导致错误。  
  
1. 向 Unit1Test 类添加一个私有方法以计算公差值，然后改调用该方法。  
  
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
        // old code  
        // double tolerance = expected/1000;  
        // new code  
        double tolerance = ToleranceHelper(expected);  
        Assert.AreEqual(expected, actual, tolerance);  
    }  
    ...  
  
    ```  
  
2. 选择“全部运行”，测试重构后的方法，并确保未引入任何错误。  
  
> [!NOTE]
> 若要向测试类添加帮助器方法，请勿向该方法添加 `[TestMethod]` 特性。 测试资源管理器未注册要运行的方法。
