---
title: 配置用于 IntelliSense 的 C++ 项目
ms.date: 10/08/2018
ms.topic: conceptual
author: corob-msft
ms.author: corob
manager: markl
ms.workload:
- cplusplus
ms.openlocfilehash: 8c43c48a797619f86f81e219e31ccf2afab5ba87
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77279313"
---
# <a name="configure-a-c-project-for-intellisense"></a>配置用于 IntelliSense 的 C++ 项目

在某些情况下，可能需要手动配置 C++ 项目，这样 IntelliSense 才能正常运行。 对于 MSBuild 项目（基于 .vcxproj 文件），可以在项目属性中调整设置。 对于非 MSBuild 项目，可以在项目根目录中的 CppProperties.json 文件内调整设置。 在某些情况下，可能需要创建有助于 IntelliSense 了解宏定义的提示文件。 Visual Studio IDE 有助于发现并修复 IntelliSense 问题。

## <a name="single-file-intellisense"></a>单个文件 IntelliSense

如果你打开项目中没有的文件，Visual Studio 会提供一些 IntelliSense 支持，但默认不会显示任何错误波形曲线。 如果导航栏  显示“杂项文件”  ，这可能就解释了为什么不正确代码下没有显示错误波形曲线，或为什么未定义预处理器宏。

## <a name="check-the-error-list"></a>查看错误列表

如果文件没有以单一文件模式打开，且 IntelliSense 未正常运行，首先要检查的是“错误列表”窗口。 若要查看当前源文件及其包含的所有头文件的全部 IntelliSense 错误，请选择下拉列表中的“生成 + IntelliSense”  ：

![“错误列表”中的 VC++ IntelliSense](media/vcpp-intellisense-error-list.png)

IntelliSense 最多生成 1000 个错误。 如果源文件包含的头文件中的错误超过 1000 个，源文件开头仅显示一条错误波形曲线。

## <a name="ensure-include-paths-are-correct"></a>确保 #include 路径正确无误

### <a name="msbuild-projects"></a>MSBuild 项目

如果在 Visual Studio IDE 外部运行生成，但在生成即将成功时 IntelliSense 不正确，可能是因为命令行与一个或多个配置的项目设置不同步。 右键单击“解决方案资源管理器”  中的项目节点，并确保所有 #include  路径对当前配置和平台都正确无误。 如果路径在所有配置和平台中都完全相同，可选择“所有配置”  和“所有平台”  ，再验证路径是否正确。

![VC++ Include 目录](media/vcpp-intellisense-include-paths.png)

若要查看生成宏（如 VC_IncludePath  ）的当前值，请选择“Include 目录”行，再单击右侧的下拉列表。 然后，选择“\<编辑>”，并单击“宏”按钮。

### <a name="makefile-projects"></a>生成文件项目

对于基于 NMake 项目模板的生成文件项目，依次选择左侧窗格中的“NMake”和“IntelliSense”类别下的“Include 搜索路径”：

![生成文件项目 Include 路径](media/vcpp-intellisense-makefile-include-paths.png)

### <a name="open-folder-projects"></a>打开文件夹项目

对于 CMake 项目，请确保已为 CMakeLists.txt 中的所有配置指定正确的 #include 路径。 其他项目类型可能需要用到 CppProperties.json 文件。 有关详细信息，请参阅[使用 CppProperties.json 配置 IntelliSense](/cpp/build/open-folder-projects-cpp#configure-code-navigation-with-cpppropertiesjson)。 请确保路径对此文件中定义的每个配置都正确无误。

如果 CppProperties.json 文件中有语法错误，那么受影响文件中的 IntelliSense 也会不正确。 Visual Studio 在输出窗口中显示错误。

## <a name="tag-parser-issues"></a>标记分析器问题

标记分析器是“模糊的”C++ 分析器，用于进行浏览和导航。 它的速度非常快，但不会尝试完全理解每个代码构造。

例如，它不会评估预处理器宏，因此可能会错误地分析频繁使用这些宏的代码。 如果标记分析器遇到不熟悉的代码构造，可能会跳过相应的整个代码区域。

此问题通常以下列两种方式在 Visual Studio 中出现：

1. 如果导航栏显示最里面的宏，表明已跳过当前函数定义：

   ![标记分析器跳过函数定义](media/vcpp-intellisense-tag-parser-macro.png)

1. IDE 提议为已定义的函数创建函数定义：

   ![标记分析器提议定义现有函数](media/vcpp-intellisense-tag-parser-function.png)

若要解决上述这几种问题，请将“cpp.hint”  文件添加到解决方案根目录中。 有关详细信息，请参阅[提示文件](/cpp/build/reference/hint-files)。

标记分析器错误显示在“错误列表”窗口中  。

## <a name="validate-project-settings-with-diagnostic-logging"></a>使用诊断日志记录验证项目设置

若要检查 IntelliSense 编译器使用的编译器选项（包括“Include 路径”和“预处理器宏”）是否正确，请依次转到“工具”>“选项”>“文本编辑器”>“C/C++”>“高级”>“诊断日志记录”  ，以启用 IntelliSense 命令行诊断日志记录。 将“启用日志记录”  设置为“True”，将“日志记录级别”  设置为“5”（即最详细），并将“日志记录筛选器”  设置为“8”（即 IntelliSense 日志记录）。

此时，输出窗口会显示传递到 IntelliSense 编译器的命令行。 下面是示例输出：

```output
[IntelliSense] Configuration Name: Debug|Win32
[IntelliSense] Toolset IntelliSense Identifier:
[IntelliSense] command line options:
/c
/I.
/IC:\Repo\Includes
/DWIN32
/DDEBUG
/D_DEBUG
/Zc:wchar_t-
/Zc:forScope
/Yustdafx.h
```

此信息可有助于了解为什么 IntelliSense 会提供不准确的信息。 例如，如果项目的 Include 目录包含 $(MyVariable)\Include  ，而诊断日志却显示 /I\Include  作为 Include 路径，表明 $(MyVariable)  未经评估，已从最终 include 路径中删除。

## <a name="about-the-intellisense-build"></a>关于 IntelliSense 生成

Visual Studio 使用专用 C++ 编译器，创建和维护为所有 IntelliSense 功能提供技术支持的数据库。 为了让 IntelliSense 数据库与代码同步，Visual Studio 会自动启动仅 IntelliSense 生成作为后台任务，以响应项目设置或源文件中的特定更改。

不过，在某些情况下，Visual Studio 可能不会及时更新 IntelliSense 数据库。 例如，当你运行 git pull  或 git checkout  命令时，Visual Studio 可能最多需要一小时，才能检测文件更改。 可强制重新扫描解决方案中的所有文件，具体方法为右键单击“解决方案资源管理器”  中的项目节点，再选择“重新扫描解决方案”  。

## <a name="troubleshooting-intellisense-build-failures"></a>IntelliSense 生成故障疑难解答

IntelliSense 生成即使不生成二进制文件，也仍可能会发生故障。 导致故障发生的一个可能原因是，自定义 .props 或 .targets 文件不正确。 在 Visual Studio 2017 版本 15.6 及更高版本中，仅 IntelliSense 生成错误记录到输出窗口中。 若要查看这些错误，请将“显示的输出来自”  设置为“解决方案”  ：

![解决方案错误输出窗口](media/vcpp-intellisense-output-window.png)

错误消息可能会提示启用设计时跟踪：

```output
error: Designtime build failed for project 'E:\src\MyProject\MyProject.vcxproj',
configuration 'Debug|x64'. IntelliSense might be unavailable.
Set environment variable TRACEDESIGNTIME=true and restart
Visual Studio to investigate.
```

如果你将环境变量 TRACEDESIGNTIME 设置为 true，并重启 Visual Studio，%TEMP% 目录中便会有可能有助于诊断生成故障的日志文件。

若要详细了解 TRACEDESIGNTIME 环境变量，请参阅 [Roslyn](https://github.com/dotnet/roslyn/wiki/Diagnosing-Project-System-Build-Errors) 和[公共项目系统](https://github.com/dotnet/project-system/blob/master/docs/design-time-builds.md)。 这些文章中的信息适用于 C++ 项目。

## <a name="see-also"></a>另请参阅

- [Visual C++ IntelliSense](visual-cpp-intellisense.md)
