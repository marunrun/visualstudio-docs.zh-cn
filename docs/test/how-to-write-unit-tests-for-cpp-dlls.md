---
title: 编写 C++ DLL 单元测试
ms.date: 05/01/2019
ms.topic: conceptual
ms.author: mblome
manager: markl
ms.workload:
- cplusplus
author: mikeblome
ms.openlocfilehash: f9f17b129b0d5d85abacb0723b57703db74bcbea
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68926656"
---
# <a name="write-unit-tests-for-c-dlls-in-visual-studio"></a>在 Visual Studio 中编写 C/C++ DLL 单元测试

测试 DLL 代码有多种方式，具体取决于是否导出要测试的函数。 选择以下方式之一：

**单元测试仅调用从 DLL 导出的函数：** 按照[编写 C/C++ 单元测试](writing-unit-tests-for-c-cpp.md)中所述添加单独的测试项目。 在测试项目中，添加对 DLL 项目的引用。

转到过程[引用从 DLL 项目导出的函数的具体步骤](#projectRef)。

**DLL 生成为 .exe 文件：** 添加单独的测试项目。 将其与输出对象文件关联起来。

转到过程[将测试与对象或库文件相关联的具体步骤](#objectRef)。

**单元测试调用不从 DLL 导出的非成员函数，并且 DLL 可以生成为静态库：** 更改 DLL 项目，以将它编译为 .lib 文件  。 添加引用所测试项目的单独测试项目。

此方法的好处是，允许测试使用非导出成员，但测试仍保留在单独的项目中。

转到过程[将 DLL 更改为静态库的具体步骤](#staticLink)。

**单元测试必须调用不导出的非成员函数，并且代码必须生成为动态链接库 (DLL)：** 在产品代码所在项目中添加单元测试。

转到过程[在同一项目中添加单元测试的具体步骤](#sameProject)。

## <a name="create-the-tests"></a>创建测试

### <a name="staticLink"></a> 将 DLL 更改为静态库的具体步骤

- 如果测试必须使用 DLL 项目不导出的成员，并且所测试项目将生成为动态库，请考虑将其转换为静态库。

  1. 在“解决方案资源管理器”  中，从受测试项目的快捷菜单中选择“属性”  。 此时将打开项目“属性”窗口  。

  2. 选择“配置属性” > “常规”   。

  3. 将“配置类型”  设为“静态库(.lib)”  。

  继续执行过程[将测试与对象或库文件相关联的具体步骤](#objectRef)。

### <a name="projectRef"></a>从测试项目引用导出的 DLL 函数的具体步骤

- 如果 DLL 项目将导出你要测试的函数，则可从测试项目添加对代码项目的引用。

  1. 创建本机单元测试项目。

      ::: moniker range="vs-2019"

      1. 在“文件”菜单上，选择“新建” > “项目”    。 在“添加新项目”对话框中，将“语言”设置为 C++ 并在搜索框中键入“测试”   。 然后，选择“本机测试项目”  。

      ::: moniker-end

      ::: moniker range="vs-2017"

      1. 在“文件”菜单中，选择“新建”>“项目”>“Visual C++”>“测试”>“C++ 单元测试项目”       。

      ::: moniker-end

  1. 在“解决方案资源管理器”中，右键单击测试项目，然后选择“添加” > “引用”    。

  1. 依次选择“项目”  和要测试的项目。

       选择 **“添加”** 按钮。

  1. 在测试项目的属性中，将所测试项目的位置添加到“包含目录”中。

       选择“配置属性” > “VC++ 目录” > “包含目录”    。

       选择“编辑”  ，然后添加受测项目的头目录。

  转到[编写单元测试](#addTests)。

### <a name="objectRef"></a>将测试与对象或库文件相关联的具体步骤

- 如果 DLL 没有导出要测试的函数，可以将输出的 *.obj* 或 *.lib* 文件添加到测试项目的依赖项中。

  1. 创建本机单元测试项目。

      ::: moniker range="vs-2019"

      1. 在“文件”菜单上，选择“新建” > “项目”    。 在“添加新项目”对话框中，将“语言”设置为 C++ 并在搜索框中键入“测试”   。 然后，选择“本机测试项目”  。

      ::: moniker-end

      ::: moniker range="vs-2017"

      1. 在“文件”菜单中，选择“新建”>“项目”>“Visual C++”>“测试”>“C++ 单元测试项目”       。

      ::: moniker-end

  2. 在“解决方案资源管理器”  中，从测试项目的快捷菜单中选择“属性”  。

  3. 选择“配置属性” > “链接器” > “输入” > “附加依赖项”     。

       选择“编辑”  ，然后添加 **.obj** 或 **.lib** 文件名。 请不要使用全路径名。

  4. 选择“配置属性” > “链接器” > “常规” > “附加库目录”     。

       选择“编辑”  ，然后添加 **.obj** 或 **.lib** 文件的目录路径。 该路径一般位于所测试项目的生成文件夹中。

  5. 选择“配置属性” > “VC++ 目录” > “包含目录”    。

       选择“编辑”  ，然后添加受测项目的头目录。

  转到[编写单元测试](#addTests)。

### <a name="sameProject"></a>在同一项目中添加单元测试的具体步骤

1. 修改产品代码项目属性，以包含单元测试所需的标头和库文件。

   1. 在解决方案资源管理器中，从受测项目的快捷菜单上选择“属性”   。 此时将打开项目“属性”窗口  。

   2. 选择“配置属性” > “VC++ 目录”   。

   3. 编辑“包含目录”和“库目录”：

       |目录|Property|
       |-|-|
       |**包含目录** | **$(VCInstallDir)UnitTest\include;$(IncludePath)**|
       |**库目录** | **$(VCInstallDir)UnitTest\lib;$(LibraryPath)**|

2. 添加 C++ 单元测试文件：

   - 在解决方案资源管理器中，从项目的快捷菜单中选择“添加” > “新建项” > “C++ 单元测试”     。

   转到[编写单元测试](#addTests)。

## <a name="addTests"></a> 编写单元测试

1. 在每个单元测试代码文件中，为所测试项目的标头添加 `#include` 语句。

2. 向单元测试代码文件添加测试类和方法。 例如:

    ```cpp
    #include "stdafx.h"
    #include "CppUnitTest.h"
    #include "MyProjectUnderTest.h"
    using namespace Microsoft::VisualStudio::CppUnitTestFramework;
    namespace MyTest
    {
      TEST_CLASS(MyTests)
      {
      public:
          TEST_METHOD(MyTestMethod)
          {
              Assert::AreEqual(MyProject::Multiply(2,3), 6);
          }
      };
    }
    ```

## <a name="run-the-tests"></a>运行测试

1. 在“测试”  菜单中，依次选择“窗口”   > “测试资源管理器”  。

1. 如果窗口中看不见任何测试，则在“解决方案资源管理器”  中右键单击其节点并选择“生成”  或“重新生成”  ，来生成测试项目。

1. 在测试资源管理器中，选择“全部运行”，或选择要运行的特定测试   。 右键单击测试以获得其他选项，包括在启用断点的情况下在调试模式中运行它。

## <a name="see-also"></a>请参阅

- [编写适用于 C/C++ 的单元测试](writing-unit-tests-for-c-cpp.md)
- [Microsoft.VisualStudio.TestTools.CppUnitTestFramework API 参考](../test/microsoft-visualstudio-testtools-cppunittestframework-api-reference.md)
- [调试本机代码](../debugger/debugging-native-code.md)
- [演练：创建和使用动态链接库 (C++)](/cpp/build/walkthrough-creating-and-using-a-dynamic-link-library-cpp)
- [导入和导出](/cpp/build/importing-and-exporting)
- [快速入门：通过测试资源管理器进行测试驱动开发](../test/quick-start-test-driven-development-with-test-explorer.md)
