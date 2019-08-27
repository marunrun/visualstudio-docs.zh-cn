---
title: MSBuild 批处理 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- batching [MSBuild]
- MSBuild, batching
ms.assetid: d35c085b-27b8-49d7-b6f8-8f2f3a0eec38
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d96330c01ab340d4db67694f358717a2dae0bce3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63439366"
---
# <a name="msbuild-batching"></a>MSBuild 批处理
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 能够基于项元数据将项列表划分为不同类别或批，并对每批运行一次目标或任务。  
  
## <a name="task-batching"></a>任务批处理  
 借助任务批处理，可以用某种方式将项列表划分为不同批次，同时将每个批次单独地传递到任务中来简化项目文件。 这意味着项目文件只需要声明一次任务及其特性就可多次运行该任务。  
  
 你指定希望 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 使用其中一个任务特性中的 %(ItemMetaDataName) 表示法对任务执行批处理。 以下示例基于 `Color` 项元数据值将 `Example` 项列表划分为几个批次，并将每个批次单独地传递到 `MyTask` 任务。  
  
> [!NOTE]
> 如果未在任务特性的其他位置引用项列表，或者如果元数据名称可能不明确，则可以使用 %(*ItemCollection.ItemMetaDataName*) 表示法完全限定要用于进行批处理的项元数据值。  
  
```  
<Project  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <Example Include="Item1">  
            <Color>Blue</Color>  
        </Example>  
        <Example Include="Item2">  
            <Color>Red</Color>  
        </Example>  
    </ItemGroup>  
  
    <Target Name="RunMyTask">  
        <MyTask  
            Sources = "@(Example)"  
            Output = "%(Color)\MyFile.txt"/>  
    </Target>  
  
</Project>  
```  
  
 有关更具体的批处理示例，请参阅[任务批处理中的项元数据](../msbuild/item-metadata-in-task-batching.md)。  
  
## <a name="target-batching"></a>目标批处理  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 会先检查目标的输入和输出是否是最新的，然后才运行该目标。 如果输入和输出都是最新的，则跳过该目标。 如果目标内的任务使用批处理，则 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 需要确定每批项的输入和输出是否是最新的。 否则，每次命中目标时，都会执行该目标。  
  
 以下示例通过 %(ItemMetaDataName) 表示法演示包含 `Outputs` 特性的 `Target` 元素。 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 会基于 `Color` 项元数据将 `Example` 项列表划分为几个批次，并分析每个批次的输出文件的时间戳。 如果某个批次的输出不是最新的，则运行目标。 否则，跳过该目标。  
  
```  
<Project  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <ItemGroup>  
        <Example Include="Item1">  
            <Color>Blue</Color>  
        </Example>  
        <Example Include="Item2">  
            <Color>Red</Color>  
        </Example>  
    </ItemGroup>  
  
    <Target Name="RunMyTask"  
        Inputs="@(Example)"  
        Outputs="%(Color)\MyFile.txt">  
        <MyTask  
            Sources = "@(Example)"  
            Output = "%(Color)\MyFile.txt"/>  
    </Target>  
  
</Project>  
```  
  
 有关目标批处理的另一个示例，请参阅[目标批处理中的项元数据](../msbuild/item-metadata-in-target-batching.md)。  
  
## <a name="property-functions-using-metadata"></a>使用元数据的属性函数  
 可通过包括元数据的属性函数控制批处理。 例如，应用于对象的  
  
 `$([System.IO.Path]::Combine($(RootPath),%(Compile.Identity)))`  
  
 使用 <xref:System.IO.Path.Combine%2A> 合并根文件夹路径与编译项路径。  
  
 属性函数可能不会出现在元数据值内。  例如，应用于对象的  
  
 `%(Compile.FullPath.Substring(0,3))`  
  
 是不允许的。  
  
 有关属性函数详细信息，请参阅[属性函数](../msbuild/property-functions.md)。  
  
## <a name="see-also"></a>请参阅  
 [ItemMetadata 元素 (MSBuild)](../msbuild/itemmetadata-element-msbuild.md)   
 [MSBuild 概念](../msbuild/msbuild-concepts.md)   
 [MSBuild 参考](../msbuild/msbuild-reference.md)   
 [高级概念](../msbuild/msbuild-advanced-concepts.md)
