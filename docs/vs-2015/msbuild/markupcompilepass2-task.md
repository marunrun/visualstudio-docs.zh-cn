---
title: MarkupCompilePass2 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
ms.assetid: 1d25689a-d21f-4b05-be26-95aa0ed4fd03
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 47e27dbfa221a9476488d563ae2a48235a08f769
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65703443"
---
# <a name="markupcompilepass2-task"></a>MarkupCompilePass2 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> 任务对引用同一项目中的类型的 [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] 文件执行第二轮标记编译。  
  
## <a name="task-parameters"></a>任务参数  
  
|参数|描述|  
|---------------|-----------------|  
|`AlwaysCompileMarkupFilesInSeparateDomain`|可选 **Boolean** 参数。<br /><br /> 指定是否在单独的 <xref:System.AppDomain> 下运行该任务。 如果此参数返回 false，则任务将在与 [!INCLUDE[TLA#tla_msbuild](../includes/tlasharptla-msbuild-md.md)] 相同的 <xref:System.AppDomain> 中运行，且运行速度更快****。 如果该参数返回 true，则任务将在独立于 [!INCLUDE[TLA2#tla_msbuild](../includes/tla2sharptla-msbuild-md.md)] 的另一个 <xref:System.AppDomain> 中运行，且运行速度更慢****。|  
|`AssembliesGeneratedDuringBuild`|可选 **String []** 参数。<br /><br /> 指定在生成过程中对更改的程序集的引用。 例如，[!INCLUDE[TLA#tla_visualstu2005](../includes/tlasharptla-visualstu2005-md.md)] 解决方案可能包含一个引用了另一个项目的已编译输出的项目。 在这种情况下，可以将第二个项目的已编译输出添加到 **AssembliesGeneratedDuringBuild**。<br /><br /> 注意：“AssembliesGeneratedDuringBuild”必须包含对生成解决方案所生成的一组完整程序集的引用  。|  
|`AssemblyName`|必需的 **String** 参数。<br /><br /> 指定为项目生成的程序集的简称。 例如，如果项目生成一个名为 **WinExeAssembly.exe** 的 [!INCLUDE[TLA#tla_win](../includes/tlasharptla-win-md.md)] 可执行文件，则 **AssemblyName** 参数的值为 **WinExeAssembly**。|  
|`GeneratedBaml`|可选的 **ITaskItem[]** 输出参数。<br /><br /> 包含已生成的 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 二进制格式文件的列表。|  
|`KnownReferencePaths`|可选 **String []** 参数。<br /><br /> 指定在生成过程中对从未更改的程序集的引用。 包括位于 [!INCLUDE[TLA#tla_gac](../includes/tlasharptla-gac-md.md)]、[!INCLUDE[TLA#tla_netframewk](../includes/tlasharptla-netframewk-md.md)] 安装目录等位置中的程序集。|  
|`Language`|必需的 **String** 参数。<br /><br /> 指定编译器支持的托管语言。 有效的选项有 **C#** 、**VB**、**JScript** 和 **C++** 。|  
|`LocalizationDirectivesToLocFile`|可选 **String** 参数。<br /><br /> 指定如何针对每个源 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 文件生成本地化信息。 有效选项有“无”  、“仅注释”  和“全部”  。|  
|`OutputPath`|必需的 **String** 参数。<br /><br /> 指定在其中生成 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 二进制格式文件的目录。|  
|`OutputType`|必需的 **String** 参数。<br /><br /> 指定项目生成的程序集的类型。 有效选项有 **winexe**、**exe**、**library** 和 **netmodule**。|  
|`References`|可选的 **ITaskItem[]** 参数。<br /><br /> 指定引用列表，范围从文件到程序集，它们包含 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 文件中所使用的类型。 一个引用针对的是 <xref:Microsoft.Build.Tasks.Windows.GenerateTemporaryTargetAssembly> 任务生成的程序集，该任务必须在 <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> 任务之前运行。|  
|`RootNamespace`|可选 **String** 参数。<br /><br /> 指定项目内部的类的根命名空间。 当对应的 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 文件不包括 `x:Class` 属性时，**RootNamespace** 也将用作生成的托管代码文件的默认命名空间。|  
|`XAMLDebuggingInformation`|可选 **Boolean** 参数。<br /><br /> 如果为 **true**，则会生成诊断信息并将其包括在编译的 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 中，以辅助调试。|  
  
## <a name="remarks"></a>备注  
 运行 **MarkupCompilePass2** 之前，必须先生成包含 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 文件（该文件的标记编译轮有延迟）所使用的类型的临时程序集。 通过运行 **GenerateTemporaryTargetAssembly** 任务生成临时程序集。  
  
 对生成的临时程序集的应用将在运行时提供给 <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2>，使得在第一轮标记编译过程中编译有延迟的 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 文件现可编译为二进制格式。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 <xref:Microsoft.Build.Tasks.Windows.MarkupCompilePass2> 任务来执行第二轮编译。  
  
```  
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
  
## <a name="see-also"></a>另请参阅  
 [WPF MSBuild 参考](../msbuild/wpf-msbuild-reference.md)   
 [任务引用](../msbuild/wpf-msbuild-task-reference.md)   
 [MSBuild 引用](../msbuild/msbuild-reference.md)   
 [任务引用](../msbuild/msbuild-task-reference.md)   
 [生成 wpf 应用程序 (WPF) ](https://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)   
 [WPF XAML 浏览器应用程序概述](https://msdn.microsoft.com/library/3a7a86a8-75d5-4898-96b9-73da151e5e16)
