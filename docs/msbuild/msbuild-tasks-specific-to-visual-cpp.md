---
title: 特定于 C++ 的 MSBuild 任务 | Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, tasks specific to C++
ms.assetid: 05410f0c-7356-4692-bc00-20664421c9ff
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 6393e771f9e9ed862d21397dabacdb3f3808c386
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633143"
---
# <a name="msbuild-tasks-specific-to-c"></a>特定于 C++ 的 MSBuild 任务

任务提供在生成过程中运行的代码。 安装 C++ 后，除了随 MSBuild 安装的任务外，以下任务也可用。 有关详细信息，请参阅 [MSBuild ( C++) 概述](/cpp/build/msbuild-visual-cpp-overview)。

 除了特定于每个任务的参数外，每个任务还具有以下参数。

| 参数 | 描述 |
|-------------------| - |
| `Condition` | 可选 `String` 参数。<br /><br /> MSBuild 引擎使用 `Boolean` 表达式来确定是否执行此任务。 有关 MSBuild 支持的条件的信息，请参阅[条件](../msbuild/msbuild-conditions.md)。 |
| `ContinueOnError` | 可选参数。 可以包含下列值之一：<br /><br /> -   **WarnAndContinue** 或 **true**。 当任务失败时，[Target](../msbuild/target-element-msbuild.md) 元素中的后续任务和生成将继续执行，并且来自该任务的所有错误都被视为警告<br />-   **ErrorAndContinue**。 当任务失败时，`Target` 元素中的后续任务和生成将继续执行，并且来自该任务的所有错误都被视为错误。<br />-   **ErrorAndStop** 或 **false**（默认值）。 当任务失败时，将不会执行 `Target` 元素中的剩余任务和生成，并且整个 `Target` 元素和生成都被视为已失败。<br /><br /> 4\.5 之前的 .NET Framework 版本仅支持 `true` 和 `false` 值。<br /><br /> 有关详细信息，请参阅[如何：忽略任务中的错误](../msbuild/how-to-ignore-errors-in-tasks.md)。 |

### <a name="related-topics"></a>相关主题

|Title|描述|
|-----------|-----------------|
|[BscMake 任务](../msbuild/bscmake-task.md)|包装 Microsoft 浏览信息维护实用工具 (bscmake.exe)  。|
|[CL 任务](../msbuild/cl-task.md)|包装 C++ 编译器工具 (cl.exe)  。|
|[CPPClean 任务](../msbuild/cppclean-task.md)|删除生成 C++ 项目时 MSBuild 创建的临时文件。|
|[ClangCompile 任务](../msbuild/clangcompile-task.md)|包装 C++ 编译器工具 (clang.exe)  。|
|[CustomBuild 任务](../msbuild/custombuild-task.md)|包装 C++ 编译器工具 (cmd.exe)  。|
|[FXC 任务](../msbuild/fxc-task.md)|在生成过程中使用 HLSL 着色器编译器。|
|[GetOutOfDateItems](../msbuild/getoutofdateitems-task.md)|读取旧 tlog、写入新 tlog 并返回不是最新的项集合。 （帮助程序任务）|
|[GetOutputFileName](../msbuild/getoutputfilename-task.md)|获取有关 cl 和其他工具（只允许指定输出目录或完整文件名或不允许指定任何内容）的输出文件名。 （帮助程序任务）|
|[LIB 任务](../msbuild/lib-task.md)|包装 Microsoft 32 位库管理器工具 (lib.exe)  。|
|[Link 任务](../msbuild/link-task.md)|包装 C++ 链接器工具 (link.exe)  。|
|[MIDL 任务](../msbuild/midl-task.md)|包装 Microsoft 接口定义语言 (MIDL) 编译器工具 (midl.exe)  。|
|[MT 任务](../msbuild/mt-task.md)|包装 Microsoft 清单工具 (mt.exe)。 |
|[MultiToolTask 任务](../msbuild/multitooltask-task.md)|无说明。|
|[ParallelCustomBuild 任务](../msbuild/parallelcustombuild-task.md)|运行 [CustomBuild 任务](../msbuild/custombuild-task.md)的并行实例。|
|[RC 任务](../msbuild/rc-task.md)|包装 Microsoft Windows 资源编译器工具 (rc.exe)。 |
|[SetEnv 任务](../msbuild/setenv-task.md)|设置或删除指定环境变量的值。|
|[TrackedVCToolTask 基类](../msbuild/trackedvctooltask-base-class.md)|继承自 [VCToolTask](../msbuild/vctooltask-base-class.md)。|
|[VCMessage 任务](../msbuild/vcmessage-task.md)|记录生成期间的警告消息和错误消息。 （不可扩展。 仅限内部使用。）|
|[VCToolTask 基类](../msbuild/vctooltask-base-class.md)|继承自 [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask)。|
|[XDCMake 任务](../msbuild/xdcmake-task.md)|包装 XML 文档工具 (xdcmake.exe  )，它将 XML 文档注释 (.xdc  ) 文件合并到一个 .xml  文件中。|
|[XSD 任务](../msbuild/xsd-task.md)|包装从源生成架构或类文件的 XML 架构定义工具 (xsd.exe)。  请参见下面的注释。 |
|[MSBuild 参考](../msbuild/msbuild-reference.md)|介绍 MSBuild 系统的元素。|
|[任务](../msbuild/msbuild-tasks.md)|介绍任务，这些任务是代码单元，可以组合起来以产生生成。|
|[任务写入](../msbuild/task-writing.md)|描述如何创建任务。|

> [!NOTE]
> 自 Visual Studio 2017 开始，已弃用对 xsd.exe 的 C++ 项目支持  。 仍可通过向 GAC 手动添加 CppCodeProvider.dll 来使用 Microsoft.VisualC.CppCodeProvider   。
