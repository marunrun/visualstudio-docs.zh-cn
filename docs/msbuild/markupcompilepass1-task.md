---
title: MarkupCompilePass1 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- converting XAML to binary format [WPF MSBuild]
- MarkupCompilePass1 task [WPF MSBuild], parameters
- converting XAML projects to compiled binary format [WPF MSBuild]
- MarkupCompilePass1 task [WPF MSBuild], converting XAML to binary format
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dfcd34daa6a9a2b4cb4bd095bc91ac5962c7335d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62979771"
---
# <a name="markupcompilepass1-task"></a>MarkupCompilePass1 任务

<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass1> 任务会将非本地化的 [!INCLUDE[TLA#tla_xaml](../msbuild/includes/tlasharptla_xaml_md.md)] 项目文件转换成已编译的二进制格式。

## <a name="task-parameters"></a>任务参数

| 参数 | 说明 |
| - | - |
| `AllGeneratedFiles` | 可选的 **ITaskItem[]** 输出参数。<br /><br /> 包含由 <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass1> 任务生成的文件的完整列表。 |
| `AlwaysCompileMarkupFilesInSeparateDomain` | 可选 **Boolean** 参数。<br /><br /> 指定是否在单独的 <xref:System.AppDomain> 下运行该任务。 如果此参数返回 false，则任务将在与 [!INCLUDE[TLA#tla_msbuild](../msbuild/includes/tlasharptla_msbuild_md.md)] 相同的 <xref:System.AppDomain> 中运行，且运行速度更快。 如果该参数返回 true，则任务将在独立于 [!INCLUDE[TLA2#tla_msbuild](../msbuild/includes/tla2sharptla_msbuild_md.md)] 的另一个 <xref:System.AppDomain> 中运行，且运行速度更慢。 |
| `ApplicationMarkup` | 可选的 **ITaskItem[]** 参数。<br /><br /> 指定应用程序定义 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件的名称。 |
| `AssembliesGeneratedDuringBuild` | 可选 **String []** 参数。<br /><br /> 指定在生成过程中对更改的程序集的引用。 例如，Visual Studio 解决方案可能包含一个引用了另一个项目的已编译输出的项目。 在这种情况下，可以将第二个项目的已编译输出添加到 **AssembliesGeneratedDuringBuild** 参数。<br /><br /> 注意:“AssembliesGeneratedDuringBuild”参数必须包含对生成解决方案所生成的一组完整程序集的引用。 |
| `AssemblyName` | 必需的 **String** 参数。<br /><br /> 指定为项目生成的程序集的简称。 例如，如果项目生成一个名为 *WinExeAssembly.exe* 的 [!INCLUDE[TLA#tla_mswin](../code-quality/includes/tlasharptla_mswin_md.md)] 可执行文件，则 **AssemblyName** 参数的值为 **WinExeAssembly**。 |
| `AssemblyPublicKeyToken` | 可选 **String** 参数。<br /><br /> 指定程序集的公钥标记。 |
| `AssemblyVersion` | 可选 **String** 参数。<br /><br /> 指定程序集的版本号。 |
| `ContentFiles` | 可选的 **ITaskItem[]** 参数。<br /><br /> 指定松散的内容文件列表。 |
| `DefineConstants` | 可选 **String** 参数。<br /><br /> 指定保留 **DefineConstants** 的当前值。 这会影响目标程序集的生成；如果更改此参数，则目标程序集中的公共 API 可能会发生更改，并且引用本地类型的 [!INCLUDE[TLA2#tla_titlexaml](../msbuild/includes/tla2sharptla_titlexaml_md.md)] 文件的编译可能会受到影响。 |
| `ExtraBuildControlFiles` | 可选的 **ITaskItem[]** 参数。<br /><br /> 指定用于控制在重新运行 <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass1> 任务时是否触发重新生成的文件列表；如果这些文件中的一个文件发生更改，则触发重新生成。 |
| `GeneratedBamlFiles` | 可选的 **ITaskItem[]** 输出参数。<br /><br /> 包含已生成的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 二进制格式文件的列表。 |
| `GeneratedCodeFiles` | 可选的 **ITaskItem[]** 输出参数。<br /><br /> 包含生成的托管代码文件的列表。 |
| `GeneratedLocalizationFiles` | 可选的 **ITaskItem[]** 输出参数。<br /><br /> 包含为每个可本地化的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件生成的本地化文件的列表。 |
| `HostInBrowser` | 可选 **String** 参数。<br /><br /> 指定生成的程序集是否为 [!INCLUDE[TLA#tla_xbap](../msbuild/includes/tlasharptla_xbap_md.md)]。 有效的选项为“true”和“false”。 如果为“true”，则生成代码以支持浏览器承载。 |
| `KnownReferencePaths` | 可选 **String []** 参数。<br /><br /> 指定对在生成过程中不更改的程序集的引用。 包括位于 [!INCLUDE[TLA#tla_gac](../msbuild/includes/tlasharptla_gac_md.md)]、[!INCLUDE[TLA#tla_netframewk](../misc/includes/tlasharptla_netframewk_md.md)] 安装目录等位置中的程序集。 |
| `Language` | 必需的 **String** 参数。<br /><br /> 指定编译器支持的托管语言。 有效的选项有 **C#**、**VB**、**JScript** 和 **C++**。 |
| `LanguageSourceExtension` | 可选 **String** 参数。<br /><br /> 指定追加到所生成的托管代码文件扩展名的扩展名：<br /><br /> `<Filename>.g<LanguageSourceExtension>`<br /><br /> 如果未采用特定的值来设置 **LanguageSourceExtension** 参数，则使用语言的默认源文件扩展名：*.vb*（适用于 [!INCLUDE[TLA#tla_visualb](../msbuild/includes/tlasharptla_visualb_md.md)]）和 *.csharp*（适用于 [!INCLUDE[TLA#tla_cshrp](../data-tools/includes/tlasharptla_cshrp_md.md)]）。 |
| `LocalizationDirectivesToLocFile` | 可选 **String** 参数。<br /><br /> 指定如何针对每个源 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件生成本地化信息。 有效选项有“无”、“仅注释”和“全部”。 |
| `OutputPath` | 必需的 **String** 参数。<br /><br /> 指定在其中生成托管代码文件和 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 二进制格式文件的目录。 |
| `OutputType` | 必需的 **String** 参数。<br /><br /> 指定项目生成的程序集的类型。 有效选项有 **winexe**、**exe**、**library** 和 **netmodule**。 |
| `PageMarkup` | 可选的 **ITaskItem[]** 参数。<br /><br /> 指定要处理的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件列表。 |
| `References` | 可选的 **ITaskItem[]** 参数。<br /><br /> 指定引用列表，范围从文件到程序集，它们包含 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件中所使用的类型。 |
| `RequirePass2ForMainAssembly` | 可选 **Boolean** 输出参数。<br /><br /> 指示项目是否包含不可本地化的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件（这些文件引用嵌入到主程序集中的本地类型）。 |
| `RequirePass2ForSatelliteAssembly` | 可选 **Boolean** 输出参数。<br /><br /> 指示项目是否包含可本地化的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件（这些文件引用嵌入在主程序集中的本地类型）。 |
| `RootNamespace` | 可选 **String** 参数。<br /><br /> 指定项目内部的类的根命名空间。 当对应的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件不包括 `x:Class` 属性时，**RootNamespace** 也将用作生成的托管代码文件的默认命名空间。 |
| `SourceCodeFiles` | 可选的 **ITaskItem[]** 参数。<br /><br /> 指定当前项目的代码文件列表。 此列表不包括所生成的特定于语言的托管代码文件。 |
| `UICulture` | 可选 **String** 参数。<br /><br /> 为在其中嵌入所生成的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 二进制格式文件的 UI 区域性指定附属程序集。 如果未设置 **UICulture**，则所生成的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 二进制格式文件将嵌入主程序集中。 |
| `XAMLDebuggingInformation` | 可选 **Boolean** 参数。<br /><br /> 如果为 **true**，则会生成诊断信息并将其包括在编译的 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 中，以辅助调试。 |

## <a name="remarks"></a>备注

<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass1> 任务通常将 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 编译成二进制格式并生成代码文件。 如果 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件包含对在相同项目中定义的类型的引用，则将此文件编译为二进制格式的任务会被 **MarkupCompilePass1** 推迟到第二个标记编译阶段 (**MarkupCompilePass2**)。 必须将此类文件的编译推迟，因为必须等到所引用的以本地方式定义的类型编译完后，才会对其进行编译。 但如果 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件具有 `x:Class` 属性，<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass1> 会为其生成特定于语言的代码文件。

如果 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件包含使用 `x:Uid` 属性的元素，则此文件是可本地化的文件：

```xml
<Page x:Class="WPFMSBuildSample.Page1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Uid="Page1Uid"
    >
  ...
</Page>
```

[!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件在声明 [!INCLUDE[TLA#tla_xml](../msbuild/includes/tlasharptla_xml_md.md)] 命名空间（该命名空间使用 `clr-namespace` 值来表示当前项目中的命名空间）时，它将引用以本地方式定义的类型：

```xml
<Page x:Class="WPFMSBuildSample.Page1"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:localNamespace="clr-namespace:WPFMSBuildSample"
    >
    <Grid>
      <Grid.Resources>
        <localNameSpace:LocalType x:Key="localType" />
      </Grid.Resources>
      ...
    </Grid>
</Page>
```

如果有任何 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件可进行本地化，或引用了以本地方式定义的类型，则需要第二个标记编译阶段，这需要先运行 [GenerateTemporaryTargetAssembly](../msbuild/generatetemporarytargetassembly-task.md)，然后再运行 [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md)。

## <a name="example"></a>示例

下面的示例演示如何将三个页面 [!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 文件转换成二进制格式文件。 Page1 包含对位于项目的根命名空间的类型 `Class1` 的引用，因此在此标记编译阶段不会转换为二进制格式文件。 改为执行 [GenerateTemporaryTargetAssembly](../msbuild/generatetemporarytargetassembly-task.md)，然后再执行 [MarkupCompilePass2](../msbuild/markupcompilepass2-task.md)。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.MarkupCompilePass1"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="MarkupCompilePass1Task">
    <MarkupCompilePass1
      AssemblyName="WPFMSBuildSample"
      Language="C#"
      OutputType="WinExe"
      OutputPath="obj\Debug\"
      ApplicationMarkup="App.xaml"
      PageMarkup="Page1.xaml;Page2.xaml;Page3.xaml"
      SourceCodeFiles="Class1.cs"
      References="c:\windows\Microsoft.net\Framework\v2.0.50727\System.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationCore.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\PresentationFramework.dll;C:\Program Files\Reference Assemblies\Microsoft\WinFx\v3.0\WindowsBase.dll" />
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