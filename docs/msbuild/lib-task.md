---
title: LIB 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VC.Project.VCLibrarianTool.Name
- VC.Project.VCLibrarianTool.TreatLibWarningsAsErrors
- VC.Project.VCLibrarianTool.Verbose
- vc.task.lib
- VC.Project.VCLibrarianTool.ErrorReporting
- VC.Project.VCLibrarianTool.LinkLibraryDependencies
- VC.Project.VCLibrarianTool.LinkTimeCodeGeneration
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), LIB task
- LIB task (MSBuild (C++))
ms.assetid: e062c7f9-cc69-4a83-9361-1bb5355e5fe8
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a5794d059a17f39531a7788895b604ae0e9590ce
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633585"
---
# <a name="lib-task"></a>LIB 任务

包装 Microsoft 32 位库管理器工具 (lib.exe)  。 库管理器创建并管理通用对象文件格式 (COFF) 对象文件的库。 库管理器还可以创建导出文件和导入库，以便引用导出的定义。 有关详细信息，请参阅 [LIB 参考](/cpp/build/reference/lib-reference)和[运行 LIB](/cpp/build/reference/running-lib)。

## <a name="parameters"></a>参数

 下表介绍了 **LIB** 任务的参数。 大多数任务参数都对应于命令行选项。

|参数|说明|
|---------------|-----------------|
|**AdditionalDependencies**|可选 **String []** 参数。<br /><br /> 指定要添加到命令行的附加项。|
|**AdditionalLibraryDirectories**|可选 **String []** 参数。<br /><br /> 重写环境库路径。 指定目录名。<br /><br /> 有关详细信息，请参阅 [/LIBPATH（附加的 Libpath）](/cpp/build/reference/libpath-additional-libpath)。|
|**AdditionalOptions**|可选 **String** 参数。<br /><br /> 在命令行上指定的 lib.exe 选项列表  。 例如，/\<option1> /\<option2> /\<option#>。 此参数用于指定无法由其他任何 LIB 任务参数表示的 lib.exe 选项   。<br /><br /> 有关详细信息，请参阅[运行 LIB](/cpp/build/reference/running-lib)。|
|**DisplayLibrary**|可选 **String** 参数。<br /><br /> 显示有关输出库的信息。 指定一个文件名，以便将信息重定向到该文件。 指定“CON”或不指定任何内容，以便将信息重定向到该控制台。<br /><br /> 此参数对应于 lib.exe 的 /LIST 选项   。|
|**ErrorReporting**|可选 **String** 参数。<br /><br /> 指定如果 lib.exe 在运行时失败，如何向 Microsoft 发送内部错误信息  。<br /><br /> 指定以下值之一，其中每个值对应于一个命令行选项。<br /><br /> -   **NoErrorReport** -  **/ERRORREPORT:NONE**<br />-   **PromptImmediately** -  **/ERRORREPORT:PROMPT**<br />-   **QueueForNextLogin** -  **/ERRORREPORT:QUEUE**<br />-   **SendErrorReport** -  **/ERRORREPORT:SEND**<br /><br /> 有关详细信息，请参阅**运行 LIB** 中的 [/ERRORREPORT](/cpp/build/reference/running-lib) 命令行选项。|
|**ExportNamedFunctions**|可选 **String []** 参数。<br /><br /> 指定要导出的一个或多个函数。<br /><br /> 此参数对应于 lib.exe 的 /EXPORT: 选项   。|
|**ForceSymbolReferences**|可选 **String** 参数。<br /><br /> 强制 lib.exe 包括对指定符号的引用  。<br /><br /> 此参数对应于 lib.exe 的 /INCLUDE: 选项   。|
|**IgnoreAllDefaultLibraries**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则在解析外部引用时从 lib.exe 搜索的库列表中删除所有默认库  。<br /><br /> 此参数对应于 lib.exe 的无参数形式 /NODEFAULTLIB 选项   。|
|**IgnoreSpecificDefaultLibraries**|可选 **String []** 参数。<br /><br /> 解析外部引用时，从 lib.exe 搜索的库列表中删除指定的库  。<br /><br /> 此形参对应于使用  **实参的 lib.exe 的 /NODEFAULTLIB 选项**  `library`。|
|**LinkLibraryDependencies**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，指定自动链接项目依赖项中的库输出。|
|**LinkTimeCodeGeneration**|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，指定链接时代码生成。<br /><br /> 此参数对应于 lib.exe 的 /LCTG 选项   。|
|**MinimumRequiredVersion**|可选 **String** 参数。<br /><br /> 指定子系统所需的最低版本。 指定范围在 0 到 65535 之间且以逗号分隔的十进制数字列表。|
|**ModuleDefinitionFile**|可选 **String** 参数。<br /><br /> 指定模块定义文件 (.def) 的名称  。<br /><br /> 此形参对应于使用  **实参的 lib.exe 的 /DEF 选项**  `filename`。|
|**Name**|可选 **String** 参数。<br /><br /> 生成导入库时，指定正在为其生成导入库的 DLL 的名称。<br /><br /> 此形参对应于使用  **实参的 lib.exe 的 /NAME 选项**  `filename`。|
|**OutputFile**|可选 **String** 参数。<br /><br /> 重写 lib.exe 所创建程序的默认名称和位置  。<br /><br /> 此形参对应于使用  **实参的 lib.exe 的 /OUT 选项**  `filename`。|
|**RemoveObjects**|可选 **String []** 参数。<br /><br /> 忽略输出库中的指定对象。 Lib.exe 通过组合所有对象（无论位于对象文件中还是库中），然后删除此选项指定的任何对象，来创建输出库  。<br /><br /> 此形参对应于使用  **实参的 lib.exe 的 /REMOVE 选项**  `membername`。|
|**Sources**|必选 `ITaskItem[]` 参数。<br /><br /> 指定用空格分隔的源文件列表。|
|**SubSystem**|可选 **String** 参数。<br /><br /> 为可执行文件指定环境。 子系统的选择会影响的入口点符号或入口点函数。<br /><br /> 指定以下值之一，其中每个值对应于一个命令行选项。<br /><br /> -   **控制台** -  **/SUBSYSTEM:CONSOLE**<br />-   **Windows** -  **/SUBSYSTEM:WINDOWS**<br />-   **本机** -  **/SUBSYSTEM:NATIVE**<br />-   **EFI 应用** -  **/SUBSYSTEM:EFI_APPLICATION**<br />-   **EFI 启动服务驱动程序** -  **/SUBSYSTEM:EFI_BOOT_SERVICE_DRIVER**<br />-   **EFI ROM** -  **/SUBSYSTEM:EFI_ROM**<br />-   **EFI 运行时** -  **/SUBSYSTEM:EFI_RUNTIME_DRIVER**<br />-   **WindowsCE** -  **/SUBSYSTEM:WINDOWSCE**<br />-   **POSIX** -  **/SUBSYSTEM:POSIX**<br /><br /> 有关详细信息，请参阅 [/SUBSYSTEM（指定子系统）](/cpp/build/reference/subsystem-specify-subsystem)。|
|**SuppressStartupBanner**|可选 **Boolean** 参数。<br /><br /> 如果为 `true`，则在任务开始时阻止显示版权和版本号消息。<br /><br /> 有关详细信息，请参阅**运行 LIB** 中的 [/NOLOGO](/cpp/build/reference/running-lib) 选项。|
|**TargetMachine**|可选 **String** 参数。<br /><br /> 指定程序或 DLL 的目标平台。<br /><br /> 指定以下值之一，其中每个值对应于一个命令行选项。<br /><br /> -   **MachineARM** -  **/MACHINE:ARM**<br />-   **MachineEBC** -  **/MACHINE:EBC**<br />-   **MachineIA64** -  **/MACHINE:IA64**<br />-   **MachineMIPS** -  **/MACHINE:MIPS**<br />-   **MachineMIPS16** -  **/MACHINE:MIPS16**<br />-   **MachineMIPSFPU** - **/MACHINE:MIPSFPU**<br />-   **MachineMIPSFPU16** -  **/MACHINE:MIPSFPU16**<br />-   **MachineSH4** -  **/MACHINE:SH4**<br />-   **MachineTHUMB** -  **/MACHINE:THUMB**<br />-   **MachineX64** -  **/MACHINE:X64**<br />-   **MachineX86** -  **/MACHINE:X86**<br /><br /> 有关详细信息，请参阅 [/MACHINE（指定目标平台）](/cpp/build/reference/machine-specify-target-platform)。|
|**TrackerLogDirectory**|可选 **String** 参数。<br /><br /> 指定跟踪器日志的目录。|
|**TreatLibWarningAsErrors**|可选 **Boolean** 参数。<br /><br /> 若为 `true`，LIB 任务不会在 lib.exe 生成警告时生成输出文件   。 如果为 `false`，则生成输出文件。<br /><br /> 有关详细信息，请参阅**运行 LIB** 中的 [/WX](/cpp/build/reference/running-lib) 选项。|
|**UseUnicodeResponseFiles**|可选 **Boolean** 参数。<br /><br /> 如果为 `true`，则指示在生成库管理器时，项目系统生成 UNICODE 响应文件。 当项目中的文件具有 UNICODE 路径时，指定 `true`。|
|**Verbose**|可选 **Boolean** 参数。<br /><br /> 如果为 `true`，则显示有关会话进度的详细信息；这包括正在添加的 .obj 文件的名称  。 信息被发送到标准输出，并可重定向到文件。<br /><br /> 有关详细信息，请参阅**运行 LIB** 中的 [/VERBOSE](/cpp/build/reference/running-lib) 选项。|

## <a name="see-also"></a>另请参阅

- [任务参考](../msbuild/msbuild-task-reference.md)