---
title: CL 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- VC.Project.VCCLCompilerTool.UseUnicodeForAssemblerListing
- vc.task.cl
- VC.Project.VCCLCompilerTool.TreatSpecificWarningsAsErrors
- VC.Project.VCCLCompilerTool.CreateHotpatchableImage
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild (Visual C++), CL task
- CL task (MSBuild (Visual C++))
ms.assetid: 651ba971-b755-4f03-a549-4816beb3cc0d
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8307bc2c9efcbbab531754cd2d49fa18b04cc48a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65698640"
---
# <a name="cl-task"></a>CL 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包装 Visual C++ 编译器工具 cl.exe。 编译器生成可执行 (.exe) 文件、动态链接库 (.dll) 文件或者代码模块 (.netmodule) 文件。 有关详细信息，请参阅[编译器选项](https://msdn.microsoft.com/library/ed3376c8-bef4-4c9a-80e9-3b5da232644c)。  
  
## <a name="parameters"></a>参数  
 下表描述了 **CL** 任务的参数。 大多数任务参数和若干组参数都对应于命令行选项。  
  
- **AdditionalIncludeDirectories**  
  
   可选 String[] 参数。  
  
   将目录添加到在其中搜索包含文件的目录列表中。  
  
   有关详细信息，请参阅 [/I（附加包含目录）](https://msdn.microsoft.com/library/3e9add2a-5ed8-4d15-ad79-5b411e313a49)。  
  
- **AdditionalOptions**  
  
   可选 String 参数。  
  
   命令行选项列表。 例如，“/*option1* /*option2* /*option#*”。 使用此参数可指定未由任何其他任务参数表示的命令行选项。  
  
   有关详细信息，请参阅[编译器选项](https://msdn.microsoft.com/library/ed3376c8-bef4-4c9a-80e9-3b5da232644c)。  
  
- AdditionalUsingDirectories 可选 String[] 参数。  
  
   指定在解析传递给 **#using** 指令的文件引用时编译器将搜索的目录。  
  
   有关详细信息，请参阅 [/AI（指定元数据目录）](https://msdn.microsoft.com/library/fb9c1846-504c-4a3b-bb39-c8696de32f6f)。  
  
- **AlwaysAppend**  
  
   可选 String 参数。  
  
   一个始终在命令行上发出的字符串。 其默认值为“**/c**”。  
  
- **AssemblerListingLocation**  
  
   创建包含程序集代码的列表文件。  
  
   有关详细信息，请参阅 [/FA、/Fa（列表文件）](https://msdn.microsoft.com/library/c7507d0e-c69d-44f9-b8e2-d2c398697402)中的 **/Fa** 选项。  
  
- **AssemblerOutput**  
  
   可选 String 参数。  
  
   创建包含程序集代码的列表文件。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **NoListing** - *\<none>*  
  
  - **AssemblyCode** - **/FA**  
  
  - **AssemblyAndMachineCode** - **/FAc**  
  
  - **AssemblyAndSourceCode** - **/FAs**  
  
  - **All** - **/FAcs**  
  
    有关详细信息，请参阅 [/FA、/Fa（列表文件）](https://msdn.microsoft.com/library/c7507d0e-c69d-44f9-b8e2-d2c398697402)中的 **/FA**、**/FAc**、**/FAs** 和 **/FAcs** 选项。  
  
- **BasicRuntimeChecks**  
  
   可选 String 参数。  
  
   结合 [runtime_checks](https://msdn.microsoft.com/library/ae50b43f-f88d-47ad-a2db-3389e9e7df5b) 杂注，启用和禁用运行时错误检查功能。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **Default** -                          *\<none>*  
  
  - **StackFrameRuntimeCheck** - **/RTCs**  
  
  - **UninitializedLocalUsageCheck** - **/RTCu**  
  
  - **EnableFastChecks** -                          **/RTC1**  
  
    有关详细信息，请参阅 [/RTC（运行时错误检查）](https://msdn.microsoft.com/library/9702c558-412c-4004-acd5-80761f589368)。  
  
- **BrowseInformation**  
  
   可选的布尔参数。  
  
   如果为 `true`，则创建浏览信息文件。  
  
   有关详细信息，请参阅 [/FR、/Fr（创建 .Sbr 文件）](https://msdn.microsoft.com/library/3fd8f88b-3924-4feb-9393-287036a28896)中的 **/FR** 选项。  
  
- **BrowseInformationFile**  
  
   可选 String 参数。  
  
   指定浏览信息文件的文件名称。  
  
   有关详细信息，请参阅此表中的 **BrowseInformation** 参数，同时还请参阅 [/FR、/Fr （创建 .Sbr 文件）](https://msdn.microsoft.com/library/3fd8f88b-3924-4feb-9393-287036a28896)。  
  
- **BufferSecurityCheck**  
  
   可选的布尔参数。  
  
   如果为 `true`，则检测覆盖返回地址的某些缓冲区溢出，这是一种开发不强制执行缓冲区大小限制的代码的常见技术。  
  
   有关详细信息，请参阅 [/GS（缓冲区安全检查）](https://msdn.microsoft.com/library/8d8a5ea1-cd5e-42e1-bc36-66e1cd7e731e)。  
  
- **BuildingInIDE**  
  
   可选的布尔参数。  
  
   如果为 `true`，则指示 **MSBuild** 由 IDE 调用。 否则，在命令行上调用 **MSBuild**。  
  
- **CallingConvention**  
  
   可选 String 参数。  
  
   指定用于确定函数参数推送到堆栈中的顺序（由调用方函数还是被调用的函数从调用末端的堆栈移除参数）的调用约定，以及编译器用来标识各个函数的名称修饰约定。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **Cdecl** - **/Gd**  
  
  - **FastCall** -                          **/Gr**  
  
  - **StdCall** -                          **/Gz**  
  
    有关详细信息，请参阅 [/Gd、/Gr、/Gv、/Gz（调用约定）](https://msdn.microsoft.com/library/fd3110cb-2d77-49f2-99cf-a03f9ead00a3)。  
  
- **CompileAs**  
  
   可选 String 参数。  
  
   指定是否将输入文件编译为 C 或 C++ 源文件。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **Default** - *\<none>*  
  
  - **CompileAsC** - **/TC**  
  
  - **CompileAsCpp** - **/TP**  
  
    有关详细信息，请参阅 [/Tc、/Tp、/TC、/TP（指定源文件类型）](https://msdn.microsoft.com/library/7d9d0a65-338b-427c-8b48-fff30e2f9d2b)。  
  
- **CompileAsManaged**  
  
   可选 String 参数。  
  
   允许应用程序和组件使用公共语言运行时 (CLR) 中的功能。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **false** - *\<none>*  
  
  - **true** - **/clr**  
  
  - **Pure** - **/clr:pure**  
  
  - **Safe** - **/clr:safe**  
  
  - **OldSyntax** - **/clr:oldSyntax**  
  
    有关详细信息，请参阅 [/clr（公共语言运行时编译）](https://msdn.microsoft.com/library/fec5a8c0-40ec-484c-a213-8dec918c1d6c)。  
  
- **CreateHotpatchableImage**  
  
   可选的布尔参数。  
  
   如果为 `true`，则告知编译器准备用于*热修补*的映像。 此参数确保每个函数的第一个指令为两个字节，这是进行热修补所要求的。  
  
   有关详细信息，请参阅 [/hotpatch（创建可热修补的映像）](https://msdn.microsoft.com/library/aad539b6-c053-4c78-8682-853d98327798)。  
  
- **DebugInformationFormat**  
  
   可选 String 参数。  
  
   选择为程序创建的调试信息的类型，并选择是将此信息保存在对象 (.obj) 文件中，还是保存在程序数据库 (PDB) 中。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **OldStyle** - **/Z7**  
  
  - **ProgramDatabase** - **/Zi**  
  
  - **EditAndContinue** - **/ZI**  
  
    有关详细信息，请参阅 [/Z7、/Zi、/ZI（调试信息格式）](https://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8)。  
  
- **DisableLanguageExtensions**  
  
   可选的布尔参数。  
  
   如果为 **true**，则告知编译器发出不与 ANSI C 或 ANSI C++ 兼容的语言构造错误。  
  
   有关详细信息，请参阅 [/Za、/Ze（禁用语言扩展）](https://msdn.microsoft.com/library/65e49258-7161-4289-a176-7c5c0656b1a2)的 **/Za** 选项。  
  
- **DisableSpecificWarnings**  
  
   可选 String[] 参数。  
  
   禁用在以分号分隔的列表中指定的警告编号。  
  
   有关详细信息，请参阅 [/w、/W0、/W1、/W2、/W3、/W4、/w1、/w2、/w3、/w4、/Wall、/wd、/we、/wo、/Wv、/WX（警告等级）](https://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f)中的 `/wd` 选项。  
  
- **EnableEnhancedInstructionSet**  
  
   可选 String 参数。  
  
   指定使用流式处理 SIMD 扩展 (SSE) 和流式处理 SIMD 扩展 2 (SSE2) 指令的代码生成体系结构。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **StreamingSIMDExtensions** - **/arch:SSE**  
  
  - **StreamingSIMDExtensions2** - **/arch:SSE2**  
  
    有关详细信息，请参阅 [/arch (x86)](https://msdn.microsoft.com/library/9dd5a75d-06e4-4674-aade-33228486078d)。  
  
- **EnableFiberSafeOptimizations**  
  
   可选的布尔参数。  
  
   如果为 `true`，则支持使用静态线程本地存储分配的数据（也就是使用 `__declspec(thread)` 分配的数据）的纤程安全。  
  
   有关详细信息，请参阅 [/GT （支持纤程安全线程本地存储）](https://msdn.microsoft.com/library/071fec79-c701-432b-9970-457344133159)。  
  
- **EnablePREfast**  
  
   可选的布尔参数。  
  
   如果为 `true`，则启用代码分析。  
  
   有关详细信息，请参阅 [/analyze（代码分析）](https://msdn.microsoft.com/library/81da536a-e030-4bd4-be18-383927597d08)。  
  
- **ErrorReporting**  
  
   可选 String 参数。  
  
   允许你直接向 Microsoft 提供内部编译器错误 (ICE) 信息。 默认情况下，IDE 生成中的设置是“提示”，命令行生成中的设置是“队列”。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **None** - **/errorReport:none**  
  
  - **Prompt** - **/errorReport:prompt**  
  
  - **Queue** - **/errorReport:queue**  
  
  - **Send** - **/errorReport:send**  
  
    有关详细信息，请参阅 [/errorReport（报告内部编译器错误）](https://msdn.microsoft.com/library/819828f8-b0a5-412c-9c57-bf822f17e667)。  
  
- **ExceptionHandling**  
  
   可选 String 参数。  
  
   指定将由编译器使用的异常处理模型。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **false** - *\<none>*  
  
  - **Async** - **/EHa**  
  
  - **Sync** - **/EHsc**  
  
  - **SyncCThrow** - **/EHs**  
  
    有关详细信息，请参阅 [/EH（异常处理模型）](https://msdn.microsoft.com/library/754b916f-d206-4472-b55a-b6f1b0f2cb4d)。  
  
- **ExpandAttributedSource**  
  
   可选的布尔参数。  
  
   如果为 `true`，则创建将扩展的属性插入到源文件中的列表文件。  
  
   有关详细信息，请参阅 [/Fx （合并插入的代码）](https://msdn.microsoft.com/library/14f0e301-3bab-45a3-bbdf-e7ce66f20560)。  
  
- **FavorSizeOrSpeed**  
  
   可选 String 参数。  
  
   指定代码大小优先还是代码速度优先。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **Neither** - *\<none>*  
  
  - **Size** - **/Os**  
  
  - **Speed** - **/Ot**  
  
    有关详细信息，请参阅 [/Os、/Ot（代码大小优先、代码速度优先）](https://msdn.microsoft.com/library/9a340806-fa15-4308-892c-355d83cac0f2)。  
  
- **FloatingPointExceptions**  
  
   可选的布尔参数。  
  
   如果为 `true`，则启用可靠的浮点异常模型。 异常将在触发后立即引发。  
  
   有关详细信息，请参阅 [/fp（指定浮点行为）](https://msdn.microsoft.com/library/10469d6b-e68b-4268-8075-d073f4f5d57e)中的 /**fp:except** 选项。  
  
- **FloatingPointModel**  
  
   可选 String 参数。  
  
   设置浮点模型。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **Precise** - **/fp:precise**  
  
  - **Strict** - **/fp:strict**  
  
  - **Fast** - **/fp:fast**  
  
    有关详细信息，请参阅 [/fp（指定浮点行为）](https://msdn.microsoft.com/library/10469d6b-e68b-4268-8075-d073f4f5d57e)。  
  
- **ForceConformanceInForLoopScope**  
  
   可选的布尔参数。  
  
   如果为 `true`，则在使用 Microsoft 扩展 ([/Ze](https://msdn.microsoft.com/library/65e49258-7161-4289-a176-7c5c0656b1a2)) 的 [for](https://msdn.microsoft.com/library/6c7d01b3-c4c1-4c6a-aa58-e2d198f33d4a) 循环中实现标准 C++ 行为。  
  
   有关详细信息，请参阅 [/Zc:forScope（强制执行 For 循环范围中的合规性）](https://msdn.microsoft.com/library/3031f02d-3b14-4ad0-869e-22b0110c3aed)。  
  
- **ForcedIncludeFiles**  
  
   可选 `String[]` 参数。  
  
   促使预处理器处理一个或多个指定的头文件。  
  
   有关详细信息，请参阅 [/FI（命名强制包含文件）](https://msdn.microsoft.com/library/07e79577-8152-4df9-a64c-aae08c603397)。  
  
- **ForcedUsingFiles**  
  
   可选 **String []** 参数。  
  
   促使预处理器处理一个或多个指定的 **#using** 文件。  
  
   有关详细信息，请参阅 [/FU（命名强制 #using 文件）](https://msdn.microsoft.com/library/698f8603-457f-435a-baff-5ac9243d6ca1)。  
  
- **FunctionLevelLinking**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则允许编译器以打包函数 (COMDAT) 形式对各个函数进行打包。  
  
   有关详细信息，请参阅 [/Gy （启用函数级链接）](https://msdn.microsoft.com/library/0d3cf14c-ed7d-4ad3-b4b6-104e56f61046)。  
  
- **GenerateXMLDocumentationFiles**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则促使编译器处理源代码文件中的文档注释，并为每个包含文档注释的源代码文件创建 .xdc 文件。  
  
   有关详细信息，请参阅 [/doc（处理文档注释）(C/C++)](https://msdn.microsoft.com/library/b54f7e2c-f28f-4f46-9ed6-0db09be2cc63)。 另请参阅此表中的 **XMLDocumentationFileName** 参数。  
  
- **IgnoreStandardIncludePath**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则禁止编译器在 PATH 和 INCLUDE 环境变量指定的目录中搜索包含文件。  
  
   有关详细信息，请参阅 [/X （忽略标准包含路径）](https://msdn.microsoft.com/library/16bdf2cc-c8dc-46e4-bdcc-f3caeba5e1ef)。  
  
- **InlineFunctionExpansion**  
  
   可选 **String** 参数。  
  
   指定生成的内联函数扩展级别。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **Default** - *\<none>*  
  
  - **Disabled** - **/Ob0**  
  
  - **OnlyExplicitInline** - **/Ob1**  
  
  - **AnySuitable** - **/Ob2**  
  
    有关详细信息，请参阅 [/Ob（内联函数扩展）](https://msdn.microsoft.com/library/f134e6df-e939-4980-a01d-47425dbc562a)。  
  
- **IntrinsicFunctions**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则将某些函数调用替换为内部函数或有助于提高应用程序运行速度的其他特殊形式函数。  
  
   有关详细信息，请参阅 [/Oi （生成内部函数）](https://msdn.microsoft.com/library/fa4a3bf6-0ed8-481b-91c0-add7636132b4)。  
  
- **MinimalRebuild**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则启用最小重新生成，它确定是否必须重新编译包含已更改的 C++ 类定义的 C++ 源文件，该定义存储在标头 (.h) 文件中。  
  
   有关详细信息，请参阅 [/Gm（启用最小重新生成）](https://msdn.microsoft.com/library/d8869ce0-d2ea-40eb-8dae-6d2cdb61dd59) 。  
  
- **MultiProcessorCompilation**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则使用多个处理器进行编译。 此参数在计算机上为每个有效的处理器创建进程。  
  
   有关详细信息，请参阅 [/MP（使用多个进程生成）](https://msdn.microsoft.com/library/a932b14a-74fe-4b45-84e4-6bf53f0f5e07)。 另请参阅此表格中的 **ProcessorNumber** 参数。  
  
- **ObjectFileName**  
  
   可选 **String** 参数。  
  
   指定对象 (.obj) 文件的名称或要使用的目录，而不是默认目录。  
  
   有关详细信息，请参阅 [/Fo（对象文件名）](https://msdn.microsoft.com/library/0e6d593e-4e7f-4990-9e6e-92e1dcbcf6e6)。  
  
- **ObjectFiles**  
  
   可选 **String []** 参数。  
  
   对象文件的列表。  
  
- **OmitDefaultLibName**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则省略对象 (.obj) 文件中的默认 C 运行时库名称。 默认情况下，编译器将库的名称放入 .obj 文件中以将链接器定向到正确的库。  
  
   有关详细信息，请参阅 [/Zl（省略默认库名）](https://msdn.microsoft.com/library/b27d39d0-44d6-498c-84ae-27c1326fee59)。  
  
- **OmitFramePointers**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则禁止在调用堆栈上创建帧指针。  
  
   有关详细信息，请参阅 [/Oy （框架指针省略）](https://msdn.microsoft.com/library/c451da86-5297-4c5a-92bc-561d41379853)。  
  
- **OpenMPSupport**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则促使编译器处理 OpenMP 子句和指令。  
  
   有关详细信息，请参阅 [/openmp（启用 OpenMP 2.0 支持）](https://msdn.microsoft.com/library/9082b175-18d3-4378-86a7-c0eb95664e13)。  
  
- **优化**  
  
   可选 **String** 参数。  
  
   指定各种代码优化的速度和大小。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **Disabled** - **/Od**  
  
  - **MinSpace** - **/O1**  
  
  - **MaxSpeed** - **/O2**  
  
  - **Full** - **/Ox**  
  
    有关详细信息，请参阅 [/O 选项（优化代码）](https://msdn.microsoft.com/library/77997af9-5555-4b3d-aa57-6615b27d4d5d)。  
  
- **PrecompiledHeader**  
  
   可选 **String** 参数。  
  
   在生成期间创建或使用预编译标头 (.pch) 文件。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **NotUsing** - *\<none>*  
  
  - **Create** - **/Yc**  
  
  - **Use** - **/Yu**  
  
    有关详细信息，请参阅 [/Yc （创建预编译头文件）](https://msdn.microsoft.com/library/47c2e555-b4f5-46e6-906e-ab5cf21f0678)和 [/Yu（使用预编译头文件）](https://msdn.microsoft.com/library/24f1bd0e-b624-4296-a17e-d4b53e374e1f)。 另外，请参阅此表中的 **PrecompiledHeaderFile** 和 **PrecompiledHeaderOutputFile** 参数。  
  
- **PrecompiledHeaderFile**  
  
   可选 **String** 参数。  
  
   指定要创建或使用的预编译头文件名。  
  
   有关详细信息，请参阅 [/Yc （创建预编译头文件）](https://msdn.microsoft.com/library/47c2e555-b4f5-46e6-906e-ab5cf21f0678)和 [/Yu（使用预编译头文件）](https://msdn.microsoft.com/library/24f1bd0e-b624-4296-a17e-d4b53e374e1f)。  
  
- **PrecompiledHeaderOutputFile**  
  
   可选 **String** 参数。  
  
   指定预编译标头的路径名称，而不是使用默认路径名称。  
  
   有关详细信息，请参阅 [/Fp（命名 .Pch 文件）](https://msdn.microsoft.com/library/0fcd9cbd-e09f-44d3-9715-b41efb5d0be2)。  
  
- **PreprocessKeepComments**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则在预处理期间保留注释。  
  
   有关详细信息，请参阅 [/C（在预处理期间保留注释）](https://msdn.microsoft.com/library/944567ca-16bc-4728-befe-d414a7787f26)。  
  
- **PreprocessorDefinitions**  
  
   可选 `String[]` 参数。  
  
   定义源文件的预处理符号。  
  
   有关详细信息，请参阅 [/D (Preprocessor Definitions)](https://msdn.microsoft.com/library/b53fdda7-8da1-474f-8811-ba7cdcc66dba)。  
  
- **PreprocessOutput**  
  
   可选 `ITaskItem[]` 参数。  
  
   定义可以由任务使用和发出的预处理器输出项的数组。  
  
- **PreprocessOutputPath**  
  
   可选 `String` 参数。  
  
   指定 **PreprocessToFile** 参数将预处理输出写入其中的输出文件的名称。  
  
   有关详细信息，请参阅 [/Fi（预处理输出文件名）](https://msdn.microsoft.com/library/6d0ba983-a8b7-41ec-84f5-b4688ef8efee)。  
  
- **PreprocessSuppressLineNumbers**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则预处理 C 和 C++ 源文件，并将预处理过的文件复制到标准输出设备。  
  
   有关详细信息，请参阅 [/EP（不使用 #line 指令预处理到 stdout）](https://msdn.microsoft.com/library/6ec411ae-e33d-4ef5-956e-0054635eabea)。  
  
- **PreprocessToFile**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则预处理 C 和 C++ 源文件，并将预处理的输出写入文件。  
  
   有关详细信息，请参阅 [/P（预处理到文件）](https://msdn.microsoft.com/library/123ee54f-8219-4a6f-9876-4227023d83fc)。  
  
- **ProcessorNumber**  
  
   可选 `Integer` 参数。  
  
   指定在多处理器编译中使用的处理器的最大数目。 将此参数与 **MultiProcessorCompilation** 参数结合使用。  
  
- **ProgramDataBaseFileName**  
  
   可选 `String` 参数。  
  
   指定程序数据库 (PDB) 文件的文件名。  
  
   有关详细信息，请参阅 [/Fd（程序数据库文件名）](https://msdn.microsoft.com/library/3977a9ed-f0ac-45df-bf06-01cedd2ba85a)。  
  
- **RuntimeLibrary**  
  
   可选 `String` 参数。  
  
   指示多线程模块是否为 DLL，并选择运行时库的零售版本或调试版本。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **MultiThreaded** - **/MT**  
  
  - **MultiThreadedDebug** - **/MTd**  
  
  - **MultiThreadedDLL** - **/MD**  
  
  - **MultiThreadedDebugDLL** - **/MDd**  
  
    有关详细信息，请参阅 [/MD、/MT、/LD（使用运行时库）](https://msdn.microsoft.com/library/cf7ed652-dc3a-49b3-aab9-ad60e5395579)。  
  
- **RuntimeTypeInfo**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，添加在运行时检查 C++ 对象类型（运行时类型信息）的代码。  
  
   有关详细信息，请参阅 [/GR（启用运行时类型信息）](https://msdn.microsoft.com/library/d1f9f850-dcec-49fd-96ef-e72d01148906)。  
  
- **ShowIncludes**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则促使编译器输出包含文件的列表。  
  
   有关详细信息，请参阅 [/showIncludes（列出包含文件）](https://msdn.microsoft.com/library/0b74b052-f594-45a6-a7c7-09e1a319547d)。  
  
- **SmallerTypeCheck**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则在某个值分配给较小的数据类型且导致数据丢失时，报告运行时错误。  
  
   有关详细信息，请参阅 [/RTC（运行时错误检查）](https://msdn.microsoft.com/library/9702c558-412c-4004-acd5-80761f589368)中的 **/RTCc** 选项。  
  
- **Sources**  
  
   必选 `ITaskItem[]` 参数。  
  
   指定用空格分隔的源文件列表。  
  
- **StringPooling**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则编译器能够在程序映像中创建相同字符串的一个副本。  
  
   有关详细信息，请参阅 [/GF（消除重复字符串）](https://msdn.microsoft.com/library/bb7b5d1c-8e1f-453b-9298-8fcebf37d16c)。  
  
- **StructMemberAlignment**  
  
   可选 `String` 参数。  
  
   指定结构中所有成员的字节对齐方式。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **Default** - **/Zp1**  
  
  - **1Byte** - **/Zp1**  
  
  - **2Bytes** - **/Zp2**  
  
  - **4Bytes** - **/Zp4**  
  
  - **8Bytes** - **/Zp8**  
  
  - **16Bytes** - **/Zp16**  
  
    有关详细信息，请参阅 [/Zp（结构成员对齐）](https://msdn.microsoft.com/library/5242f656-ed9b-48a3-bc73-cfcf3ed2520f)。  
  
- **SuppressStartupBanner**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则在任务开始时阻止显示版权和版本号消息。  
  
   有关详细信息，请参阅 [/nologo（取消显示启动版权标志）(C/C++)](https://msdn.microsoft.com/library/75930d8b-b11c-4db8-99e5-b52f97da0693)。  
  
- **TrackerLogDirectory**  
  
   可选 `String` 参数。  
  
   指定存储此任务跟踪日志的中间目录。  
  
   有关详细信息，请参阅此表中的 **TLogReadFiles** 和 **TLogWriteFiles** 参数。  
  
- **TreatSpecificWarningsAsErrors**  
  
   可选 **String []** 参数。  
  
   将编译器警告的指定列表视为错误。  
  
   有关详细信息，请参阅 [/w、/W0、/W1、/W2、/W3、/W4、/w1、/w2、/w3、/w4、/Wall、/wd、/we、/wo、/Wv、/WX（警告等级）](https://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f)中的 **/we**`n` 选项。  
  
- **TreatWarningAsError**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则将所有编译器警告视为错误。  
  
   有关详细信息，请参阅 [/w、/W0、/W1、/W2、/W3、/W4、/w1、/w2、/w3、/w4、/Wall、/wd、/we、/wo、/Wv、/WX（警告等级）](https://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f)中的 **/WX** 选项。  
  
- **TreatWChar_tAsBuiltInType**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则将 `wchar_t` 类型视为本机类型。  
  
   有关详细信息，请参阅 [/Zc:wchar_t（wchar_t 是本机类型）](https://msdn.microsoft.com/library/b0de5a84-da72-4e5a-9a4e-541099f939e0)。  
  
- **UndefineAllPreprocessorDefinitions**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则取消定义编译器定义的特定于 Microsoft 的符号。  
  
   有关详细信息，请参阅 [/U、/u（未定义符号）](https://msdn.microsoft.com/library/7bc0474f-6d1f-419b-807d-0d8816763b2a)中的 **/u** 选项。  
  
- **UndefinePreprocessorDefinitions**  
  
   可选 `String[]` 参数。  
  
   指定一个或多个要取消定义的预处理器符号的列表。  
  
   有关详细信息，请参阅 [/U、/u（未定义符号）](https://msdn.microsoft.com/library/7bc0474f-6d1f-419b-807d-0d8816763b2a)中的 **/U** 选项。  
  
- **UseFullPaths**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则在诊断中显示传递给编译器的源代码文件的完整路径。  
  
   有关详细信息，请参阅 [/FC（所诊断源代码文件的完整路径）](https://msdn.microsoft.com/library/1f11414e-cb42-421b-be68-9d369aab036b)。  
  
- **UseUnicodeForAssemblerListing**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则指示使用 UTF-8 格式创建输出文件。  
  
   有关详细信息，请参阅 [/FA、/Fa（列表文件）](https://msdn.microsoft.com/library/c7507d0e-c69d-44f9-b8e2-d2c398697402)中的 **/FAu** 选项。  
  
- **WarningLevel**  
  
   可选 `String` 参数。  
  
   指定编译器生成的警告的最高等级。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **TurnOffAllWarnings** - **/W0**  
  
  - **Level1** - **/W1**  
  
  - **Level2** - **/W2**  
  
  - **Level3** - **/W3**  
  
  - **Level4** - **/W4**  
  
  - **EnableAllWarnings** - **/Wall**  
  
    有关详细信息，请参阅 [/w、/W0、/W1、/W2、/W3、/W4、/w1、/w2、/w3、/w4、/Wall、/wd、/we、/wo、/Wv、/WX（警告等级）](https://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f)中的 **/W**_n_ 选项。  
  
- **WholeProgramOptimization**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则启用全程序优化。  
  
   有关详细信息，请参阅 [/GL（全程序优化）](https://msdn.microsoft.com/library/09d51e2d-9728-4bd0-b5dc-3b8284aca1d1)。  
  
- **XMLDocumentationFileName**  
  
   可选 `String` 参数。  
  
   指定所生成的 XML 文档文件的名称。 此参数可以是文件，也可以是目录名。  
  
   有关详细信息，请参阅 [/doc（处理文档注释）(C/C++)](https://msdn.microsoft.com/library/b54f7e2c-f28f-4f46-9ed6-0db09be2cc63) 中的 `name` 参数。 另请参阅此表中的 **GenerateXMLDocumentationFiles** 参数。  
  
- **MinimalRebuildFromTracking**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则执行跟踪的增量生成；如果为 `false`，则执行重新生成。  
  
- **TLogReadFiles**  
  
   可选 `ITaskItem[]` 参数。  
  
   指定表示*读取文件跟踪日志*的项的数组。  
  
   读取文件跟踪日志 (.tlog) 包含由任务读取的输入文件的名称，并由项目生成系统来使用以支持增量生成。 有关详细信息，请参阅此表中的 **TrackerLogDirectory** 和 **TrackFileAccess** 参数。  
  
- **TLogWriteFiles**  
  
   可选 `ITaskItem[]` 参数。  
  
   指定表示*写入文件跟踪日志*的项的数组。  
  
   写入文件跟踪日志 (.tlog) 包含由任务写入的输出文件的名称，并由项目生成系统来使用以支持增量生成。 有关详细信息，请参阅此表中的 **TrackerLogDirectory** 和 **TrackFileAccess** 参数。  
  
- **TrackFileAccess**  
  
   可选 `Boolean` 参数。  
  
   如果为 `true`，则跟踪文件访问模式。  
  
   有关详细信息，请参阅此表中的 **TLogReadFiles** 和 **TLogWriteFiles** 参数。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [任务参考](../msbuild/msbuild-task-reference.md)
