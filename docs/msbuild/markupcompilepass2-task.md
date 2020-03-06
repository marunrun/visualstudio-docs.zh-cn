---
title: MarkupCompilePass2 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- performing second-pass markup [WPF MSBuild], MarkupCompilePass2 task
- MarkupCompilePass2 task [WPF MSBuild]
- MarkupCompilePass2 task [WPF MSBuild], parameters
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d18bc3638454e2a6b034cd2e35c3a158361a033e
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633520"
---
# <a name="markupcompilepass2-task"></a>MarkupCompilePass2 任务

<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> 任务对引用同一项目中的类型的 XAML 文件执行第二轮标记编译。

## <a name="task-parameters"></a>任务参数

| 参数 | 描述 |
| - | - |
| `AlwaysCompileMarkupFilesInSeparateDomain` | 可选 **Boolean** 参数。<br /><br /> 指定是否在单独的 <xref:System.AppDomain> 下运行该任务。 如果此参数返回 false，则任务将在与 MSBuild 相同的 <xref:System.AppDomain> 中运行，且运行速度更快  。 如果该参数返回 true，则任务将在独立于 MSBuild 的另一个 <xref:System.AppDomain> 中运行，且运行速度更慢  。 |
| `AssembliesGeneratedDuringBuild` | 可选 **String []** 参数。<br /><br /> 指定在生成过程中对更改的程序集的引用。 例如，Visual Studio 解决方案可能包含一个引用了另一个项目的已编译输出的项目。 在这种情况下，可以将第二个项目的已编译输出添加到 **AssembliesGeneratedDuringBuild**。<br /><br /> 注意：“AssembliesGeneratedDuringBuild”必须包含对生成解决方案所生成的一组完整程序集的引用  。 |
| `AssemblyName` | 必需的 **String** 参数。<br /><br /> 指定为项目生成的程序集的简称。 例如，如果项目生成一个名为 WinExeAssembly.exe 的可执行文件，则 AssemblyName 参数的值为 WinExeAssembly    。 |
| `GeneratedBaml` | 可选的 **ITaskItem[]** 输出参数。<br /><br /> 包含已生成的 XAML 二进制格式文件的列表。 |
| `KnownReferencePaths` | 可选 **String []** 参数。<br /><br /> 指定在生成过程中对从未更改的程序集的引用。 包括位于全局程序集缓存 (GAC)、.NET 安装目录等位置中的程序集。 |
| `Language` | 必需的 **String** 参数。<br /><br /> 指定编译器支持的托管语言。 有效的选项有 **C#** 、**VB**、**JScript** 和 **C++** 。 |
| `LocalizationDirectivesToLocFile` | 可选 **String** 参数。<br /><br /> 指定如何针对每个源 XAML 文件生成本地化信息。 有效选项有“无”  、“仅注释”  和“全部”  。 |
| `OutputPath` | 必需的 **String** 参数。<br /><br /> 指定在其中生成 XAML 二进制格式文件的目录。 |
| `OutputType` | 必需的 **String** 参数。<br /><br /> 指定项目生成的程序集的类型。 有效选项有 **winexe**、**exe**、**library** 和 **netmodule**。 |
| `References` | 可选的 **ITaskItem[]** 参数。<br /><br /> 指定引用列表，范围从文件到程序集，它们包含 XAML 文件中所使用的类型。 一个引用针对的是 <xref:Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly> 任务生成的程序集，该任务必须在 <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> 任务之前运行。 |
| `RootNamespace` | 可选 **String** 参数。<br /><br /> 指定项目内部的类的根命名空间。 当对应的 XAML 文件不包括 `x:Class` 属性时，RootNamespace  也将用作生成的托管代码文件的默认命名空间。 |
| `XAMLDebuggingInformation` | 可选 **Boolean** 参数。<br /><br /> 如果为 true  ，则会生成诊断信息并将其包括在编译的 XAML 中，以辅助调试。 |

## <a name="remarks"></a>备注

运行 MarkupCompilePass2  之前，必须先生成包含 XAML 文件（该文件的标记编译轮有延迟）所使用的类型的临时程序集。 通过运行 **GenerateTemporaryTargetAssembly** 任务生成临时程序集。

对生成的临时程序集的引用将在运行时提供给 <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2>，使得在第一轮标记编译过程中编译存在延迟的 XAML 文件现可编译为二进制格式。

## <a name="example"></a>示例

下面的示例演示如何使用 <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> 任务来执行第二轮编译。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.MarkupCompilePass2"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="MarkupCompilePass2Task">
    <MarkupCompilePass2
      AssemblyName="WPFMSBuildSample"
      Language="C#"
      OutputType="WinExe"
      OutputPath="obj\Debug\"
      References=".\obj\debug\WPFMSBuildSample.exe;c:\windows\Microsoft.net\Framework\v2.0.50727\System.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationCore.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationFramework.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\WindowsBase.dll" />
  </Target>
</Project>
```

## <a name="see-also"></a>请参阅

- [WPF MSBuild 参考](../msbuild/wpf-msbuild-reference.md)
- [WPF MSBuild 任务参考](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [MSBuild 任务参考](../msbuild/msbuild-task-reference.md)
- [生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
- [WPF XAML 浏览器应用程序概述](/dotnet/framework/wpf/app-development/wpf-xaml-browser-applications-overview)
