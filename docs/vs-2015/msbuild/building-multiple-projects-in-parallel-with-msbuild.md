---
title: 用 MSBuild 并行生成多个项目 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- parallel project builds
- building multiple projects in parallel
- msbuild, building projects in parallel
ms.assetid: c8c9aadc-33ad-4aa1-b07d-b879e9eabda0
caps.latest.revision: 23
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f80f0898167de133d78d27d26f97d0ab8ced0b31
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75843950"
---
# <a name="building-multiple-projects-in-parallel-with-msbuild"></a>用 MSBuild 并行生成多个项目
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过 MSBuild，可通过并行运行多个项目来更快地生成它们。 若要并行运行生成，请在一台多核或多处理器计算机上采用以下设置：  
  
- 在命令提示符处使用 `/maxcpucount` 开关。  
  
- 在 MSBuild 任务中使用 <xref:Microsoft.Build.Tasks.MSBuild.BuildInParallel%2A> 任务参数。  
  
> [!NOTE]
> 命令行中的 **/verbosity** ( **/v**) 开关也会影响生成性能。 如果将生成日志信息的详细级别设置为详细或诊断以用于疑难解答，生成性能可能会降低。 有关详细信息，请参阅[获取生成日志](../msbuild/obtaining-build-logs-with-msbuild.md)和[命令行引用](../msbuild/msbuild-command-line-reference.md)。  
  
## <a name="maxcpucount-switch"></a>/maxcpucount 开关  
 如果使用 `/maxcpucount` 开关（简写为 `/m`），MSBuild 将可以创建指定数量的能够并行运行的 MSBuild.exe 进程。 这些进程也称为“辅助进程”。 每个工作进程使用单独的核心或处理器（若有），以便在其他可用处理器可能生成其他项目的同时生成项目。 例如，如果将此开关的值设置为“4”，MSBuild 将创建 4 个辅助进程来生成项目。  
  
 如果包含 `/maxcpucount` 开关而没有指定值，MSBuild 将使用计算机上的处理器总数作为其值。  
  
 有关 MSBuild 3.5 中引入的此开关的详细信息，请参阅[命令行引用](../msbuild/msbuild-command-line-reference.md)。  
  
 下面的示例指示 MSBuild 使用 3 个辅助进程。 如果使用此配置，MSBuild 可以同时生成三个项目。  
  
```  
msbuild.exe myproj.proj /maxcpucount:3  
```  
  
## <a name="buildinparallel-task-parameter"></a>BuildInParallel 任务参数  
 `BuildInParallel` 是 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 任务上的可选布尔参数。 当 `BuildInParallel` 设置为 `true`（默认值）时，会生成多个工作进程以尽可能同时生成多个项目。 为使此操作能够正常进行，`/maxcpucount` 开关必须设置为一个大于 1 的值，并且系统必须至少为双核或具有两个或多个处理器。  
  
 以下是一个来自 microsoft.common.targets 的有关如何设置 `BuildInParallel` 参数的示例。  
  
```  
<PropertyGroup>  
    <BuildInParallel Condition="'$(BuildInParallel)' ==   
        ''">true</BuildInParallel>  
</PropertyGroup>  
<MSBuild  
    Projects="@(_MSBuildProjectReferenceExistent)"  
    Targets="GetTargetPath"  
    BuildInParallel="$(BuildInParallel)"  
    Properties="%(_MSBuildProjectReferenceExistent.SetConfiguration);   
        %(_MSBuildProjectReferenceExistent.SetPlatform)"  
    Condition="'@(NonVCProjectReference)'!='' and   
        ('$(BuildingSolutionFile)' == 'true' or   
        '$(BuildingInsideVisualStudio)' == 'true' or   
        '$(BuildProjectReferences)' != 'true') and     
        '@(_MSBuildProjectReferenceExistent)' != ''"  
    ContinueOnError="!$(BuildingProject)">  
    <Output TaskParameter="TargetOutputs"   
        ItemName="_ResolvedProjectReferencePaths"/>  
</MSBuild>  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用多个处理器生成项目](../msbuild/using-multiple-processors-to-build-projects.md)   
 [编写可识别多处理器的记录器](../msbuild/writing-multi-processor-aware-loggers.md)   
 [“调整的 C++ 并行生成功能”博客](https://blogs.msdn.com/b/visualstudio/archive/2010/03/08/tuning-c-build-parallelism-in-vs2010.aspx)
