---
title: 目标批处理中的项元数据 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- batching [MSBuild]
- MSBuild, target batching
- target batching [MSBuild]
ms.assetid: f3cc4186-6a4c-4161-bbe5-1ec638b4925b
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9dd6c297e00a305fbd1b13cf0fe0bd4a4f151f6b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192875"
---
# <a name="item-metadata-in-target-batching"></a>目标批处理中的项元数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 能够对生成目标的输入和输出执行依赖项分析。 如果确定了目标的输入或输出是最新的，将跳过该目标并继续生成过程。 `Target` 元素使用 `Inputs` 和 `Outputs` 属性指定要在依赖项分析过程中检查的项。  
  
 如果目标包含使用批处理的项作为输入或输出的任务，该目标的 `Target` 元素应在其 `Inputs` 或 `Outputs` 属性中使用批处理，以便 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 能够跳过最新的项批。  
  
## <a name="batching-targets"></a>批处理目标  
 下面的示例包含名为 `Res` 的项列表，该列表根据 `Culture` 项元数据划分为两个批。 其中每个批分别传递到 `AL` 任务中，该任务为每个批创建一个输出程序集。 通过对 `Target` 元素的 `Outputs` 属性使用批处理，[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 可在运行目标之前确定各个批是否是最新的。 如果不使用目标批处理，在每次执行目标时，任务都会运行这两个项批。  
  
```  
<Project  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <Res Include="Strings.fr.resources">  
            <Culture>fr</Culture>  
        </Res>  
        <Res Include="Strings.jp.resources">  
            <Culture>jp</Culture>  
        </Res>  
        <Res Include="Menus.fr.resources">  
            <Culture>fr</Culture>  
        </Res>  
        <Res Include="Dialogs.fr.resources">  
            <Culture>fr</Culture>  
        </Res>  
        <Res Include="Dialogs.jp.resources">  
            <Culture>jp</Culture>  
        </Res>  
        <Res Include="Menus.jp.resources">  
            <Culture>jp</Culture>  
        </Res>  
    </ItemGroup>  
  
    <Target Name="Build"  
        Inputs="@(Res)"  
        Outputs="%(Culture)\MyApp.resources.dll">  
  
        <AL Resources="@(Res)"  
            TargetType="library"  
            OutputAssembly="%(Culture)\MyApp.resources.dll"  
  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>另请参阅  
 [如何：增量生成](../msbuild/how-to-build-incrementally.md)   
 [批处理](../msbuild/msbuild-batching.md)   
 [目标元素 (MSBuild) ](../msbuild/target-element-msbuild.md)   
 [任务批处理中的项元数据](../msbuild/item-metadata-in-task-batching.md)
