---
title: 如何测试 UWP 应用的 C++ DLL
ms.date: 05/01/2019
ms.topic: conceptual
ms.author: mblome
manager: jillfra
ms.workload:
- uwp
author: mikeblome
ms.openlocfilehash: 18d8382bcb4f3e348443050e818f0b59c2a18688
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748075"
---
# <a name="how-to-test-a-c-dll"></a>如何测试 C++ DLL

本主题介绍使用用于 C++ 的 Microsoft Test Framework 为通用 Windows 平台 (UWP) 应用的 C++ DLL 创建单元测试的一种方法。 RooterLib DLL 通过实现计算给定数的平方根的估计的函数来演示限制计算理论的模糊内存。 然后，可能会将 DLL 包括在一个 UWP 应用中，向用户展示可通过数学完成的有趣操作。

本主题演示如何使用单元测试作为开发的第一步。 在此方法中，首先编写验证要测试的系统的特定行为的测试方法，然后编写通过测试的代码。 通过按照以下过程的顺序进行更改，您可调转此策略的顺序，即先编写要测试的代码，然后编写单元测试。

本主题还为单元测试和要测试的 DLL 创建一个 Visual Studio 解决方案和单独的项目。 你还可在 DLL 项目中直接包含单元测试，也可以为单元测试和 .DLL 创建不同的解决方案。 有关要使用的指令的提示，请参阅[向现有的 C++ 应用程序添加单元测试](../test/how-to-use-microsoft-test-framework-for-cpp.md)。

## <a name="Create_the_solution_and_the_unit_test_project"></a> 创建解决方案和单元测试项目

::: moniker range="vs-2019"

首先创建新的测试项目。 在“文件”菜单上，选择“新建” > “项目”    。 在“新建项目”对话框中，在搜索框中键入“测试”，然后将“语言”设置为 C++   。 然后从项目模板列表中选择“单元测试应用(通用 Windows)”  。

   ![创建新的 UWP 测试项目](media/vs-2019/cpp-new-uwp-test-project-vs2019.png)

::: moniker-end

::: moniker range="vs-2017"

首先创建新的测试项目。 在“文件”菜单上，选择“新建” > “项目”    。 在“新建项目”对话框中，依次展开“已安装” > “Visual C++”，然后选择“Windows 通用”     。 然后从项目模板列表中选择“单元测试应用(通用 Windows)”  。

::: moniker-end

1. 在“新建项目”对话框中，依次展开“已安装”   > “Visual C#”  ，然后选择“Windows 通用”  。 然后从项目模板列表中选择“单元测试应用(通用 Windows)”  。

2. 将项目命名为 `RooterLibTests`；指定位置；将解决方案命名为 `RooterLib`；确保选中了“创建解决方案的目录”  。

     ![指定解决方案和项目名称以及位置](../test/media/ute_cpp_windows_unittestlib_createspecs.png)

3. 在新项目中，打开 **unittest1.cpp**。

     ![unittest1.cpp](../test/media/ute_cpp_windows_unittest1_cpp.png)

     请注意：

    - 每个测试都使用 `TEST_METHOD(YourTestName){...}` 来定义。

         你不必编写常规函数签名。 签名由宏 TEST_METHOD 来创建。 该宏将生成一个返回 void 的实例函数。 它还将生成返回有关测试方法的信息的静态函数。 此信息允许测试资源管理器查找方法。

    - 使用 `TEST_CLASS(YourClassName){...}`将测试方法分组为各个类。

         当测试运行时，将为每个测试类创建一个实例。 测试方法以未指定的顺序进行调用。 可以定义在每个模块、类或方法之前和之后调用的特殊方法。 有关详细信息，请参阅[使用 Microsoft.VisualStudio.TestTools.CppUnitTestFramework](how-to-use-microsoft-test-framework-for-cpp.md)。

## <a name="Verify_that_the_tests_run_in_Test_Explorer"></a> 验证测试是否可在资源管理器中运行

1. 插入某些测试代码：

    ```cpp
    TEST_METHOD(TestMethod1)
    {
        Assert::AreEqual(1,1);
    }
    ```

     请注意， `Assert` 类提供了几个可以用来验证测试方法结果的静态方法。

2. 在“测试”  菜单上，选择“运行”  ，然后选择“全部运行”  。

     将生成并运行测试项目。 随即显示测试资源管理器窗口，并且测试在“通过的测试”下列出   。 窗口底部的“摘要”窗格将提供有关所选测试的其他详细信息  。

     ![测试资源管理器](../test/media/ute_cpp_testexplorer_testmethod1.png)

## <a name="Add_the_DLL_project_to_the_solution"></a> 向解决方案添加 DLL 项目

::: moniker range="vs-2019"

在解决方案资源管理器中，选择解决方案名称  。 从快捷菜单中选择“添加”，然后选择“新建项目”   。 在“添加新项目”对话框中，将“语言”设置为 C++ 并在搜索框中键入“DLL”   。 从结果列表中，选择“单元测试应用（通用 Windows - C++/CX）”  。

![创建 RooterLib 项目](../test/media/vs-2019/cpp-new-uwp-test-project-vs2019.png)

::: moniker-end

::: moniker range="vs-2017"
在解决方案资源管理器中，选择解决方案名称  。 从快捷菜单中选择“添加”，然后选择“新建项目”   。

![创建 RooterLib 项目](../test/media/ute_cpp_windows_rooterlib_create.png)

::: moniker-end

1. 在“添加新项目”  对话框中，选择“DLL (UWP 应用)”  。

2. 将以下代码添加到 *RooterLib.h* 文件中：

    ```cpp
    // The following ifdef block is the standard way of creating macros which make exporting
    // from a DLL simpler. All files within this DLL are compiled with the ROOTERLIB_EXPORTS
    // symbol defined on the command line. This symbol should not be defined on any project
    // that uses this DLL. This way any other project whose source files include this file see
    // ROOTERLIB_API functions as being imported from a DLL, whereas this DLL sees symbols
    // defined with this macro as being exported.
    #ifdef ROOTERLIB_EXPORTS
    #define ROOTERLIB_API  __declspec(dllexport)
    #else
    #define ROOTERLIB_API __declspec(dllimport)
    #endif //ROOTERLIB_EXPORTS

    class ROOTERLIB_API CRooterLib {
    public:
        CRooterLib(void);
        double SquareRoot(double v);
    };
    ```

     注释向 dll 的开发人员以及任何在其项目中引用 DLL 的用户说明了 ifdef 块。 可以通过使用 DLL 的项目属性将 ROOTERLIB_EXPORTS 符号添加到命令行。

     `CRooterLib` 类声明一个构造函数和 `SqareRoot` estimator 方法。

3. 将 ROOTERLIB_EXPORTS 符号添加到命令行。

    1. 在解决方案资源管理器中，选择“RooterLib”项目，然后从快捷菜单选择“属性”    。

         ![添加预处理器符号定义](../test/media/ute_cpp_windows_addpreprocessorsymbol.png)

    2. 在“RooterLib 属性页”对话框中，展开“配置属性”，展开“C++”并选择“预处理器”     。

    3. 从“预处理器定义”列表选择“\<编辑...>”，然后在“预处理器定义”对话框中添加 `ROOTERLIB_EXPORTS`    。

4. 添加已声明函数的最小实现。 打开 *RooterLib.cpp* 并添加以下代码：

    ```cpp
    // constructor
    CRooterLib::CRooterLib()
    {
    }

    // Find the square root of a number.
    double CRooterLib::SquareRoot(double v)
    {
        return 0.0;
    }

    ```

## <a name="make_the_dll_functions_visible_to_the_test_code"></a>使 dll 函数对测试代码可见

1. 将 RooterLib 添加到 RooterLibTests 项目。

   1. 在解决方案资源管理器中，选择“RooterLibTests”项目，然后选择快捷菜单上的“添加” > “引用”     。

   1. 在“添加引用”对话框中，选择“项目”   。 然后选择“RouterLib”  项。

2. 将 RooterLib 头文件包括到 *unittest1.cpp* 中。

   1. 打开 *unittest1.cpp*。

   2. 将此代码添加到以下 `#include "CppUnitTest.h"` 行：

       ```cpp
       #include "..\RooterLib\RooterLib.h"
       ```

3. 添加一个使用 imported 函数的测试。 将以下代码添加到 *unittest1.cpp*：

   ```cpp
   TEST_METHOD(BasicTest)
   {
       CRooterLib rooter;
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

    新测试将显示在测试资源管理器的“未运行的测试”节点中   。

5. 在“测试资源管理器”  中，选择“全部运行”  。

    ![已通过基本测试](../test/media/ute_cpp_testexplorer_basictest.png)

   你已设置测试和代码项目，并已验证可运行测试（运行测试项目中的函数）。 现在可以开始编写实际测试和代码。

## <a name="Iteratively_augment_the_tests_and_make_them_pass"></a> 以迭代方式增加测试并使它们通过

1. 添加新测试：

    ```cpp
    TEST_METHOD(RangeTest)
    {
        CRooterLib rooter;
        for (double v = 1e-6; v < 1e6; v = v * 3.2)
        {
            double expected = v;
            double actual = rooter.SquareRoot(v*v);
            double tolerance = expected/1000;
            Assert::AreEqual(expected, actual, tolerance);
        }
    };
    ```

    > [!TIP]
    > 建议你不更改已通过的测试。 相反，请添加新测试，更新代码，使测试通过，然后添加其他测试，依此类推。
    >
    > 当用户更改其要求时，请禁用不再正确的测试。 编写新测试，并以相同的增量方式使他们每次运行一个。

2. 在“测试资源管理器”  中，选择“全部运行”  。

3. 测试将不会通过。

     ![RangeTest 未通过](../test/media/ute_cpp_testexplorer_rangetest_fail.png)

    > [!TIP]
    > 验证每个测试是否在编写之后立即失败。 这有助于避免编写从不失败的测试这一易犯错误。

4. 增强受测代码，以便新测试通过。 将以下内容添加到 *RooterLib.cpp*：

    ```cpp
    #include <math.h>
    ...
    // Find the square root of a number.
    double CRooterLib::SquareRoot(double v)
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

5. 生成解决方案，然后在“测试资源管理器”  中选择“全部运行”  。

     两个测试均通过。

> [!TIP]
> 通过一次添加一个测试来开发代码。 确保每次迭代后所有的测试都会通过。

## <a name="Debug_a_failing_test"></a> 调试失败测试

1. 将另一个测试添加到 *unittest1.cpp*：

   ```cpp
   // Verify that negative inputs throw an exception.
    TEST_METHOD(NegativeRangeTest)
    {
      wchar_t message[200];
      CRooterLib rooter;
      for (double v = -0.1; v > -3.0; v = v - 0.5)
      {
        try
        {
          // Should raise an exception:
          double result = rooter.SquareRoot(v);

          swprintf_s(message, L"No exception for input %g", v);
          Assert::Fail(message, LINE_INFO());
        }
        catch (std::out_of_range ex)
        {
          continue; // Correct exception.
        }
        catch (...)
        {
          swprintf_s(message, L"Incorrect exception for %g", v);
          Assert::Fail(message, LINE_INFO());
        }
      }
   };
   ```

2. 在“测试资源管理器”  中，选择“全部运行”  。

    测试将不会通过。 在“测试资源管理器”  中选择测试名称。 失败的断言会突出显示。 失败消息会显示在“测试资源管理器”  的“详细信息”窗格中。

    ![NegativeRangeTests 未通过](../test/media/ute_cpp_testexplorer_negativerangetest_fail.png)

3. 若要查看未通过测试的原因，请单步调试函数：

   1. 在 `SquareRoot` 函数的开头设置断点。

   2. 在失败测试的快捷菜单上，选择“调试所选测试”  。

        当在断点处停止运行时，请单步调试代码。

   3. 将代码添加到 *RooterLib.cpp* 来捕获异常：

       ```cpp
       #include <stdexcept>
       ...
       double CRooterLib::SquareRoot(double v)
       {
           //Validate the input parameter:
           if (v < 0.0)
           {
             throw std::out_of_range("Can't do square roots of negatives");
           }
       ...

       ```

   1. 在测试资源管理器中，选择“全部运行”以测试已更正的方法，并确保未引入回归   。

   现在所有测试均通过。

   ![所有测试通过](../test/media/ute_ult_alltestspass.png)

## <a name="Refactor_the_code_without_changing_tests"></a> 在不更改测试的情况下重构代码

1. 简化 `SquareRoot` 函数中的核心计算过程：

    ```csharp
    // old code
    //result = result - (result*result - v)/(2*result);
    // new code
    result = (result + v/result) / 2.0;
    ```

2. 选择“全部运行”  以测试已重构的方法，并确保你未引入回归。

    > [!TIP]
    > 一组稳定的优良单元测试可保证你在更改代码时不会引入 Bug。
    >
    > 将重构更改与其他更改分开。
