---
title: Clang 项目属性 (Android C++) | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 663140ea-a568-472b-a79a-dfea8818e06a
author: corob
ms.author: mblome
manager: jillfra
f1_keywords:
- VC.Project.VCClangCompilerTool.AdditionalIncludeDirectories
- VC.Project.VCClangCompilerTool.DebugInformationFormat
- VC.Project.VCClangCompilerTool.ObjectFile
- VC.Project.VCClangCompilerTool.WarningLevel
- VC.Project.VCClangCompilerTool.WarnAsError
- VC.Project.VCClangCompilerTool.Verbose
- VC.Project.VCClangCompilerTool.Optimization
- VC.Project.VCClangCompilerTool.StrictAliasing
- VC.Project.VCClangCompilerTool.OmitFramePointers
- VC.Project.VCClangCompilerTool.ExceptionHandling
- VC.Project.VCClangCompilerTool.EnableFunctionLevelLinking
- VC.Project.VCClangCompilerTool.DataLevelLinking
- VC.Project.VCClangCompilerTool.DataLevelLinking
- VC.Project.VCClangCompilerTool.FloatABI
- VC.Project.VCClangCompilerTool.BufferSecurityCheck
- VC.Project.VCClangCompilerTool.PIC
- VC.Project.VCClangCompilerTool.UseShortEnums
- VC.Project.VCClangCompilerTool.RuntimeTypeInfo
- VC.Project.VCClangCompilerTool.CLanguageStandard
- VC.Project.VCClangCompilerTool.CppLanguageStandard
- VC.Project.VCClangCompilerTool.PreprocessorDefinitions
- VC.Project.VCClangCompilerTool.UndefinePreprocessorDefinitions
- VC.Project.VCClangCompilerTool.UndefineAllPreprocessorDefinitions
- VC.Project.VCClangCompilerTool.ShowIncludes
- VC.Project.VCClangCompilerTool.PrecompiledHeader
- VC.Project.VCClangCompilerTool.PrecompiledHeaderFile
- VC.Project.VCClangCompilerTool.PrecompiledHeaderOutputFileDirectory
- VC.Project.VCClangCompilerTool.PrecompiledHeaderCompileAs
- VC.Project.VCClangCompilerTool.CompileAs
- VC.Project.VCClangCompilerTool.ForcedIncludeFiles
- VC.Project.VCClangCompilerTool.MultiProcessorCompilation
- vc.project.AdditionalOptionsPage
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: 055ec15deed2e5071c50d9903779d00030e07b02
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62819911"
---
# <a name="clang-project-properties-android-c"></a>Clang 项目属性 (Android C++)

Property | 说明 | 选项
--- | ---| ---
附加包含目录 | 指定一个或多个要添加到包含路径中的目录；存在多个目录时，请用分号分隔。 (-I[path])。
调试信息格式 | 指定编译器生成的调试信息的类型。 | 无 - 没有生成调试信息，因此编译可能会更快。<br>完全调试信息 (DWARF2) - 生成了 DWARF2 调试信息。<br>行号信息 - 仅生成行号信息。<br>
对象文件名 | 指定一个名称以替代默认对象文件名；可以是文件或目录名。 (/Fo[name])。
警告级别 | 选择编译器对代码错误的严格程度。  其他标志应直接添加到附加选项。 （/w、/Weverything）。 | 关闭所有警告 - 禁用所有编译器警告。<br>启用所有警告 - 启用所有警告，包括默认情况下禁用的那些警告。<br>
将警告视为错误 | 将所有编译器警告视为错误。 对于新项目，最好在所有编译中使用 /WX；对所有警告进行解析可确保将可能难以发现的代码缺陷减至最少。
启用详细模式 | 显示要运行的命令，并使用详细输出。
优化 | 指定应用程序的优化级别。 | 自定义 - 自定义优化。<br>禁用 - 禁用优化。<br>使大小最小化 - 优化尺寸。<br>使速度最大化 - 优化速度。<br>完全优化 - 成本高昂的优化。<br>
严格别名 | 假设使用最严格的别名规则。  一种类型的对象将始终不会被假定驻留在与另一种类型的对象相同的位置。
省略框架指针 | 禁止在调用堆栈上创建帧指针。
启用 C++ 异常 | 指定将由编译器使用的异常处理模型。 | 否 - 禁用异常处理。<br>是 - 启用异常处理。<br>展开表 - 生成任何所需的静态数据，但不会影响生成的代码。<br>
启用函数级别链接 | 允许编译器以打包函数 (COMDAT) 形式对各个函数进行打包。 需进行此操作后才能编辑并继续工作。     (ffunction-sections)。
启用数据级别链接 | 启用链接器优化，通过在一个独立的分区中发出每个数据项来删除未使用的数据。
启用高级 SIMD (Neon) | 针对 NEON 浮点硬件启用代码生成。 仅适用于 ARM 架构。
浮点 ABI | 选择浮点 ABI 选项。 | Soft -“Soft”可使编译器生成包含浮点运算库调用的输出。<br>SoftFP -“SoftFP”允许使用硬件浮点指令生成代码，但仍然使用软浮点调用约定。<br>**Hard** - 使用“Hard”，可以生成浮点指令，并使用 FPU 专用调用约定。<br>
安全检查 | 安全检查有助于检查堆栈缓冲区是否超负荷运行，它是一种常见的尝试攻击程序安全的命令。 (fstack-protector)。 | 禁用安全检查 - 禁用安全检查。<br>启用安全检查 - 启用安全检查。 (fstack-protector)<br>
位置无关代码 | 生成位置无关代码 (PIC) 以便在共享库中使用。
使用短枚举 | 枚举类型仅用作可能值的输入集需要的字节数。
启用运行时类型信息 | 添加在运行时检查 C++ 对象类型（运行时类型信息）的代码。     （frtti、fno-rtti）
C 语言标准 | 确定 C 语言标准。 | **默认**<br>C89 - C89 语言标准。<br>C99 - C99 语言标准。<br>C11 - C11 语言标准。<br>C99 (GNU Dialect) - C99 (GNU Dialect) 语言标准。<br>C11 (GNU Dialect) - C11 (GNU Dialect) 语言标准。<br>
C++ 语言标准 | 确定 C++ 语言标准。 | **默认**<br>C++03 - C++03 语言标准。<br>C++11 - C++11 语言标准。<br>C++14 - C++14 语言标准。<br>C++03 (GNU Dialect) - C++03 (GNU Dialect) 语言标准。<br>C++11 (GNU Dialect) - C++11 (GNU Dialect) 语言标准。<br>C++14 (GNU Dialect) - C++14 (GNU Dialect) 语言标准。<br>
预处理器定义 | 定义源文件的预处理符号。 (-D)
取消定义预处理器定义 | 指定取消定义一个或多个预处理器。  (-U [macro])
取消所有预处理器定义 | 取消以前定义的所有预处理器值。  (-undef)
显示包含文件 | 生成包含文件的列表及编译器输出。  (-H)
预编译头 | 创建/使用预编译标头：在生成期间启用创建或使用预编译标头。 | 使用 - 使用预编译标头。<br>不使用预编译标头 - 不使用预编译标头。<br>
预编译标头文件 | 指定用于预编译标头文件的标头文件名。 此文件也会在生成期间被添加到“强制包含文件”
预编译标头输出文件目录 | 指定生成的预编译标头的目录。 此目录也会在生成期间被添加到“附加包含目录”
将预编译标头编译为 | 选择预编译标头文件的编译语言选项（-x c-header、-x c++-header）。 | 编译为 C 代码 - 编译为 C 代码。<br>编译为 C++ 代码 - 编译为 C++ 代码。<br>
编译为 | 选择 .c 和 .cpp 文件的编译语言选项。  “默认”将根据 .c 或 .cpp 扩展名执行检测。 （-x c、-x c++） | 默认 - 默认代码。<br>编译为 C 代码 - 编译为 C 代码。<br>编译为 C++ 代码 - 编译为 C++ 代码。<br>
强制包含文件 | 一个或多个强制包含文件。     (-include [名称])
多处理器编译 | 多处理器编译。
附加选项 | 附加选项。
