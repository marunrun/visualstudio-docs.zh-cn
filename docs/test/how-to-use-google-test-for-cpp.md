---
title: 如何使用适用于 C++ 的 Google Test
description: 使用 Google Test 在 Visual Studio 中创建 C++ 单元测试。
ms.date: 05/06/2017
ms.topic: conceptual
ms.author: corob
manager: markl
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: 31078b060c94f3253232d22681a1a5dae47e03b6
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77279306"
---
# <a name="how-to-use-google-test-for-c-in-visual-studio"></a>如何在 Visual Studio 中使用适用于 C++ 的 Google Test

在 Visual Studio 2017 及更高版本中，Google Test 作为“使用 C++ 的桌面开发”工作负载的默认组件集成到 Visual Studio IDE 中  。 若要验证是否在计算机上安装了它，请打开 Visual Studio 安装程序，在工作负荷组件列表下找到 Google Test：

![安装 Google Test](media/cpp-google-component.png)

::: moniker range="vs-2019"

## <a name="add-a-google-test-project-in-visual-studio-2019"></a>在 Visual Studio 2019 中添加 Google Test 项目

1. 在“解决方案资源管理器”中，右键单击解决方案节点，然后选择“添加”>“新建项目”    。
2. 将“语言”设置为“C++”并在搜索框中键入“测试”    。 从结果列表中，选择“Google Test 项目”  。
3. 为测试项目提供名称，然后单击“确定”  。

![新建 Google Test 项目](media/vs-2019/cpp-gtest-new-project-vs2019.png)

::: moniker-end

::: moniker range="vs-2017"

## <a name="add-a-google-test-project-in-visual-studio-2017"></a>在 Visual Studio 2017 中添加 Google Test 项目

1. 在“解决方案资源管理器”中，右键单击解决方案节点，然后选择“添加”>“新建项目”    。
2. 在左窗格中，依次选择“Visual C++”>“测试”，然后在中心窗格中选择“Google Test 项目”    。
3. 为测试项目提供名称，然后单击“确定”  。

![新建 Google Test 项目](media/cpp-gtest-new-project.png)

::: moniker-end

## <a name="configure-the-test-project"></a>配置测试项目

在出现的“测试项目配置”  对话框中，可以选择要测试的项目。 选择一个项目时，Visual Studio 会添加对所选项目的引用。 如果你不选择任何项目，则需要手动添加对要测试的项目的引用。 在 Google Test 二进制文件的静态和动态链接之间进行选择时，注意事项与任何 C++ 程序相同。 有关详细信息，请参阅 [Visual C++ 中的 DLL](/cpp/build/dlls-in-visual-cpp)。

![配置 Google Test 项目](media/cpp-gtest-config.png)

## <a name="set-additional-options"></a>设置附加选项

从主菜单中，选择“工具” > “选项” > “Google Test 测试适配器”以设置附加选项    。 有关这些设置的详细信息，请参阅 Google Test 文档。

![Google Test 项目设置](media/cpp-gtest-settings.png)

## <a name="add-include-directives"></a>添加 include 指令

在测试 .cpp 文件中，添加任何所需的 `#include` 指令以使程序的类型和函数对测试代码可见  。 通常，程序在文件夹层次结构中的上一层。 如果键入 `#include "../"`，则会出现一个 IntelliSense 窗口，使你可以选择头文件的完整路径。

![添加 #include 指令](media/cpp-gtest-includes.png)

## <a name="write-and-run-tests"></a>编写和运行测试

现在已准备就绪，可以编写和运行 Google Test。 有关测试宏的信息，请参阅 [Google Test 入门](https://github.com/google/googletest/blob/master/googletest/docs/primer.md)。 有关使用“测试资源管理器”  发现、运行和分组测试的信息，请参阅[使用测试资源管理器运行单元测试](run-unit-tests-with-test-explorer.md)。

## <a name="see-also"></a>请参阅

[编写适用于 C/C++ 的单元测试](writing-unit-tests-for-c-cpp.md)
