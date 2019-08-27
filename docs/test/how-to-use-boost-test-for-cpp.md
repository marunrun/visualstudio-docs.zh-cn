---
title: 如何使用适用于 C++ 的 Boost.Test
description: 使用 Boost.Test 在 Visual Studio 中创建单元测试。
ms.date: 05/06/2019
ms.topic: conceptual
author: mikeblome
ms.author: mblome
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: cf962ec4ecade1bb88d9e301d62eb6ab8a5131cf
ms.sourcegitcommit: 6196d0b7fdcb08ba6d28a8151ad36b8d1139f2cc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2019
ms.locfileid: "65226098"
---
# <a name="how-to-use-boosttest-for-c-in-visual-studio"></a>如何在 Visual Studio 中使用适用于 C++ 的 Boost.Test

在 Visual Studio 2017 及更高版本中，Boost.Test 测试适配器作为“使用 C++ 的桌面开发”工作负载的组件集成到 Visual Studio IDE 中。

![Boost.Test 测试适配器](media/cpp-boost-component.png)

如果没有安装“使用 C++ 的桌面开发”工作负载，则打开“Visual Studio 安装程序”。 选择“使用 C++ 的桌面开发”工作负载，然后选择“修改”按钮。

## <a name="install-boost"></a>安装 Boost

Boost.Test 需要[Boost](http://www.boost.org/)！ 如果未安装 Boost，则建议使用 Vcpkg 程序包管理器。

1. 按照 [Vcpkg：适用于 Windows 的 C++ 包管理器](/cpp/vcpkg)中的说明来安装 vcpkg（如果尚未安装）。

1. 安装 Boost.Test 动态或静态库：

    - 运行 vcpkg install boost-test 以安装 Boost.Test 动态库。

       - 或 -

    - 运行 vcpkg install boost-test:x86-windows-static 以安装 Boost.Test 静态库。

1. 运行 vcpkg integrate install，使用该库以及 Boost 标头和二进制文件的包含路径配置 Visual Studio。

## <a name="add-the-item-template-visual-studio-2017-version-156-and-later"></a>添加项模板（Visual Studio 2017 版本 15.6 及更高版本）

1. 要创建用于测试的 .cpp 文件，右键单击解决方案资源管理器中的项目节点，然后选择“添加新项”。

   ![Boost.Test 项模板](media/boost_test_item_template.png)

1. 新文件包含示例测试方法。 构建项目以启用“测试资源管理器”来发现方法。

项模板使用 Boost.Test 的单标头变量，但是你可以修改 #include 路径来使用独立库变量。 有关详细信息，请参阅[添加 include 指令](#add-include-directives)。

## <a name="create-a-test-project"></a>创建测试项目

在 Visual Studio 2017 版本 15.5 中，没有预配置测试项目或项模板可用于 Boost.Test。 因此，必须创建和配置控制台应用程序项目来存放测试。

1. 在“解决方案资源管理器”中，右键单击解决方案节点，然后选择“添加” > “新建项目”。

1. 在左窗格中，选择“Visual C++” > “Windows 桌面”，然后选择“Windows 控制台应用程序”模板。

1. 为项目提供名称，然后选择“确定”。

1. 删除 .cpp 文件中的 `main` 功能。

1. 如果你使用的是 Boost.Test 的单标头或动态库版本，请转到[添加 include 指令](#add-include-directives)。 如果你使用的是静态库版本，则必须执行一些额外的配置：

   a. 若要编辑项目文件，请先将其卸载。 在解决方案资源管理器中，右键单击项目节点，并选择“卸载项目”。 然后，右键单击项目节点并选择“编辑 < 名称\>.vcxproj”。

   b. 向“全局”属性组添加两行，如下所示：

    ```xml
    <PropertyGroup Label="Globals">
    ....
        <VcpkgTriplet>x86-windows-static</VcpkgTriplet>
        <VcpkgEnabled>true</VcpkgEnabled>
    </PropertyGroup>
    ```

   c. 保存并关闭 \*.vcxproj 文件，然后重载该项目。

   d. 若要打开“属性页”，右键单击项目节点并选择“属性”。

   d. 展开“C/C++” > “代码生成”，然后选择“运行时库”。 为调试静态运行时库选择“/MTd”，为发布静态运行时库选择“/MT”。

   f. 展开“链接器” > “系统”。 验证“子系统”是否设置为“控制台”。

   g. 单击“确定”关闭属性页。

## <a name="add-include-directives"></a>添加 include 指令

1. 在测试 .cpp 文件中，添加任何所需的 `#include` 指令以使程序的类型和函数对测试代码可见。 通常，程序在文件夹层次结构中的上一层。 如果键入 `#include "../"`，则会出现一个 IntelliSense 窗口，使你可以选择头文件的完整路径。

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

下面的示例足以使测试可在“测试资源管理器”中被发现：

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

现已准备就绪，可编写和运行 Boost Test。 有关测试宏的信息，请参阅 [Boost Test 库文档](http://www.boost.org/doc/libs/release/libs/test/doc/html/index.html)。 有关使用“测试资源管理器”发现、运行和分组测试的信息，请参阅[使用测试资源管理器运行单元测试](run-unit-tests-with-test-explorer.md)。

## <a name="see-also"></a>请参阅

- [编写适用于 C/C++ 的单元测试](writing-unit-tests-for-c-cpp.md)
