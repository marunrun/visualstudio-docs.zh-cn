---
title: 如何使用适用于 C++ 的 CTest
ms.date: 01/23/2020
ms.topic: conceptual
ms.author: corob
manager: jillfra
ms.workload:
- cplusplus
author: corob-msft
ms.openlocfilehash: 78759a017575916bce3b3fff643cbce8ff303fd6
ms.sourcegitcommit: 8cbced0fb46959a3a2494852df1e41db1177a26c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76826518"
---
# <a name="how-to-use-ctest-for-c-in-visual-studio-2017-and-later"></a>如何在 Visual Studio 2017 及更高版本中使用适用于 C++ 的 CTest

默认情况下，CMake（包括 CTest）作为“使用 C++ 的桌面开发”工作负载的组件集成到 Visual Studio IDE 中  。 如果需要将其安装在计算机上，请打开 Visual Studio 安装程序计划，单击“使用 C++ 的桌面开发”按钮，然后单击“修改”   。 检查工作负载组件列表下的适用于 Windows 的 C++ CMake 工具  。

## <a name="to-write-tests"></a>编写测试

Visual Studio 中的 CMake 支持不涉及 Visual Studio 项目系统。 因此，可如同在任何 CMake 环境中一样编写和配置 CTest 测试。 使用 `enable_testing()` 命令启用测试，并使用 `add_test()` 或 `gtest_discover_tests()` 命令添加新测试。 若要了解有关 CTest 的详细信息，请参阅 [CMake 文档](https://gitlab.kitware.com/cmake/community/wikis/doc/ctest/Testing-With-CTest)。 

有关在 Visual Studio 中使用 CMake 的详细信息，请参阅 [Visual C++ 中的 CMake 项目](/cpp/build/cmake-projects-in-visual-studio)。

## <a name="to-run-tests"></a>运行测试

CTest 与“测试资源管理器”完全集成，同时支持 Google 和 Boost 单元测试框架  。 默认情况下，这些框架作为组件包含在“使用 C++ 的桌面开发”工作负载中  。 但是，如果你要从较旧版本的 Visual Studio 升级项目，可能需要通过使用 Visual Studio 安装程序来安装这些框架。

下图显示使用 Google Test 框架的 CTest 运行结果：

![在 Visual Studio 中使用 Google Test Framework 进行 CTest](media/ctest-test-explorer.png)

如果使用的是 CTest 而不是 Google 或 Boost 适配器，你将看到 CTest 级别而非单个测试方法级别的结果。 可以调试并单步调试仅限 CTest 的可执行文件，但不支持单个测试上的堆栈跟踪。

## <a name="see-also"></a>请参阅

- [编写适用于 C/C++ 的单元测试](writing-unit-tests-for-c-cpp.md)
