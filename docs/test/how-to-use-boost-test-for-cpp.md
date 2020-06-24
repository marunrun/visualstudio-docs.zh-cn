---
title: 如何使用适用于 C++ 的 Boost.Test
description: 使用 Boost.Test 在 Visual Studio 中创建单元测试。
ms.date: 01/29/2020
ms.topic: how-to
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 34c593469a586d1314c7ee52f3aeb3ab6faf334c
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287267"
---
# <a name="how-to-use-boosttest-for-c-in-visual-studio"></a>如何在 Visual Studio 中使用适用于 C++ 的 Boost.Test

在 Visual Studio 2017 及更高版本中，Boost.Test 测试适配器集成到 Visual Studio IDE 中。 它是“使用 C++ 的桌面开发”  工作负载的组件。

![Boost.Test 测试适配器](media/cpp-boost-component.png)

如果没有安装“使用 C++ 的桌面开发”工作负载，则打开“Visual Studio 安装程序”   。 选择“使用 C++ 的桌面开发”  工作负载，然后选择“修改”  按钮。

## <a name="install-boost"></a>安装 Boost

Boost.Test 需要[Boost](https://www.boost.org/)！ 如果未安装 Boost，则建议使用 Vcpkg 包管理器。

1. 按照 [Vcpkg：适用于 Windows 的 C++ 包管理器](/cpp/vcpkg)中的说明来安装 vcpkg（如果尚未安装）。

1. 安装 Boost.Test 动态或静态库：

    - 运行 `vcpkg install boost-test` 以安装 Boost.Test 动态库。

       \- 或 -

    - 运行 `vcpkg install boost-test:x86-windows-static` 以安装 Boost.Test 静态库。

1. 运行 `vcpkg integrate install`，使用该库以及 Boost 标头和二进制文件的包含路径配置 Visual Studio。

可以选择如何在 Visual Studio 的解决方案中配置测试：可以将测试代码包含在要测试的项目中，也可以为测试创建一个单独的测试项目。 这两种选择都有优缺点。

## <a name="add-tests-inside-your-project"></a>在项目内添加测试

在 Visual Studio 2017 版本 15.6 及更高版本中，可以将用于测试的项模板添加到项目中。 测试和代码位于同一项目中。 必须创建一个单独的生成配置才能生成测试版本。 而且，需要将测试排除在调试和发布版本之外。

在 Visual Studio 2017 版本 15.5 中，没有预配置测试项目或项模板可用于 Boost.Test。 按照说明创建和配置单独的测试项目。

### <a name="create-a-boosttest-item"></a>创建 Boost.Test 项

1. 若要创建用于测试的 .cpp 文件，请右键单击解决方案资源管理器中的项目节点，然后选择“添加” > “新项”     。

1. 在“添加新项”对话框中，展开“已安装” > “Visual C++” > “测试”     。 选择 Boost.Test，然后选择“添加”以将 Test.cpp 添加到项目中    。

   ![Boost.Test 项模板](media/boost_test_item_template.png)

新 Test.cpp 文件包含示例测试方法  。 可以在此文件中包含自己的头文件，并为应用编写测试。

测试文件还使用宏为测试配置定义新 `main` 例程。 如果现在生成项目，则会出现 LNK2005 错误，如“_main already defined in main.obj.”

### <a name="create-and-update-build-configurations"></a>创建和更新生成配置

1. 若要创建测试配置，请在菜单栏上选择“生成” > “配置管理器”   。 在“配置管理器”对话框中，打开“活动解决方案配置”下的下拉列表，然后选择“新建”    。 在“新建解决方案配置”对话框中，输入一个名称，如“Debug Run-unittests”  。 在“复制设置”中，选择“调试”，然后选择“确定”    。

1. 从调试和发布配置中排除测试代码：在“解决方案资源管理器”中，右键单击 Test.cpp 然后选择“属性”   。 在“属性页”对话框中，选择“配置”下拉列表中的“所有配置”    。 选择“配置属性” > “常规”，然后打开“从生成中排除”属性的下拉列表    。 选择“是”，然后选择“应用”以保存所做的更改   。

1. 若要将测试代码包含在 Debug UnitTests 配置中，请在“属性页”对话框中，选择“配置”下拉列表中的“Debug UnitTests”    。 在“从生成中排除”属性中选择“否”，然后选择“确定”以保存更改    。

1. 从 Debug UnitTests 配置中排除主代码。 在“解决方案资源管理器”中，右键单击包含 `main` 函数的文件，然后选择“属性”   。 在“属性页”对话框中，选择“配置”下拉列表中的“Debug UnitTests”    。 选择“配置属性” > “常规”，然后打开“从生成中排除”属性的下拉列表    。 选择“是”，然后选择“确定”以保存所做的更改   。

1. 将解决方案配置设置为 Debug Run-unittests，然后生成项目以启用“测试资源管理器”来发现方法   。

只要你创建的配置名称以“Debug”或“Release”字样开头，系统会自动选取相应的 Boost.Test 库。

项模板使用 Boost.Test 的单标头变量，但是你可以修改 #include 路径来使用独立库变量。 有关详细信息，请参阅[添加 include 指令](#add-include-directives)。

## <a name="create-a-separate-test-project"></a>创建单独的测试项目

在许多情况下，使用单独的项目进行测试会更加容易。 无需为项目创建特殊的测试配置。 或从调试和发布版本中排除测试文件。

### <a name="to-create-a-separate-test-project"></a>创建单独的测试项目

1. 在“解决方案资源管理器”中，右键单击解决方案节点，然后选择“添加” > “新建项目”    。

1. 在“添加新项目”对话框中，选择筛选器下拉列表中的“C++”、“Windows”和“控制台”     。 选择“控制台应用”模板，然后选择“下一步”   。

1. 为项目提供名称，然后选择“创建”  。

1. 删除 .cpp 文件中的 `main` 功能  。

1. 如果你使用的是 Boost.Test 的单标头或动态库版本，请转到[添加 include 指令](#add-include-directives)。 如果你使用的是静态库版本，则必须执行一些额外的配置：

   a. 若要编辑项目文件，请先将其卸载。 在解决方案资源管理器中，右键单击项目节点，并选择“卸载项目”   。 然后，右键单击项目节点并选择“编辑 < 名称\>.vcxproj”  。

   b. 向“全局”属性组添加两行，如下所示： 

    ```xml
    <PropertyGroup Label="Globals">
    ....
        <VcpkgTriplet>x86-windows-static</VcpkgTriplet>
        <VcpkgEnabled>true</VcpkgEnabled>
    </PropertyGroup>
    ```

   c. 保存并关闭 \*.vcxproj 文件，然后重载该项目  。

   d. 若要打开“属性页”  ，右键单击项目节点并选择“属性”  。

   e. 展开“C/C++”   > “代码生成”  ，然后选择“运行时库”  。 为调试静态运行时库选择“/MTd”  ，为发布静态运行时库选择“/MT”  。

   f. 展开“链接器” > “系统”   。 验证“子系统”是否设置为“控制台”   。

   g. 单击“确定”关闭属性页  。

## <a name="add-include-directives"></a>添加 include 指令

1. 在测试 .cpp 文件中，添加任何所需的 `#include` 指令以使程序的类型和函数对测试代码可见  。 如果使用的是单独的测试项目，则该程序通常位于文件夹层次结构中的一个同级层次。 如果键入 `#include "../"`，则会出现一个 IntelliSense 窗口，使你可以选择头文件的完整路径。

   ![添加 #include 指令](media/cpp-gtest-includes.png)

   可以将独立库用于：

   ```cpp
   #include <boost/test/unit_test.hpp>
   ```

   或将单标头版本用于：

   ```cpp
   #include <boost/test/included/unit_test.hpp>
   ```

   然后，定义 `BOOST_TEST_MODULE`。

下面的示例足以使测试可在“测试资源管理器”  中被发现：

```cpp
#define BOOST_TEST_MODULE MyTest
#include <boost/test/included/unit_test.hpp\> //single-header
#include "../MyProgram/MyClass.h" // project being tested
#include <string>

BOOST_AUTO_TEST_CASE(my_boost_test)
{
    std::string expected_value = "Bill";

    // assume MyClass is defined in MyClass.h
    // and get_value() has public accessibility
    MyClass mc;
    BOOST_CHECK(expected_value == mc.get_value());
}
```

## <a name="write-and-run-tests"></a>编写和运行测试

现已准备就绪，可编写和运行 Boost Test。 有关测试宏的信息，请参阅 [Boost Test 库文档](https://www.boost.org/doc/libs/1_71_0/libs/test/doc/html/index.html)。 有关使用“测试资源管理器”  发现、运行和分组测试的信息，请参阅[使用测试资源管理器运行单元测试](run-unit-tests-with-test-explorer.md)。

## <a name="see-also"></a>请参阅

- [编写适用于 C/C++ 的单元测试](writing-unit-tests-for-c-cpp.md)
