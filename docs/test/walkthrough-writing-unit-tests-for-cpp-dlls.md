---
title: 如何：编写 C++ DLL 单元测试
ms.date: 06/13/2019
ms.topic: how-to
ms.author: corob
manager: markl
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: 16020c0928229c80a9eb33b3bc4804b004d9f432
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85816002"
---
# <a name="how-to-write-unit-tests-for-c-dlls"></a>如何：编写 C++ DLL 单元测试

本演练介绍如何使用测试优先方法开发本机 C++ DLL。 基本步骤如下：

1. [创建本机测试项目](#create_test_project)。 测试项目位于与 DLL 项目相同的解决方案中。

2. [创建 DLL 项目](#create_dll_project)。 此演练将创建一个新 DLL，但测试现有 DLL 的过程类似。

3. [使 DLL 函数对测试可见](#make_functions_visible)。

4. [以迭代方式扩大测试](#iterate)。 建议使用“红-绿-重构”循环，其中代码开发由测试来主导。

5. [调试失败测试](#debug)。 可以在调试模式下运行测试。

6. [在保持测试不变时重构](#refactor)。 重构是指改善代码的结构，而不更改其外部行为。 你可以通过重构来提高代码的性能、扩展性或可读性。 由于目的不是更改行为，因此，在对代码进行重构更改时不会更改测试。 测试有助于确保重构时不引入 Bug。

7. [检查覆盖率](using-code-coverage-to-determine-how-much-code-is-being-tested.md)。 单元测试在执行更多代码时更加有用。 可以查看测试使用了哪些代码部分。

8. [将单元与外部资源隔离](using-stubs-to-isolate-parts-of-your-application-from-each-other-for-unit-testing.md)。 通常，DLL 依赖于你开发的系统的其他组件，例如其他 DLL、数据库或远程子系统。 在测试每个单元时，使之与它的依赖项相隔离非常有用。 外部组件可能会降低测试的运行速度。 在开发期间，其他组件可能不完整。

## <a name="create-a-native-unit-test-project"></a><a name="create_test_project"></a> 创建本机单元测试项目

1. 在“文件”菜单上，选择“新建” > “项目”    。

     **Visual Studio 2017 及更早版本**：依次展开“已安装” > “模板” > “Visual C++” > “测试”     。
     **Visual Studio 2019** ：将“语言”设置为 C++ 并在搜索框中键入“测试”  。

     选择“本机单元测试项目”  模板，或任何所需的已安装框架。 如果选择其他模板（如 Google Test 或 Boost.Test），则基本原则是相同的，不过某些细节将有所不同。

     在本演练中，该测试项目的名称为 `NativeRooterTest`。

2. 在新项目中，检查 **unittest1.cpp**

     ![具有 TEST_CLASS 和 TEST_METHOD 的测试项目](../test/media/utecpp2.png)

     请注意：

    - 每个测试都使用 `TEST_METHOD(YourTestName){...}`来定义。

         你不必编写常规函数签名。 签名由宏 TEST_METHOD 来创建。 该宏将生成一个返回 void 的实例函数。 它还将生成返回有关测试方法的信息的静态函数。 此信息允许测试资源管理器查找方法。

    - 使用 `TEST_CLASS(YourClassName){...}`将测试方法分组为各个类。

         当测试运行时，将为每个测试类创建一个实例。 测试方法以未指定的顺序进行调用。 可以定义在每个模块、类或方法之前和之后调用的特殊方法。

3. 验证测试是否可在资源管理器中运行：

    1. 插入某些测试代码：

        ```cpp
        TEST_METHOD(TestMethod1)
        {
            Assert::AreEqual(1,1);
        }
        ```

         请注意， `Assert` 类提供了几个可以用来验证测试方法结果的静态方法。

    2. 在“测试”  菜单中，选择“运行”   > “全部测试”  。

         将生成并运行测试。

         此时将显示测试资源管理器  。

         测试显示在“通过的测试”  下方。

         ![具有 1 个已通过测试的单元测试资源管理器](../test/media/utecpp04.png)

## <a name="create-a-dll-project"></a><a name="create_dll_project"></a>创建 DLL 项目

::: moniker range="vs-2019"

以下步骤说明如何在 Visual Studio 2019 中创建 DLL 项目。

1. 使用“Windows 桌面向导”创建 C++ 项目  ：右键单击“解决方案资源管理器”中的解决方案名称，然后依次选择“添加” > “新建项目”    。 将“语言”设置为 C++，然后在搜索框中键入“windows”  。 从结果列表中选择“Windows 桌面向导”  。

     在本演练中，该项目的名称为 `RootFinder`。

2. 按“创建”  。 在下一个对话框中，在“应用程序类型”下选择“动态链接库 (dll)”，同时选中“导出符号”    。

     “导出符号”  选项生成可用来声明导出方法的便利宏。

     ![为 DLL 设置的 C++ 项目向导和导出符号](../test/media/vs-2019/windows-desktop-project-dll.png)

3. 在主体 .h 文件中声明导出的函数  ：

     ![使用 API 宏新建 DLL 代码项目和 .h 文件](../test/media/utecpp07.png)

     声明符 `__declspec(dllexport)` 会导致类的公共和受保护成员在 DLL 外可见。 有关详细信息，请参阅 [Using dllimport and dllexport in C++ Classes](/cpp/cpp/using-dllimport-and-dllexport-in-cpp-classes)。

4. 在主体 .cpp 文件中，添加最小的函数体  ：

    ```cpp
        // Find the square root of a number.
        double CRootFinder::SquareRoot(double v)
        {
            return 0.0;
        }
    ```

::: moniker-end

::: moniker range="vs-2017"

以下步骤说明如何在 Visual Studio 2017 中创建 DLL 项目。

1. 使用“Win32 项目”模板创建 C++ 项目  。

     在本演练中，该项目的名称为 `RootFinder`。

2. 在 Win32 应用程序向导中，选择“DLL”  和“导出符号”  。

     “导出符号”  选项生成可用来声明导出方法的便利宏。

     ![为 DLL 设置的 C++ 项目向导和导出符号](../test/media/utecpp06.png)

3. 在主体 .h 文件中声明导出的函数  ：

     ![使用 API 宏新建 DLL 代码项目和 .h 文件](../test/media/utecpp07.png)

     声明符 `__declspec(dllexport)` 会导致类的公共和受保护成员在 DLL 外可见。 有关详细信息，请参阅 [Using dllimport and dllexport in C++ Classes](/cpp/cpp/using-dllimport-and-dllexport-in-cpp-classes)。

4. 在主体 .cpp 文件中，添加最小的函数体  ：

    ```cpp
        // Find the square root of a number.
        double CRootFinder::SquareRoot(double v)
        {
            return 0.0;
        }
    ```

::: moniker-end

## <a name="couple-the-test-project-to-the-dll-project"></a><a name="make_functions_visible"></a> 将测试项目耦合到 DLL 项目

1. 将 DLL 项目添加到测试项目的项目引用中：

   1. 右键单击解决方案资源管理器中的测试项目节点，并选择“添加” > “引用”    。

   2. 在“添加引用”  对话框中，选择 DLL 项目并选择“添加”  。

        ![C++ 项目属性 | 添加新引用](../test/media/utecpp09.png)

2. 在主体单元测试 .cpp 文件中，将 DLL 代码的 .h 文件包括在内   ：

   ```cpp
   #include "..\RootFinder\RootFinder.h"
   ```

3. 添加使用导出函数的基本测试：

   ```cpp
   TEST_METHOD(BasicTest)
   {
      CRootFinder rooter;
      Assert::AreEqual(
         // Expected value:
         0.0,
         // Actual value:
         rooter.SquareRoot(0.0),
         // Tolerance:
         0.01,
        // Message:
        L"Basic test failed",
        // Line number - used if there is no PDB file:
        LINE_INFO());
   }
   ```

4. 生成解决方案。

    新测试出现在测试资源管理器中  。

5. 在“测试资源管理器”  中，选择“全部运行”  。

    ![单元测试资源管理器 - 已通过基本测试](../test/media/utecpp10.png)

   你已设置测试和代码项目，并已验证可运行测试（运行测试项目中的函数）。 现在可以开始编写实际测试和代码。

## <a name="iteratively-augment-the-tests-and-make-them-pass"></a><a name="iterate"></a> 以迭代方式增加测试并使它们通过

1. 添加新测试：

    ```cpp
    TEST_METHOD(RangeTest)
    {
      CRootFinder rooter;
      for (double v = 1e-6; v < 1e6; v = v * 3.2)
      {
        double actual = rooter.SquareRoot(v*v);
        Assert::AreEqual(v, actual, v/1000);
      }
    }
    ```

    > [!TIP]
    > 建议你不更改已通过的测试。 相反，请添加新测试，更新代码，使测试通过，然后添加其他测试，依此类推。
    >
    > 当用户更改其要求时，请禁用不再正确的测试。 编写新测试，并以相同的增量方式使他们每次运行一个。

2. 生成解决方案，然后在测试资源管理器中选择“全部运行”   。

     新未通过测试。

     ![RangeTest 未通过](../test/media/ute_cpp_testexplorer_rangetest_fail.png)

    > [!TIP]
    > 验证每个测试是否在编写之后立即失败。 这有助于避免编写从不失败的测试这一易犯错误。

3. 增强 DLL 代码，以便新测试可通过：

    ```cpp
    #include <math.h>
    ...
    double CRootFinder::SquareRoot(double v)
    {
      double result = v;
      double diff = v;
      while (diff > result/1000)
      {
        double oldResult = result;
        result = result - (result*result - v)/(2*result);
        diff = abs (oldResult - result);
      }
      return result;
    }
    ```

4. 生成解决方案，然后在“测试资源管理器”  中选择“全部运行”  。

     两个测试均通过。

     ![单元测试资源管理器 - 已通过范围测试](../test/media/utecpp12.png)

    > [!TIP]
    > 通过一次添加一个测试来开发代码。 确保每次迭代后所有的测试都会通过。

## <a name="debug-a-failing-test"></a><a name="debug"></a> 调试失败测试

1. 添加另一个测试：

    ```cpp
    #include <stdexcept>
    ...
    // Verify that negative inputs throw an exception.
    TEST_METHOD(NegativeRangeTest)
    {
      wchar_t message[200];
      CRootFinder rooter;
      for (double v = -0.1; v > -3.0; v = v - 0.5)
      {
        try
        {
          // Should raise an exception:
          double result = rooter.SquareRoot(v);

          _swprintf(message, L"No exception for input %g", v);
          Assert::Fail(message, LINE_INFO());
        }
        catch (std::out_of_range ex)
        {
          continue; // Correct exception.
        }
        catch (...)
        {
          _swprintf(message, L"Incorrect exception for %g", v);
          Assert::Fail(message, LINE_INFO());
        }
      }
    }
    ```

2. 生成解决方案并选择“全部运行”  。

3. 打开（或双击）失败的测试。

     失败的断言会突出显示。 失败消息会显示在“测试资源管理器”  的“详细信息”窗格中。

     ![NegativeRangeTests 未通过](../test/media/ute_cpp_testexplorer_negativerangetest_fail.png)

4. 若要查看未通过测试的原因，请单步调试函数：

    1. 在 SquareRoot 函数的开始处设置一个断点。

    2. 在失败测试的快捷菜单上，选择“调试所选测试”  。

         当在断点处停止运行时，请单步调试代码。

5. 在你开发的函数中插入代码：

    ```cpp

    #include <stdexcept>
    ...
    double CRootFinder::SquareRoot(double v)
    {
        // Validate parameter:
        if (v < 0.0)
        {
          throw std::out_of_range("Can't do square roots of negatives");
        }

    ```

6. 现在所有测试均通过。

   ![所有测试通过](../test/media/ute_ult_alltestspass.png)

::: moniker range="vs-2017"

> [!TIP]
> 如果各个测试没有防止其以任何顺序运行的依赖项，则可使用工具栏上的 ![UTE_parallelicon - 小](../test/media/ute_parallelicon-small.png)切换按钮来打开并行测试执行。 这可以显著降低运行所有测试所需的时间。

::: moniker-end

::: moniker range=">=vs-2019"

> [!TIP]
> 如果各个测试没有阻止其以任何顺序运行的依赖项，则可以在工具栏的设置菜单中启用并行测试执行。 这可以显著降低运行所有测试所需的时间。

::: moniker-end

## <a name="refactor-the-code-without-changing-tests"></a><a name="refactor"></a> 在不更改测试的情况下重构代码

1. 简化 SquareRoot 函数中的核心计算：

    ```cpp
    // old code:
    //   result = result - (result*result - v)/(2*result);
    // new code:
         result = (result + v/result)/2.0;

    ```

2. 生成解决方案并选择“全部运行”  ，以确保未引入错误。

    > [!TIP]
    > 良好的单元测试组可以让你确信在更改代码时不会引入 Bug。
    >
    > 将重构更改与其他更改分开。

## <a name="next-steps"></a>后续步骤

- **隔离。** 大多数 DLL 依赖其他子系统，如数据库和其他 DLL。 这些其他组件通常并行开发。 若要允许在其他组件尚不可用时执行单元测试，你必须替代模拟或

- **版本验证测试。** 可以每隔固定时间在团队的生成服务器上执行测试。 这可以确保在集成多名团队成员的工作时不会引入 Bug。

- **签入测试。** 在每个团队成员向源代码管理签入代码之前，您可以强制执行某些测试。 这通常是一组完整版本验证测试中的一部分。

   也可以强制实施最低级别的代码覆盖率。

## <a name="see-also"></a>请参阅

- [将单元测试添加到现有 C++ 应用程序](../test/how-to-use-microsoft-test-framework-for-cpp.md)
- [使用 Microsoft.VisualStudio.TestTools.CppUnitTestFramework](how-to-use-microsoft-test-framework-for-cpp.md)
- [调试本机代码](../debugger/debugging-native-code.md)
- [演练：创建和使用动态链接库 (C++)](/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp)
- [导入和导出](/cpp/build/importing-and-exporting)
