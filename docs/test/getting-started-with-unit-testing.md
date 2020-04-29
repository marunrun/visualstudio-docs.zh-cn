---
title: 单元测试入门
ms.date: 04/07/2020
ms.topic: conceptual
helpviewer_keywords:
- unit testing, create unit test plans
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c167e98f9419842876aed713e008b8746064669a
ms.sourcegitcommit: dab57cebd484228e6f0cf7ab1b9685c575410c06
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/25/2020
ms.locfileid: "82153040"
---
# <a name="get-started-with-unit-testing"></a>单元测试入门

使用 Visual Studio 定义和运行单元测试，使代码保持正常运行、确保代码覆盖率并在客户之前找到错误和缺陷。 经常运行单元测试，确保代码正常运行。

## <a name="create-unit-tests"></a>创建单元测试

本节介绍了如何创建单元测试项目。

1. 在 Visual Studio 中，打开要测试的项目。

   为了演示示例单元测试，本文测试了简单的“Hello World”项目（名为“HelloWorldCore”）  。 此类项目的示例代码如下所示：

   ```csharp
   namespace HelloWorldCore

      public class Program
      {
         public static void Main()
         {
            Console.WriteLine("Hello World!");
         }
      }
   ```

1. 在“解决方案资源管理器”中，选择解决方案节点  。 然后，在顶部菜单栏中，选择“文件” > “添加” > “新项目”    。

1. 在新项目对话框中，找到并选择要使用的测试框架的单元测试项目模板。

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 中的单元测试项目模板](media/vs-2019/add-new-test-project.png)

   单击“下一步”，选择测试项目的名称，然后单击“创建”   。

   ::: moniker-end

   ::: moniker range="vs-2017"

   ![Visual Studio 2019 中的单元测试项目模板](media/mstest-test-project-template.png)

   选择测试项目的名称，然后单击“确定”  。

   ::: moniker-end

   项目将添加到解决方案中。

   ![解决方案资源管理器中的单元测试项目](media/vs-2019/solution-explorer.png)

1. 在单元测试项目中，右键单击“引用”或“依赖项”，然后选择“添加引用”，添加对要测试的项目的引用    。

1. 选择包含待测试代码的项目，单击“确定”  。

   ![在 Visual Studio 中添加项目引用](media/vs-2019/reference-manager.png)

1. 向单元测试方法添加代码。

   例如，对于 MSTest 项目，可以使用以下代码。

   ```csharp
   using Microsoft.VisualStudio.TestTools.UnitTesting;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
      [TestClass]
      public class UnitTest1
      {
         private const string Expected = "Hello World!";
         [TestMethod]
         public void TestMethod1()
         {
            using (var sw = new StringWriter())
            {
               Console.SetOut(sw);
               HelloWorldCore.Program.Main();

               var result = sw.ToString().Trim();
               Assert.AreEqual(Expected, result);
            }
         }
      }
   }
   ```

   或者，对于 NUnit 项目，可以使用以下代码。

   ```csharp
   using NUnit.Framework;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
      public class Tests
      {
         private const string Expected = "Hello World!";

         [SetUp]
         public void Setup()
         {
         }
         [Test]
         public void TestMethod1()
         {
            using (var sw = new StringWriter())
            {
               Console.SetOut(sw);
               HelloWorldCore.Program.Main();

               var result = sw.ToString().Trim();
               Assert.AreEqual(Expected, result);
            }
         }
      }
   }
   ```

> [!TIP]
> 有关创建单元测试的更详细信息，请参阅[创建并运行托管代码的单元测试](walkthrough-creating-and-running-unit-tests-for-managed-code.md)。

## <a name="run-unit-tests"></a>运行单元测试

1. 打开[测试资源管理器](../test/run-unit-tests-with-test-explorer.md)。

   ::: moniker range=">=vs-2019"
   若要打开测试资源管理器，请选择顶部菜单栏中的“测试”>“测试资源管理器”   。
   ::: moniker-end
   ::: moniker range="vs-2017"
   若要打开测试资源管理器，请选择顶部菜单栏中的“测试”>“Windows”>“测试资源管理器”    。
   ::: moniker-end

1. 单击“全部运行”，运行单元测试  。

   ![在测试资源管理器中运行单元测试](media/vs-2019/test-explorer-run-all.png)

   测试完成后，绿色复选标记表示测试通过。 红色“x”图标表示测试失败。

   ![在测试资源管理器中查看单元测试结果](media/vs-2019/unit-test-passed.png)

> [!TIP]
> 可以使用[测试资源管理器](../test/run-unit-tests-with-test-explorer.md)从内置测试框架 (MSTest) 或第三方测试框架运行单元测试。 可以将测试分组为不同类别、筛选测试列表，以及创建、保存和运行测试播放列表。 你还可以调试测试并分析测试性能和代码覆盖率。

## <a name="view-live-unit-test-results"></a>查看实时单元测试结果

如果在 Visual Studio 2017 或更高版本中使用 MSTest、xUnit 或 NUnit 测试框架，可查看单元测试的实时结果。

> [!NOTE]
> 只有企业版中提供 Live Unit Testing 功能。

1. 选择“测试” > “Live Unit Testing” > “启动”，从“测试”菜单启用 Live Unit Testing     。

   ::: moniker range="vs-2017"

   ![启用 Live Unit Testing](media/live-test-results-start.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![在 Visual Studio 2019 中启用 Live Unit Testing](media/vs-2019/start-live-unit-testing.png)

   ::: moniker-end

1. 编写和编辑代码时，请在代码编辑器窗口中查看测试的结果。

   ![查看测试的结果](media/vs-2019/live-unit-testing-results.png)

1. 单击测试结果指示器查看详细信息，例如涵盖该方法的测试的名称。

   ![选择测试结果指示符](media/vs-2019/live-unit-testing-details.png)

有关 Live Unit Testing 的详细信息，请参阅 [Live Unit Testing](../test/live-unit-testing-intro.md)。

## <a name="generate-unit-tests-with-intellitest"></a>使用 IntelliTest 生成单元测试

运行 IntelliTest 时，可以看到哪些测试会失败，并可添加任何必要的代码来修复它们。 你可选择要保存到测试项目中的已生成测试，以提供回归套件。 当你更改代码时，重新运行 IntelliTest，以使生成的测试与你的代码更改同步。 若要了解如何操作，请参阅[使用 IntelliTest 为你的代码生成单元测试](../test/generate-unit-tests-for-your-code-with-intellitest.md)。

> [!TIP]
> IntelliTest 仅适用于面向 .NET Framework 的托管代码。

![使用 IntelliTest 生成单元测试](media/intellitest.png)

## <a name="analyze-code-coverage"></a>分析代码覆盖率

若要确定正在由编码的测试（例如单元测试）实际进行测试的项目代码的比例，则可以使用 Visual Studio 的代码覆盖率功能。 若要有效防止 Bug，测试应作用于你的大部分代码。 若要了解如何操作，请参阅[使用代码覆盖率确定所测试的代码量](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)。

## <a name="use-a-third-party-test-framework"></a>使用第三方测试框架

通过使用第三方测试框架（如 Boost、Google、和 NUnit），可以在 Visual Studio 中运行单元测试。 使用 NuGet 包管理器为所选框架安装 NuGet 包  。 或者，对于 NUnit 和 xUnit 测试框架，Visual Studio 包含预配置的测试项目模板，其中包含必要的 NuGet 包。

创建使用 [NUnit](https://nunit.org/) 的单元测试：

1. 打开包含待测试代码的解决方案。

2. 右键单击“解决方案资源管理器”中的解决方案，然后选择“添加” > “新建项目”    。

3. 选择“NUnit 测试项目”项目模板  。

   ::: moniker range=">=vs-2019"

   ![Visual Studio 2019 中的 NUnit 测试项目模板](media/vs-2019/nunit-test-project-template.png)

   单击“下一步”，为项目命名，然后单击“创建”   。

   ::: moniker-end

   ::: moniker range="vs-2017"

   为项目命名，然后单击“确定”进行创建  。

   ::: moniker-end

   项目模板包括对 NUnit 和 NUnit3TestAdapter 的 NuGet 引用。

   ![解决方案资源管理器中的 NUnit NuGet 依赖项](media/vs-2019/nunit-nuget-dependencies.png)

4. 将测试项目中的引用添加到包含待测试代码的项目中。

   右键单击“解决方案资源管理器”中的项目，然后选择“添加” > “引用”    。 （还可以从“引用”  或“依赖项”  节点右键单击菜单来添加一个引用。）

5. 将代码添加到测试方法。

   ![将代码添加到单元测试代码文件](media/vs-2019/unit-test-method.png)

6. 从测试资源管理器运行测试，或右键单击测试代码并选择“运行测试”   。

## <a name="see-also"></a>请参阅

* [演练：创建并运行托管代码的单元测试](walkthrough-creating-and-running-unit-tests-for-managed-code.md)
* [创建单元测试命令](create-unit-tests-menu.md)
* [使用 IntelliTest 生成测试](generate-unit-tests-for-your-code-with-intellitest.md)
* [使用测试资源管理器运行测试](run-unit-tests-with-test-explorer.md)
* [分析代码覆盖率](using-code-coverage-to-determine-how-much-code-is-being-tested.md)
