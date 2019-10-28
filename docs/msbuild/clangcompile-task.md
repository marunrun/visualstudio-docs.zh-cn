---
title: ClangCompile 任务 | Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.clangcompile
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), ClangCompile task
- ClangCompile task (MSBuild (C++))
author: mikeblome
ms.author: mblome
ms.workload:
- multiple
ms.openlocfilehash: 1bd1d749461c423d51e0f5b736563a9f9aa757c5
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747344"
---
# <a name="clangcompile-task"></a>ClangCompile 任务

包装 Microsof C++ 编译器工具 (clang.exe)。

## <a name="parameters"></a>参数

下表介绍了  ClangCompile 任务的参数。

|参数|说明|
|---------------|-----------------|
|**AdditionalIncludeDirectories**|可选的 string[]  参数。<br/><br/>指定一个或多个要添加到包含路径中的目录；存在多个目录时，请用分号分隔。<br/><br/>请使用 `-I[path]`。|
|**AdditionalOptions**|可选的 string  参数。|
|**BufferSecurityCheck**|可选的 string  参数。<br/><br/>安全检查有助于检查堆栈缓冲区是否超负荷运行，它是一种常见的尝试攻击程序安全的命令。 <br/><br/>请使用 `fstack-protector`。|
|**BuildingInIde**|可选的 bool  参数。|
|**CLanguageStandard**|可选的 string  参数。<br/><br/>确定 C 语言标准。<br/><br/>将 `std=[value]` 与 c89、  c99  、c11、  gnu99  或 gnu11  的值搭配使用。|
|**ClangVersion**|可选的 string  参数。|
|**CompileAs**|可选的 string  参数。<br/><br/>选择 .c 和 .cpp 文件的编译语言选项。 默认将基于 .c 或 .cpp 扩展名进行检测。<br/><br/>使用 `-x c`、`-x c++`。|
|**CppLanguageStandard**|可选的 string  参数。<br/><br/>确定 C++ 语言标准。<br/><br/>将 `std=[value]` 与 c++98  、c++11  、c++1y  gnu++98  、gnu++11  或 gnu++1y 的值搭配使用  。|
|**DataLevelLinking**|可选的 bool  参数。<br/><br/>启用链接器优化，通过在一个独立的分区中发出每个数据项来删除未使用的数据。|
|**DebugInformationFormat**|可选的 string  参数。<br/><br/>指定编译器生成的调试信息的类型。<br/><br/>**None**，不生成任何调试信息，编译更加快速（使用 `g0`）。<br/>**FullDebug**，生成 DWARF2 调试信息。（使用 `g2 -gdwarf-2`）。<br/>**LineNumber**，仅生成行号信息（使用 `gline-tables-only`）。|
|**EnableNeonCodegen**|可选的 bool  参数。<br/><br/>针对 NEON 浮点硬件启用代码生成。 仅适用于 ARM 架构。|
|**ExceptionHandling**|可选的 string  参数。<br/><br/>指定将由编译器使用的异常处理模型。<br/><br/>**Disabled**，禁用异常处理（使用 `fno-exceptions`）。<br/>**Enabled**，启用异常处理（使用 `fexceptions`）。<br/>**UnwindTables**，生成任何所需的静态数据，但不会影响生成的代码（使用 `funwind-tables`）。|
|**FloatABI**|可选的 string  参数。<br/><br/>选择浮点 ABI 选项。<br/><br/>**soft**，可使编译器生成包含浮点运算库调用的输出（使用 `mfloat-abi=soft`）。<br/>**softfp**，允许使用硬件浮点指令生成代码，但仍然使用软浮点调用约定（使用 `mfloat-abi=softfp`）。<br/>**hard**，允许生成浮点指令，并使用 FPU 专用调用约定（使用 `mfloat-abi=hard`）。|
|**ForcedIncludeFiles**|可选的 string[]  参数。<br/><br/>一个或多个强制包含文件。<br/><br/>请使用 `-include [name]`。|
|**FunctionLevelLinking**|可选的 bool  参数。<br/><br/>允许编译器以打包函数 (COMDAT) 形式对各个函数进行打包。 需进行此操作后才能编辑并继续工作。<br/><br/>请使用 `ffunction-sections`。|
|**GccToolChain**|可选的 string  参数。<br/><br/>Gcc 工具链的文件夹路径。|
|**GNUMode**|可选的 bool  参数。<br/><br/>|
|**MSCompatibility**|可选的 bool  参数。<br/><br/>启用 Microsoft C++ 完全兼容性。|
|**MSCompatibilityVersion**|可选的 string  参数。<br/><br/>句点分隔的值，表示要在 _MSC_VER 中报告的 Microsoft 编译器版本号（0 = 不定义（默认））。|
|**MSExtensions**|可选的 bool  参数。<br/><br/>接受 Microsoft 编译器支持的一些非标准构造。|
|**MSCompilerVersion**|可选的 string  参数。<br/><br/>要在 _MSC_VER 中报告的 Microsoft 编译器版本号（0 = 不定义（默认））。|
|**MSVCErrorReport**|可选的 bool  参数。<br/><br/>报告 Visual Studio 可用于分析文件和行信息的错误。|
|**ObjectFileName**|可选的 string  参数。<br/><br/>指定一个名称以替代默认对象文件名；可以是文件或目录名。<br/><br/>请使用 `/Fo[name]`。|
|**OmitFramePointers**|可选的 bool  参数。<br/><br/>禁止在调用堆栈上创建帧指针。|
|**优化**|可选的 string  参数。<br/><br/>指定应用程序的优化级别。<br/><br/>**Custom**，自定义优化。<br/>**Disabled**，禁用优化（使用 `O0`）。<br/>**MinSize**，针对大小进行优化（使用 `Os`）。<br/>**MaxSpeed**，针对速度进行优化（使用 `O2`）。<br/>**Full**，成本高昂的优化（使用 `O3`）。|
|**PositionIndependentCode**|可选的 bool  参数。<br/><br/>生成位置无关代码 (PIC) 以便在共享库中使用。|
|**PrecompiledHeader**|可选的 string  参数。<br/><br/>在生成期间启用创建或使用预编译标头。|
|**PrecompiledHeaderFile**|可选的 string  参数。<br/><br/>指定用于预编译标头文件的标头文件名。 此文件也会在生成期间被添加到“强制包含文件”  。|
|**PrecompiledHeaderOutputFileDirectory**|可选的 string  参数。<br/><br/>指定生成的预编译标头的目录。 此目录也会在生成期间被添加到“附加包含目录”  。|
|**PrecompiledHeaderCompileAs**|可选的 string  参数。<br/><br/>选择预编译标头文件的编译语言选项。<br/><br/>使用 `-x c-header`、`-x c++-header`。|
|**PreprocessorDefinitions**|可选的 string[]  参数。<br/><br/>定义源文件的预处理符号。<br/><br/>请使用 `-D`。|
|**RuntimeLibrary**|可选的 string  参数。<br/><br/>指定运行时库以进行链接。<br/><br/>使用 `MSVC /MT`、`/MTd`、`/MD`、`/MDd` 开关。<br/><br/>**MultiThreaded**，使应用程序使用多线程静态版本运行时库。<br/>**MultiThreadedDebug**，定义 _DEBUG 和 _MT。 此选项还会让编译器将库名称 LIBCMTD.lib 放置到 .obj 文件中，以便链接器将使用 LIBCMTD.lib 来解析外部符号。<br/>**MultiThreadedDLL**，使应用程序使用特定于多线程和 DLL 的运行时库版本。 定义 _MT 和 _DLL，并使编译器将库名 MSVCRT.lib 放入 .obj 文件中。<br/>**MultiThreadedDebugDLL**，定义 _DEBUG、_MT 和 _DLL，并使应用程序使用特定于调试多线程和 DLL 的运行时库版本。 它还会让编译器将库名称 MSVCRTD.lib 放入 .obj 文件中。|
|**RuntimeTypeInfo**|可选的 bool  参数。<br/><br/>添加在运行时检查 C++ 对象类型（运行时类型信息）的代码。<br/><br/>使用 `frtti`、`fno-rtti`。|
|**ShowIncludes**|可选的 bool  参数。<br/><br/>生成包含文件的列表及编译器输出。<br/><br/>请使用 `-H`。|
|**Sources**|必需的 **ITaskItem[]** 参数。|
|**StrictAliasing**|可选的 bool  参数。<br/><br/>假设使用最严格的别名规则。 一种类型的对象将始终不会被假定驻留在与另一种类型的对象相同的位置。|
|**Sysroot**|可选的 string  参数。<br/><br/>标头和库的根目录的文件夹路径。|
|**TargetArch**|可选的 string  参数。<br/><br/>目标体系结构。|
|**ThumbMode**|可选的 string  参数。<br/><br/>生成执行 Thumb 微架构的代码。 仅适用于 ARM 架构。<br/><br/>**Thumb**，生成 Thumb 代码（使用 `mthumb`）。<br/>**ARM**，生成 Arm 代码（使用 `marm`）。<br/>**Disabled**，此选项不适用于所选平台。|
|**TrackerLogDirectory**|可选的 string  参数。<br/><br/>跟踪器日志目录。|
|**TreatWarningAsError**|可选的 bool  参数。<br/><br/>将所有编译器警告视为错误。<br/><br/>对于新项目，最好在所有编译中使用 `/WX`；对所有警告进行解析可确保将可能难以发现的代码缺陷减至最少。|
|**UndefinePreprocessorDefinitions**|可选的 string[]  参数。<br/><br/>指定取消定义一个或多个预处理器。<br/><br/>请使用 `-U [macro]`。|
|**UndefineAllPreprocessorDefinitions**|可选的 bool  参数。<br/><br/>取消以前定义的所有预处理器值。<br/><br/>请使用 `-undef`。|
|**UseMultiToolTask**|可选的 bool  参数。<br/><br/>多处理器编译。|
|**UseShortEnums**|可选的 bool  参数。<br/><br/>枚举类型仅用作可能值的输入集需要的字节数。|
|**Verbose**|可选的 bool  参数。<br/><br/>显示要运行的命令，并使用详细输出。|
|**WarningLevel**|可选的 string  参数。<br/><br/>选择编译器对代码错误的严格程度。 其他标记应直接添加到附加选项  （使用 `/w`、`/Weverything`）。<br/><br/>**TurnOffAllWarnings**，禁用所有编译器警告（使用 `w`）。<br/>**EnableAllWarnings**，启用所有警告，包括默认情况下禁用的那些警告（使用 `Wall`）。|

## <a name="see-also"></a>请参阅

[任务参考](../msbuild/msbuild-task-reference.md)