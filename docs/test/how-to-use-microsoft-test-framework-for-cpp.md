---
title: 使用适用于 C++ 的 Microsoft 单元测试框架
description: 使用适用于 C++ 的 Microsoft 单元测试框架为 C++ 代码创建单元测试。
ms.date: 01/08/2020
ms.topic: how-to
ms.author: corob
manager: markl
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: a9393fd248f4e6520c261d405bc624a75d8cf69f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287111"
---
# <a name="use-the-microsoft-unit-testing-framework-for-c-in-visual-studio"></a>在 Visual Studio 中使用适用于 C++ 的 Microsoft Unit Testing 框架

默认情况下，适用于 C++ 的 Microsoft 单元测试框架包含在“使用 C++ 的桌面开发”工作负荷中。

## <a name="to-write-unit-tests-in-a-separate-project"></a><a name="separate_project"></a> 在单独的项目中编写单元测试

通常，你在测试代码自己的项目（与要测试的代码处于相同解决方案中）中运行测试代码。 若要设置和配置新测试项目，请参阅[编写 C/C++ 单元测试](writing-unit-tests-for-c-cpp.md)。

## <a name="to-write-unit-tests-in-the-same-project"></a><a name="same_project"></a>在同一项目中编写单元测试

在某些情况下，例如测试 DLL 中的非导出函数时，可能需要在所测试程序所处的同一项目中创建测试。 在同一项目中编写单元测试：

1. 修改项目属性，以包含单元测试所需的标头和库文件。

   1. 在解决方案资源管理器中，从要测试的项目的快捷菜单中选择“属性”。 此时将打开项目属性窗口。

   1. 在“属性页”对话框中，选择“配置属性” > “VC++ 目录” 。

   1. 单击以下行中的向下箭头，然后选择 \<Edit>。 添加这些路径：

      | 目录 | Property |
      |-| - |
      | **包含目录** | $(VCInstallDir)Auxiliary\VS\UnitTest\include |
      | **库目录** | $(VCInstallDir)Auxiliary\VS\UnitTest\lib |

1. 添加 C++ 单元测试文件：

   - 右键单击解决方案资源管理器中的项目节点，然后选择“添加” > “新建项” > “C++ 文件(.cpp)”   。

## <a name="to-link-the-tests-to-the-object-or-library-files"></a><a name="object_files"></a>将测试与对象或库文件相关联的具体步骤

如果受测代码没有导出要测试的函数，可以将输出的 .obj 或 .lib 文件添加到测试项目的依赖项中 。 修改测试项目的属性，以包含单元测试所需的标头和库或对象文件。

1. 在“解决方案资源管理器”中，从测试项目的快捷菜单中选择“属性”。 此时将打开项目属性窗口。

1. 选择“配置属性” > “链接器” > “输入”页，然后选择“附加依赖项”   。

   选择“编辑”，然后添加 **.obj** 或 **.lib** 文件名。 请勿使用完整路径名称。

1. 选择“配置属性” > “链接器” > “常规”页，然后选择“附加库目录”   。

   选择“编辑”，然后添加 **.obj** 或 **.lib** 文件的目录路径。 该路径一般位于所测试项目的生成文件夹中。

1. 选择“配置属性” > “VC++ 目录”页，然后选择“包含目录”  。

   选择“编辑”，然后添加受测项目的头目录。

## <a name="write-the-tests"></a>编写测试

包含测试类的任何 .cpp 文件都必须包含“CppUnitTest.h”，并具有用于 `using namespace Microsoft::VisualStudio::CppUnitTestFramework` 的 using 语句。 测试项目已为你进行了配置。 它还包含命名空间定义以及带有 TEST_METHOD 的 TEST_CLASS 来帮助你上手。 可修改命名空间名称，以及类和方法宏中带圆括号的名称。

测试框架定义了特殊宏，用于初始化测试模块、类和方法，以及在测试完成后清理资源。 这些宏生成代码，用于在首次访问类或方法之前，以及在最后一个测试运行之后执行。 有关详细信息，请参阅[初始化和清理](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md#Initialize_and_cleanup)。

在 [Assert](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md#general_asserts) 类中使用静态方法定义测试条件。 使用 [Logger](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md#logger) 类将消息写入到**输出窗口**。 将属性添加到测试方法

## <a name="run-the-tests"></a>运行测试

1. 在“测试”菜单中，依次选择“窗口” > “测试资源管理器”。

1. 如果部分测试在窗口中不可见，请在解决方案资源管理器中右键单击测试项目的节点并选择“生成”或“重新生成”，生成该测试项目  。

1. 在测试资源管理器中，选择“全部运行”，或选择要运行的特定测试 。 右键单击测试以获得其他选项，包括在启用断点的情况下在调试模式中运行它。

1. 在“输出窗口”中，从下拉菜单中选择“测试”以查看 `Logger` 类写出的消息 ：

   ![显示测试消息的 C++ 输出窗口](media/cpp-test-output-window.png)

## <a name="define-traits-to-enable-grouping"></a>定义特征以实现分组

可对测试方法定义特征，这样就能在测试资源管理器中对测试进行分类和分组。 若要定义特性，请使用 `TEST_METHOD_ATTRIBUTE` 宏。 例如，若要定义名为 `TEST_MY_TRAIT`的特性：

```cpp
#define TEST_MY_TRAIT(traitValue) TEST_METHOD_ATTRIBUTE(L"MyTrait", traitValue)
```

在单元测试中使用已定义的特征：

```cpp
BEGIN_TEST_METHOD_ATTRIBUTE(Method1)
    TEST_OWNER(L"OwnerName")
    TEST_PRIORITY(1)
    TEST_MY_TRAIT(L"thisTraitValue")
END_TEST_METHOD_ATTRIBUTE()

TEST_METHOD(Method1)
{
    Logger::WriteMessage("In Method1");
    Assert::AreEqual(0, 0);
}
```

### <a name="c-trait-attribute-macros"></a>C++ 特征特性宏

以下预定义特征位于 `CppUnitTest.h` 中。 有关详细信息，请参阅[适用于 C++ API 参考的 Microsoft 单元测试框架](microsoft-visualstudio-testtools-cppunittestframework-api-reference.md)。

|宏|描述|
|-|-----------------|
|`TEST_METHOD_ATTRIBUTE(attributeName, attributeValue)`|使用 TEST_METHOD_ATTRIBUTE 宏定义特性。|
|`TEST_OWNER(ownerAlias)`|使用预定义的“所有者”特征来指定测试方法的所有者。|
|`TEST_PRIORITY(priority)`|使用预定义的“优先级”特征向测试方法分配相对优先级。|

## <a name="see-also"></a>请参阅

- [快速入门：通过测试资源管理器进行测试驱动开发](../test/quick-start-test-driven-development-with-test-explorer.md)
