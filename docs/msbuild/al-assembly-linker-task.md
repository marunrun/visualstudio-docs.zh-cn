---
title: AL（程序集链接器）任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#AL
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- AL task [MSBuild]
- MSBuild, AL task
ms.assetid: 2ddefbf2-5662-4d55-99a6-ac383bf44560
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d90e6c94d07b73e79d793982944bca395a562df2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593468"
---
# <a name="al-assembly-linker-task"></a>AL（程序集链接器）任务
AL 任务包装 AL.exe（一种随 [!INCLUDE[winsdklong](../deployment/includes/winsdklong_md.md)] 一起分发的工具）  。 此程序集链接器工具用于创建包含来自一个或多个文件（这些文件可以是模块或资源文件）的清单的程序集。 编译器和开发环境可能已提供这些功能，因此通常不需要直接使用此任务。 对于需要从多个组件文件（例如可能从混合语言开发生成的组件文件）创建单个程序集的开发人员来说，程序集链接器非常有用。 此任务不能将模块合并到单个程序集文件；单个模块必须仍为分布式且可用，以便正确加载生成程序集。 有关 AL.exe 的详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)  。

## <a name="parameters"></a>参数
 下表描述了 `AL` 任务的参数。

| 参数 | 描述 |
|---------------------| - |
| `AlgorithmID` | 可选 `String` 参数。<br /><br /> 指定一种算法来对多文件程序集中的所有文件（包含程序集清单的文件除外）进行哈希处理。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/algid` 选项的文档。 |
| `BaseAddress` | 可选 `String` 参数。<br /><br /> 指定一个地址，运行时在用户计算机上在该地址加载 DLL。 如果指定 DLL 的基址，而不是让操作系统在进程空间内重新定位 DLL，则应用程序的加载速度会更快。 此参数对应于 /base[address](/dotnet/framework/tools/al-exe-assembly-linker)。 |
| `CompanyName` | 可选 `String` 参数。<br /><br /> 为程序集中的 `Company` 字段指定字符串。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/comp[any]` 选项的文档。 |
| `Configuration` | 可选 `String` 参数。<br /><br /> 为程序集中的 `Configuration` 字段指定字符串。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/config[uration]` 选项的文档。 |
| `Copyright` | 可选 `String` 参数。<br /><br /> 为程序集中的 `Copyright` 字段指定字符串。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/copy[right]` 选项的文档。 |
| `Culture` | 可选 `String` 参数。<br /><br /> 指定要与程序集关联的区域性字符串。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/c[ulture]` 选项的文档。 |
| `DelaySign` | 可选 `Boolean` 参数。<br /><br /> 若要仅将公钥放在程序集中，则为 `true`；若要对程序集进行完全签名，则为 `false`。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/delay[sign]` 选项的文档。 |
| `Description` | 可选 `String` 参数。<br /><br /> 为程序集中的 `Description` 字段指定字符串。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/descr[iption]` 选项的文档。 |
| `EmbedResources` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 将指定资源嵌入包含程序集清单的映像中。 此任务将资源文件的内容复制到映像。 传递给此参数的项可能附加名为 `LogicalName` 和 `Access` 的可选元数据。 `LogicalName` 元数据用于指定资源的内部标识符。  `Access` 元数据可以设置为 `private`，以使该资源对其他程序集不可见。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/embed[resource]` 选项的文档。 |
| `EvidenceFile` | 可选 `String` 参数。<br /><br /> 将指定文件嵌入资源名为 `Security.Evidence` 的程序集。<br /><br /> 不能对常规资源使用 `Security.Evidence`。 此参数对应于 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中的 `/e[vidence]` 选项。 |
| `ExitCode` | 可选 `Int32` 输出只读参数。<br /><br /> 指定执行的命令提供的退出代码。 |
| `FileVersion` | 可选 `String` 参数。<br /><br /> 为程序集中的 `File Version` 字段指定字符串。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/fileversion` 选项的文档。 |
| `Flags` | 可选 `String` 参数。<br /><br /> 为程序集中的 `Flags` 字段指定一个值。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/flags` 选项的文档。 |
| `GenerateFullPaths` | 可选 `Boolean` 参数。<br /><br /> 使此任务对错误消息中报告的任何文件使用绝对路径。 此参数对应于 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中的 `/fullpaths` 选项。 |
| `KeyContainer` | 可选 `String` 参数。<br /><br /> 指定保存密钥对的容器。 这样将会通过将公钥插入程序集清单来对程序集签名（为它指定一个强名称）。 然后，此任务使用私钥对最终程序集进行签名。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/keyn[ame]` 选项的文档。 |
| `KeyFile` | 可选 `String` 参数。<br /><br /> 指定一个文件，该文件包含密钥对或只包含用于对程序集进行签名的公钥。 编译器在程序集清单中插入公钥，然后使用私钥对最终的程序集进行签名。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/keyf[ile]` 选项的文档。 |
| `LinkResources` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 将指定的资源文件链接至某个程序集。 该资源成为程序集的组成部分，但不复制该文件。 传递给此参数的项可能附加名为 `LogicalName``Target` 和 `Access` 的可选元数据。 `LogicalName` 元数据用于指定资源的内部标识符。 `Target` 元数据可以指定任务将文件复制到的路径和文件名，然后将此新文件编译到程序集。 `Access` 元数据可以设置为 `private`，以使该资源对其他程序集不可见。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/link[resource]` 选项的文档。 |
| `MainEntryPoint` | 可选 `String` 参数。<br /><br /> 指定用作将模块转换为可执行文件时的入口点的方法的完全限定名称 (*class.method*)。 此参数对应于 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中的 `/main` 选项。 |
| `OutputAssembly` | 必需的 <xref:Microsoft.Build.Framework.ITaskItem> 输出参数。<br /><br /> 指定此任务生成的文件的名称。 此参数对应于 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中的 `/out` 选项。 |
| `Platform` | 可选 `String` 参数。<br /><br /> 限制可运行此代码的平台；必须是下面中的某一项：`x86`、`Itanium`、`x64` 或 `anycpu`。 默认值为 `anycpu`。 此参数对应于 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中的 `/platform` 选项。 |
| `ProductName` | 可选 `String` 参数。<br /><br /> 为程序集中的 `Product` 字段指定字符串。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/prod[uct]` 选项的文档。 |
| `ProductVersion` | 可选 `String` 参数。<br /><br /> 为程序集中的 `ProductVersion` 字段指定字符串。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/productv[ersion]` 选项的文档。 |
| `ResponseFiles` | 可选 `String[]` 参数。<br /><br /> 指定包含要传递到程序集链接器的其他选项的响应文件。 |
| `SdkToolsPath` | 可选 `String` 参数。<br /><br /> 指定 SDK 工具（例如 resgen.exe）的路径。 |
| `SourceModules` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 要编译到程序集中的一个或多个模块。 模块将在生成的程序集清单中列出，并且仍需为分布式且可用，以便加载程序集。 传递到此参数的项可能具有名为 `Target` 的其他元数据，该元数据指定任务将文件复制到的路径和文件名，然后将此新文件编译到程序集。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)的文档。 此参数对应于不使用特定开关而传递到 Al.exe 的模块的列表。  |
| `TargetType` | 可选 `String` 参数。<br /><br /> 指定输出文件的文件格式：`library`（代码库）、`exe`（控制台应用程序）或 `win`（基于 Windows 的应用程序）。 默认值为 `library`。 此参数对应于 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中的 `/t[arget]` 选项。 |
| `TemplateFile` | 可选 `String` 参数。<br /><br /> 指定程序集，除区域性字段之外的所有程序集元数据都从该程序集继承。 指定的程序集必须具有强名称。<br /><br /> 使用 `TemplateFile` 参数创建的程序集将成为附属程序集。 此参数对应于 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中的 `/template` 选项。 |
| `Timeout` | 可选 `Int32` 参数。<br /><br /> 指定终止任务可执行文件之前的时间量（以毫秒为单位）。 默认值是 `Int.MaxValue`，指示没有超时期限。 |
| `Title` | 可选 `String` 参数。<br /><br /> 为程序集中的 `Title` 字段指定字符串。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/title` 选项的文档。 |
| `ToolPath` | 可选 `String` 参数。<br /><br /> 指定任务从中加载基础可执行文件 (Al.exe) 的位置。 如果未指定此参数，则任务会使用与运行 [!INCLUDE[vstecmsbuild](../extensibility/internals/includes/vstecmsbuild_md.md)] 的框架版本对应的 SDK 安装路径。 |
| `Trademark` | 可选 `String` 参数。<br /><br /> 为程序集中的 `Trademark` 字段指定字符串。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/trade[mark]` 选项的文档。 |
| `Version` | 可选 `String` 参数。<br /><br /> 指定此程序集的版本信息。 此字符串的格式是 *major.minor.build.revision*。 默认值为 0。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/v[ersion]` 选项的文档。 |
| `Win32Icon` | 可选 `String` 参数。<br /><br /> 在程序集中插入 .ico 文件  。 .ico 文件在文件资源管理器中赋予输出文件所需的外观  。 此参数对应于 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中的 `/win32icon` 选项。 |
| `Win32Resource` | 可选 `String` 参数。<br /><br /> 在输出文件中插入 Win32 资源（.res 文件）  。 有关详细信息，请参阅 [Al.exe（程序集链接器）](/dotnet/framework/tools/al-exe-assembly-linker)中 `/win32res` 选项的文档。 |

## <a name="remarks"></a>备注
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.ToolTaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.ToolTask> 类。 有关这些其他参数的列表及其说明，请参阅 [ToolTaskExtension 基类](../msbuild/tooltaskextension-base-class.md)。

## <a name="example"></a>示例
 以下示例通过指定选项创建程序集。

```xml
<AL
    EmbedResources="@(EmbeddedResource)"
    Culture="%(EmbeddedResource.Culture)"
    TemplateFile="@(IntermediateAssembly)"
    KeyContainer="$(KeyContainerName)"
    KeyFile="$(KeyOriginatorFile)"
    DelaySign="$(DelaySign)"

    OutputAssembly=
       "%(EmbeddedResource.Culture)\$(TargetName).resources.dll">

    <Output TaskParameter="OutputAssembly"
        ItemName="SatelliteAssemblies"/>
</AL>
```

## <a name="see-also"></a>请参阅
* [任务参考](../msbuild/msbuild-task-reference.md)
* [任务](../msbuild/msbuild-tasks.md)
