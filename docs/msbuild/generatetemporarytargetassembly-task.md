---
title: GenerateTemporaryTargetAssembly 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- build process [WPF MSBuild], XAML page refers to a locally declared type
- GenerateTemporaryTargetAssembly task [WPF MSBuild]
- GenerateTemporaryTargetAssembly task [WPF MSBuild], parameters
- creating an assembly [WPF MSBuild], XAML page refers to a locally declared type
ms.assetid: 92b6539c-6897-45e0-8989-0c234bbfe782
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 634cf365c0cd42e3eb146b74a137a66f742a8730
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594807"
---
# <a name="generatetemporarytargetassembly-task"></a>GenerateTemporaryTargetAssembly 任务
如果项目中至少有一个 [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] 页引用该项目中本地声明的类型，则 <xref:Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly> 任务会生成一个程序集。 在生成过程完成后或者在生成过程失败的情况下，生成的程序集会被删除。

## <a name="task-parameters"></a>任务参数

| 参数 | 描述 |
|--------------------------| - |
| `AssemblyName` | 必需的 **String** 参数。<br /><br /> 指定为项目生成的程序集的短名称，该名称同时也是临时生成的目标程序集的名称。 例如，如果项目生成一个名为 *WinExeAssembly.exe* 的 [!INCLUDE[TLA#tla_mswin](../code-quality/includes/tlasharptla_mswin_md.md)] 可执行文件，则 **AssemblyName** 参数的值为 **WinExeAssembly**。 |
| `CompileTargetName` | 必需的 **String** 参数。<br /><br /> 指定用于从源代码文件生成程序集的 [!INCLUDE[TLA#tla_msbuild](../msbuild/includes/tlasharptla_msbuild_md.md)] 目标的名称。 **CompileTargetName** 的典型值为 **CoreCompile**。 |
| `CompileTypeName` | 必需的 **String** 参数。<br /><br /> 指定由 **CompileTargetName** 参数所指定目标执行的编译的类型。 对于 **CoreCompile** 目标，此值为 **Compile**。 |
| `CurrentProject` | 必需的 **String** 参数。<br /><br /> 为要求临时目标程序集的项目指定 [!INCLUDE[TLA2#tla_msbuild](../msbuild/includes/tla2sharptla_msbuild_md.md)] 项目文件的完整路径。 |
| `GeneratedCodeFiles` | 可选的 **ITaskItem[]** 参数。<br /><br /> 指定由 [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md) 任务生成的语言特定托管代码文件列表。 |
| `IntermediateOutputPath` | 必需的 **String** 参数。<br /><br /> 指定在其中生成临时目标程序集的目录。 |
| `MSBuildBinPath` | 必需的 **String** 参数。<br /><br /> 指定编译临时目标程序集所需的 *MSBuild.exe* 的位置。 |
| `ReferencePath` | 可选的 **ITaskItem[]** 参数。<br /><br /> 按路径和文件名指定一列由编译到临时目标程序集中的类型所引用的程序集。 |
| `ReferencePathTypeName` | 必需的 **String** 参数。<br /><br /> 指定编译目标 (**CompileTargetName**) 参数用于指定程序集引用列表 (**ReferencePath**) 的参数。 相应的值为 **ReferencePath**。 |

## <a name="remarks"></a>备注
第一个标记编译传递（由 [MarkupCompilePass1](../msbuild/markupcompilepass1-task.md) 运行）会将 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件编译为二进制格式。 因此，编译器需要一列其中包含 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件所使用的类型的引用程序集。 但是，如果 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件使用在同一项目中定义的类型，则直到该项目生成时才会创建该项目对应的程序集。 因此，在第一个标记编译传递期间无法提供程序集引用。

但是，**MarkupCompilePass1** 会将包含对同一项目中类型的引用的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件转换推迟到由 [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md) 执行的第二个标记编译传递。 **MarkupCompilePass2** 执行前会生成一个临时程序集。 该程序集包含推迟了标记编译传递的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件所使用的类型。 在其运行以允许被推迟的编译 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件转换为二进制格式时，会向 **MarkupCompilePass2** 提供一个对已生成程序集的引用。

## <a name="example"></a>示例
以下示例会生成一个临时程序集，因为 Page1.xaml 包含对同一项目中的类型的引用  。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="GenerateTemporaryTargetAssemblyTask">
    <GenerateTemporaryTargetAssembly
      AssemblyName="WPFMSBuildSample"
      CompileTargetName="CoreCompile"
      CompileTypeName="Compile"
      CurrentProject="FullBuild.proj"
      GeneratedCodeFiles="obj\debug\app.g.cs;obj\debug\Page1.g.cs;obj\debug\Page2.g.cs"
      ReferencePath="c:\windows\Microsoft.net\Framework\v2.0.50727\System.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationCore.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationFramework.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\WindowsBase.dll"
      IntermediateOutputPath=".\obj\debug\"
      MSBuildBinPath="$(MSBuildBinPath)"
      ReferencePathTypeName="ReferencePath"/>
  </Target>
</Project>
```

## <a name="see-also"></a>请参阅
- [WPF MSBuild 参考](../msbuild/wpf-msbuild-reference.md)
- [任务参考](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
- [生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
- [WPF XAML 浏览器应用程序概述](/dotnet/framework/wpf/app-development/wpf-xaml-browser-applications-overview)
