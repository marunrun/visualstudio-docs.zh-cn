---
title: 在 Visual Studio 中使用 Clang
ms.date: 10/04/2019
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.clangtidy
author: frozenpandaman
ms.author: efessler
ms.workload:
- cplusplus
ms.openlocfilehash: e226ac6c83839474b9d8ac6be7fb57e376de4a4f
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745983"
---
# <a name="using-clang-tidy-in-visual-studio"></a>在 Visual Studio 中使用 Clang

无论是使用 Clang 还是 MSVC 工具集，代码分析都以本机[方式支持 Clang](https://clang.llvm.org/extra/clang-tidy/)和 CMake 项目。 Clang-整理检查可以作为后台代码分析的一部分运行，以编辑器警告（波形曲线）的形式显示，并显示在错误列表中。

为了使用 Clang，必须通过 Visual Studio 安装程序安装 "C++ Clang Tools for Windows" 组件。

Clang 是使用 LLVM/Clang-cl 工具集时的默认分析工具，可在 MSBuild 和 CMake 中使用。 你可以将其配置为与一起运行，或者在使用 MSVC 工具集时替换标准代码分析体验;如果使用 clang-cl 工具集，Microsoft 代码分析将不可用。

成功编译后，Clang 运行可能需要解决源代码错误，才能获取 Clang 的结果。


## <a name="msbuild"></a>MSBuild

可以将 Clang 配置为作为代码分析的一部分运行，并在项目属性窗口的 "**代码分析**"  >  "**常规**" 页下生成。 用于配置工具的选项可在 "Clang" 子菜单中找到。

有关详细信息，请参阅[如何：设置 C/C++项目的代码分析属性](../code-quality/how-to-set-code-analysis-properties-for-c-cpp-projects.md)。

## <a name="cmake"></a>CMake

在 CMake 项目中，您可以在 `CMakeSettings.json` 中配置 Clang 检查。 打开后，在 "CMake 项目设置" 编辑器的右上角单击 "编辑 JSON"。 识别以下密钥：

- `enableMicrosoftCodeAnalysis`：启用 Microsoft 代码分析
- `enableClangTidyCodeAnalysis`：启用 Clang 分析
- `clangTidyChecks`： Clang 的配置，指定为以逗号分隔的列表，即要启用或禁用的检查

如果未指定任何 "启用" 选项，则 Visual Studio 将选择与所使用的平台工具集匹配的分析工具。

## <a name="warning-display"></a>警告显示

Clang 运行会导致错误列表中显示警告，并在代码相关部分下显示为编辑器内波形曲线。 使用错误列表中的 "Category" 列对 Clang 警告进行排序和组织。 可以通过在 "**工具**"  >  "**选项**" 下切换 "禁用代码分析波形曲线" 设置来配置编辑器内警告。

## <a name="clang-tidy-configuration"></a>Clang 配置

您可以通过 " **Clang 检查**" 选项配置检查 clang 是否在 Visual Studio 中运行。 此输入提供给该工具的 **--检查**参数。 任何进一步的配置都可以包含在**clang 的**文件中。 有关更多详细信息，请参阅[LLVM.org 上的 Clang 文档](https://clang.llvm.org/extra/clang-tidy/)。

## <a name="see-also"></a>请参阅

- [Clang/LLVM 对 MSBuild 项目的支持](https://aka.ms/cpp/clangmsbuild)
- [CMake 项目的 Clang/LLVM 支持](https://aka.ms/cpp/clangcmake)
