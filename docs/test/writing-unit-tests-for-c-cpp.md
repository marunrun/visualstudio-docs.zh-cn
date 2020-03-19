---
title: 编写适用于 C/C++ 的单元测试
description: 使用 CTest、Boost.Test 和 Google Test 等各种测试框架在 Visual Studio 中编写 C++ 单元测试。
ms.date: 02/08/2020
ms.topic: conceptual
ms.author: corob
manager: markl
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: 354ccad121884c99541057a2e0e0a47d9d2a4341
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "78937558"
---
# <a name="write-unit-tests-for-cc-in-visual-studio"></a>在 Visual Studio 中编写 C/C++ 单元测试

可使用“测试资源管理器”窗口编写并运行 C++ 单元测试  。 它的工作方式与其他语言的相同。 有关使用“测试资源管理器”  的详细信息，请参阅[使用测试资源管理器运行单元测试](run-unit-tests-with-test-explorer.md)。

> [!NOTE]
> C++ 不支持某些功能，如 Live Unit Testing、编码的 UI 测试和 IntelliTest。

Visual Studio 包含这些 C++ 测试框架，无需进行额外下载：

- 适用于 C++ 的 Microsoft 单元测试框架
- Google Test
- Boost.Test
- CTest

除了使用已安装的框架，你还可为要在 Visual Studio 中使用的任何框架编写自己的测试适配器。 测试适配器可以将单元测试与“测试资源管理器”  窗口集成。 在 [Visual Studio Marketplace](https://marketplace.visualstudio.com) 上提供了几个第三方适配器。 有关详细信息，请参阅[安装第三方单元测试框架](install-third-party-unit-test-frameworks.md)。

**Visual Studio 2017 及更高版本（Professional 和 Enterprise）**

C++ 单元测试项目支持 [CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md)。

**Visual Studio 2017 及更高版本（所有版本）**

- **Google Test 适配器**作为“使用 C++ 的桌面开发”  工作负荷的默认组件包含在内。 它具有可添加到解决方案的项目模板。 要添加它，可使用解决方案资源管理器中“解决方案”节点上的“添加新项目”右键单击菜单   。 它还提供了可通过“工具” > “选项”进行配置的选项   。 有关详细信息，请参阅[如何：在 Visual Studio 中使用 Google Test](how-to-use-google-test-for-cpp.md)。

- **Boost.Test** 作为“使用 C++ 的桌面开发”  工作负荷的默认组件包含在内。 它与测试资源管理器集成，但当前没有项目模板  。 必须手动配置它。 有关详细信息，请参阅[如何：在 Visual Studio 中使用 Boost.Test](how-to-use-boost-test-for-cpp.md)。

- CTest  支持随附在 C++ CMake 工具  组件中，该组件是“使用 C++ 的桌面开发”  工作负载的一部分。 有关详细信息，请参阅[如何：在 Visual Studio 中使用 CTest](how-to-use-ctest-for-cpp.md)。

**Visual Studio 2015 及更早版本**

可在 Visual Studio Marketplace 中下载 Google Test 适配器和 Boost.Test 适配器扩展。 可在 [Boost.Test 测试适配器](https://marketplace.visualstudio.com/items?itemName=VisualCPPTeam.TestAdapterforBoostTest)和 [Google Test 测试适配器](https://marketplace.visualstudio.com/items?itemName=VisualCPPTeam.TestAdapterforGoogleTest)中找到它们。

## <a name="basic-test-workflow"></a>基本测试工作流

以下各部分演示开始使用 C++ 单元测试的基本步骤。 Microsoft 和 Google Test 框架的基本配置非常相似。 Boost.Test 要求手动创建测试项目。

::: moniker range="vs-2019"

### <a name="create-a-test-project-in-visual-studio-2019"></a>在 Visual Studio 2019 中创建测试项目

在一个或多个测试项目中定义并运行测试。 在要测试的代码所在的解决方案中创建项目。 若要向现有解决方案添加新的测试项目，请右键单击解决方案资源管理器中的“解决方案”节点  。 在弹出菜单中，选择“添加” > “新建项目”   。 将“语言”设置为 C++ 并在搜索框中键入“测试”  。 下图显示安装“使用 C++ 的桌面开发”和“UWP 开发”工作负载后可用的测试项目   ：

![Visual Studio 2019 中的 C++ 项目](media/vs-2019/cpp-new-test-project-vs2019.png)

::: moniker-end

::: moniker range="vs-2017"

### <a name="create-a-test-project-in-visual-studio-2017"></a>在 Visual Studio 2017 中创建测试项目

在一个或多个测试项目中定义并运行测试。 在要测试的代码所在的解决方案中创建项目。 若要添加新的测试项目，请右键单击解决方案资源管理器中的“解决方案”节点，然后选择“添加” > “新建项目”    。 在左侧窗格中，选择“Visual C++ 测试”  。 然后，从中间窗格中选择一个项目类型。 下图显示在安装了“使用 C++ 的桌面开发”  工作负荷时可用的测试项目：

![C++ 测试项目](media/cpp-new-test-project.png)

::: moniker-end

### <a name="create-references-to-other-projects-in-the-solution"></a>创建对解决方案中的其他项目的引用

若要允许访问被测项目中的函数，请在测试项目中添加对项目的引用。 右键单击解决方案资源管理器中的“测试项目”节点  ，调出弹出菜单。 选择“添加” > “引用”   。 在“添加引用”对话框中，选择要测试的项目。

![添加引用](media/cpp-add-ref-test-project.png)

### <a name="link-to-object-or-library-files"></a>将测试与对象或库文件相关联

如果测试代码没有导出要测试的函数，可以将输出的 .obj 或 .lib 文件添加到测试项目的依赖项中。 有关详细信息，请参阅[将测试与对象或库文件相关联](/visualstudio/test/how-to-use-microsoft-test-framework-for-cpp#object_files)。

### <a name="add-include-directives-for-header-files"></a>为头文件添加 #include 指令

接下来，在单元测试 .cpp 文件中，为声明要测试的类型和函数的任何头文件添加 `#include` 指令  。 输入 `#include "`，随后 IntelliSense 会激活以帮助进行选择。 对任何其他头文件重复此操作。

![添加 include 指令](media/cpp-add-includes-test-project.png)

若要避免必须在源文件的每个 include 语句中键入完整路径，可以在“项目”   > “属性”   > “C/C++”   > “常规”   > “附加包含目录”  中添加所需的文件夹。

### <a name="write-test-methods"></a>编写测试方法

> [!NOTE]
> 此部分演示适用于 C/C++ 的 Microsoft 单元测试框架的语法。 记录在此处：[Microsoft.VisualStudio.TestTools.CppUnitTestFramework API reference](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md)。 有关 Google Test 文档，请参阅 [Google Test 入门](https://github.com/google/googletest/blob/master/googletest/docs/primer.md)。 有关 Boost.Test，请参阅 [Boost Test 库：单元测试框架](https://www.boost.org/doc/libs/1_46_0/libs/test/doc/html/utf.html)。

测试项目中的 .cpp 文件有一个为你定义的存根类和方法  。 其中显示了如何编写测试代码的示例。 签名使用 TEST_CLASS 和 TEST_METHOD 宏，它们使方法可在“测试资源管理器”窗口中被发现  。

![添加 include 指令](media/cpp-write-test-methods.png)

TEST_CLASS 和 TEST_METHOD 是 [Microsoft 本机策略框架](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md)的一部分。 “测试资源管理器”  以类似方式发现其他受支持框架中的测试方法。

TEST_METHOD 返回 void。 若要生成测试结果，请使用 `Assert` 类中的静态方法针对预期结果测试实际结果。 在以下示例中，假设 `MyClass` 具有一个采用 `std::string` 的构造函数。 我们可以测试该构造函数是否按预期方式初始化类：

```cpp
TEST_METHOD(TestClassInit)
{
    std::string name = "Bill";
    MyClass mc(name);
    Assert::AreEqual(name, mc.GetName());
}
```

在上面的示例中，`Assert::AreEqual` 调用的结果可确定测试是通过还是失败。 Assert 类包含用于比较预期结果与实际结果的许多其他方法。

可向测试方法添加特征  ，以指定测试所有者、优先级和其他信息。 随后可以使用这些值在“测试资源管理器”  中对测试进行排序和分组。 有关详细信息，请参阅[使用测试资源管理器运行单元测试](run-unit-tests-with-test-explorer.md)。

### <a name="run-the-tests"></a>运行测试

1. 在“测试”  菜单中，依次选择“窗口”   > “测试资源管理器”  。 下图显示其测试尚未运行的测试项目。

   ![运行测试之前的测试资源管理器](media/cpp-test-explorer.png)

   > [!NOTE]
   > CTest 与“测试资源管理器”  的集成尚不可用。 从 CMake 主菜单运行 CTest 测试。

1. 如果部分测试在窗口中不可见，请在解决方案资源管理器中右键单击测试项目的节点并选择“生成”或“重新生成”，生成该测试项目    。

1. 在测试资源管理器中，选择“全部运行”，或选择要运行的特定测试   。 右键单击测试以获得其他选项，包括在启用断点的情况下在调试模式中运行它。 运行所有测试之后，窗口会显示哪些测试通过和哪些测试失败：

![运行测试之后的测试资源管理器](media/cpp-test-explorer-passed.png)

对于失败的测试，该消息会提供有助于诊断原因的详细信息。 右键单击失败的测试，调出弹出菜单。 选择“调试选定的测试”，以单步执行发生故障的函数  。

有关使用“测试资源管理器”  的详细信息，请参阅[使用测试资源管理器运行单元测试](run-unit-tests-with-test-explorer.md)。

有关单元测试的详细信息，请参阅[单元测试基础知识](unit-test-basics.md)

## <a name="use-codelens"></a>使用 CodeLens

**Visual Studio 2017 及更高版本（Professional 和 Enterprise 版）**

通过 [CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md)，无需退出代码编辑器即可快速查看单元测试的状态。

若要为 C++ 单元测试项目初始化 CodeLens，可使用下面的方法之一：

- 编辑和生成测试项目或解决方案。
- 重新生成项目或解决方案。
- 在“测试资源管理器”窗口中运行测试  。

在它初始化后，你便可在各个单元测试上方看到测试状态图标。

![C++ CodeLens 图标](media/cpp-test-codelens-icons.png)

单击图标可以查看详细信息，也可以运行或调试单元测试：

![C++ CodeLens 运行和调试](media/cpp-test-codelens-run-debug.png)

## <a name="see-also"></a>请参阅

- [单元测试代码](unit-test-your-code.md)
