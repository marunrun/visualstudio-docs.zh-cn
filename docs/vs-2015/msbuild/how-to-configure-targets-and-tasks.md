---
title: 如何：配置目标和任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
ms.assetid: 92814100-392a-471d-96fd-e26f637d6cc2
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c8ef52638858160822fcc271a53513b130afc3f4
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440043"
---
# <a name="how-to-configure-targets-and-tasks"></a>如何；配置目标和任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可将所选的 MSBuild 任务设置为在其目标环境中运行，而不考虑开发计算机的环境。 例如，当使用 64 位计算机生成面向 32 位体系结构的应用程序时，将在 32 位进程中运行所选的任务。  
  
> [!NOTE]
> 如果生成任务采用 .NET 语言（例如 Visual C# 或 Visual Basic）编写，并且不使用本机资源或工具，则该任务无需修改便可在任何目标上下文中运行。  
  
## <a name="usingtask-attributes-and-task-parameters"></a>UsingTask 属性和 Task 参数  
 以下 `UsingTask` 属性影响特定生成过程中任务的所有操作：  
  
- `Runtime` 属性（如果存在）可设置公共语言运行时 (CLR) 版本，并可采用以下值之一：`CLR2`、`CLR4`、`CurrentRuntime` 或 `*`（任何运行时）。  
  
- `Architecture` 属性（如果存在）可设置平台和位数，并可采用以下值之一：`x86`、`x64`、`CurrentArchitecture` 或 `*`（任何体系结构）。  
  
- `TaskFactory` 属性（如果存在）可设置创建和运行任务实例的任务工厂，并仅使用值 `TaskHostFactory`。 有关详细信息，请参阅本白皮书后面的“任务工厂”一节。  
  
```  
<UsingTask TaskName="SimpleTask"   
   Runtime="CLR2"  
   Architecture="x86"  
   AssemblyFile="$(MSBuildToolsPath)\Microsoft.Build.Tasks.v3.5.dll" />  
```  
  
 还可以使用 `MSBuildRuntime` 和 `MSBuildArchitecture` 参数来设置单个任务的目标上下文。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   <Target Name="MyTarget">  
      <SimpleTask MSBuildRuntime="CLR2" MSBuildArchitecture= "x86"/>  
   </Target>  
</Project>  
```  
  
 在 MSBuild 运行任务之前，它将查找具有相同目标上下文的匹配 `UsingTask`。  在 `UsingTask` 中指定的参数（但不在相应的任务中）视为要进行匹配的参数。  在任务中指定的参数（但不在相应的 `UsingTask` 中）也视为要进行匹配的参数。 如果未在 `UsingTask` 或任务中指定参数值，则该值将默认为 `*`（任何参数）。  
  
> [!WARNING]
> 如果存在多个 `UsingTask` 且它们都具有匹配的 `TaskName`、`Runtime` 和 `Architecture` 属性，则要进行评估的最后一个值将替换其他值。  
  
 如果对任务设置参数，则 MSBuild 将尝试查找匹配这些参数或至少不与这些参数冲突的 `UsingTask`。  多个 `UsingTask` 可指定具有相同任务的目标上下文。  例如，针对不同的目标环境具有不同的可执行文件的任务可能类似于：  
  
```  
<UsingTask TaskName="MyTool"   
   Runtime="CLR2"  
   Architecture="x86"  
   AssemblyFile="$(MyToolsPath)\MyTool.v2.0.dll" />  
  
<UsingTask TaskName="MyTool"   
   Runtime="CLR4"  
   Architecture="x86"  
   AssemblyFile="$(MyToolsPath)\MyTool.4.0.dll" />  
  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   <Target Name="MyTarget">  
      <MyTool MSBuildRuntime="CLR2" MSBuildArchitecture= "x86"/>  
   </Target>  
</Project>  
  
```  
  
## <a name="task-factories"></a>任务工厂  
 在其运行任务之前，MSBuild 将检查该任务是否指定为在当前软件上下文中运行。  如果该任务指定为在当前软件上下文中运行，则 MSBuild 将其传递给 AssemblyTaskFactory（它在当前进程中运行该任务）；否则，MSBuild 将其传递给 TaskHostFactory（它在匹配目标上下文的进程中运行该任务）。 即使当前上下文和目标上下文互相匹配，也可以通过将 `TaskFactory` 设置为 `TaskHostFactory`，强制任务在进程外运行（出于隔离、安全性或其他原因）。  
  
```  
<UsingTask TaskName="MisbehavingTask"   
   TaskFactory="TaskHostFactory"  
   AssemblyFile="$(MSBuildToolsPath)\MyTasks.dll">  
</UsingTask>  
```  
  
## <a name="phantom-task-parameters"></a>虚拟任务参数  
 与任何其他任务参数类似，可以从生成属性设置 `MSBuildRuntime` 和 `MSBuildArchitecture`。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   <PropertyGroup>  
      <FrameworkVersion>3.0</FrameworkVersion>  
   </PropertyGroup>  
   <Target Name="MyTarget">  
      <SimpleTask MSBuildRuntime="$(FrameworkVerion)" MSBuildArchitecture= "x86"/>  
   </Target>  
</Project>  
```  
  
 与其他任务参数不同，`MSBuildRuntime` 和 `MSBuildArchitecture` 并不对任务本身显示。  若要编写可识别其运行的上下文的任务，必须通过调用 .NET Framework 来测试上下文，或使用生成属性通过其他任务参数来传递上下文信息。  
  
> [!NOTE]
> 可通过工具集和环境属性设置 `UsingTask` 特性。  
  
 `MSBuildRuntime` 和 `MSBuildArchitecture` 参数提供设置目标上下文的最灵活方式，但其范围也最受限制。  一方面，因为这些参数是在任务实例本身上设置的，并在任务运行之前不会进行计算，因此可从计算时和生成时都可用的全部属性范围中派生其值。  另一方面，这些参数仅适用于特定目标中任务的特定实例。  
  
> [!NOTE]
> 任务参数在父节点的上下文中，而不是任务主机的上下文中进行计算；运行时相关或体系结构相关的环境变量（例如程序文件位置）将计算为与该父节点匹配的值。  但是，如果同一个环境变量直接由任务读取，则它会在任务主机的上下文中正确计算。  
  
## <a name="see-also"></a>请参阅  
 [配置目标和任务](../msbuild/configuring-targets-and-tasks.md)
