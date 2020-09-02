---
title: MSBuild 目标 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
helpviewer_keywords:
- MSBuild, targets
ms.assetid: 8060b4d2-e4a9-48cf-a437-852649ceb417
caps.latest.revision: 29
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c4cc8d9654fc2d277f0b7c69483ab46aa3209983
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157614"
---
# <a name="msbuild-targets"></a>MSBuild 目标
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

目标以特定的顺序将任务组合到一起，并允许生成过程分解为较小的单位。 例如，一个目标可能会删除输出目录中的所有文件以准备进行生成，而另一个目标可能会编译项目的输入并将它们置于该空目录中。 有关任务的详细信息，请参阅[任务](../msbuild/msbuild-tasks.md)。  
  
## <a name="declaring-targets-in-the-project-file"></a>在项目文件中声明目标  
 目标是通过 [Target](../msbuild/target-element-msbuild.md) 元素在项目文件中声明的。 例如，以下 XML 创建一个名为 Construct 的目标，然后，该目标通过 Compile 项类型调用 Csc 任务。  
  
```  
<Target Name="Construct">  
    <Csc Sources="@(Compile)" />  
</Target>  
```  
  
 与 MSBuild 属性一样，可以重新定义目标。 例如，应用于对象的  
  
```  
<Target Name="AfterBuild" >  
    <Message Text="First occurrence" />  
</Target>  
<Target Name="AfterBuild" >  
    <Message Text="Second occurrence" />  
</Target>  
```  
  
 如果 AfterBuild 执行，则仅显示“第二个匹配项”。  
  
## <a name="target-build-order"></a>目标生成顺序  
 如果目标的输入取决于另一目标的输出，那么必须将目标排序。 可以通过多种方法指定目标的运行顺序。  
  
- 初始目标  
  
- 默认目标  
  
- 第一个目标  
  
- 目标依赖项  
  
- `BeforeTargets` 和 `AfterTargets` (MSBuild 4.0)  
  
  目标决不会在一个生成过程中运行两次，即使在生成中有后续目标依赖于该目标。 目标运行后，其在生成中的任务就已完成。  
  
  有关目标生成顺序的详细信息和详细信息，请参阅 [目标生成顺序](../msbuild/target-build-order.md)。  
  
## <a name="target-batching"></a>目标批处理  
 目标元素可能具有 `Outputs` 特性，该特性指定 %(元数据) 形式的元数据。 如果是这样，MSBuild 将针对每个唯一元数据值运行一次目标，对具有该元数据值的项进行分组或“批处理”。 例如，应用于对象的  
  
```  
<ItemGroup>  
    <Reference Include="System.Core">  
      <RequiredTargetFramework>3.5</RequiredTargetFramework>  
    </Reference>  
    <Reference Include="System.Xml.Linq">  
      <RequiredTargetFramework>3.5</RequiredTargetFramework>  
    </Reference>  
    <Reference Include="Microsoft.CSharp">  
      <RequiredTargetFramework>4.0</RequiredTargetFramework>  
    </Reference>  
</ItemGroup>  
<Target Name="AfterBuild"  
    Outputs="%(Reference.RequiredTargetFramework)">  
    <Message Text="Reference:  
      @(Reference->'%(RequiredTargetFramework)')" />  
</Target>  
```  
  
 按 Reference 项的 RequiredTargetFramework 元数据对其进行批处理。 目标的输出如下所示：  
  
```  
Reference: 3.5;3.5  
Reference: 4.0  
```  
  
 实际生成中很少使用目标批处理。 任务批处理更为常见。 有关详细信息，请参阅[批处理](../msbuild/msbuild-batching.md)。  
  
## <a name="incremental-builds"></a>增量生成  
 增量生成是经过优化的生成。优化后，如果目标所含输出文件相对于其相应的输入文件保持为最新，则系统不会执行该目标。 目标元素既可以具有 `Inputs` 特性（指示目标预计作为输入的项），也可以具有 `Outputs` 特性（指示目标作为输出所生成的项）。  
  
 如果所有输出项都是最新的，则 MSBuild 将跳过目标，这可以显著加快生成速度。 这称为目标的增量生成。 如果只有部分文件为最新，则 MSBuild 将执行不包含最新项的目标。 这称为目标的部分增量生成。 有关详细信息，请参阅[增量生成](../msbuild/incremental-builds.md)。  
  
## <a name="see-also"></a>另请参阅  
 [MSBuild 概念](../msbuild/msbuild-concepts.md)   
 [如何：在多个项目文件中使用同一目标](../msbuild/how-to-use-the-same-target-in-multiple-project-files.md)
