---
title: 任务元素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Task element [MSBuild]
- <Task> element [MSBuild]
ms.assetid: d82e2485-e5f0-4936-a357-745bacccc299
caps.latest.revision: 26
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6683aac3c5a4314df6fde3d72dd9085b6608d8a3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68202269"
---
# <a name="task-element-msbuild"></a>Task 元素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

创建并执行的 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 任务的实例。 元素名称由正在创建的任务名称确定。  
  
 \<Project>  
 \<Target>  
  
## <a name="syntax"></a>语法  
  
```  
<Task Parameter1="Value1"... ParameterN="ValueN"  
    ContinueOnError="WarnAndContinue/true/ErrorAndContinue/ErrorAndStop/false"  
    Condition="'String A' == 'String B'" >  
    <Output... />  
</Task>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`Condition`|可选特性。 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|  
|`ContinueOnError`|可选特性。 可以包含下列值之一：<br /><br /> -   **WarnAndContinue** 或 **true**。 当任务失败时，[Target](../msbuild/target-element-msbuild.md) 元素中的后续任务和生成将继续执行，并且来自该任务的所有错误都被视为警告。<br />-   **ErrorAndContinue**。 当任务失败时，`Target` 元素中的后续任务和生成将继续执行，并且来自该任务的所有错误都被视为错误。<br />-   **ErrorAndStop** 或 **false**（默认值）。 当任务失败时，将不会执行 `Target` 元素中的剩余任务和生成，并且整个 `Target` 元素和生成都被视为已失败。<br /><br /> 4\.5 之前的 .NET Framework 版本仅支持 `true` 和 `false` 值。<br /><br /> 有关详细信息，请参阅[如何：忽略任务中的错误](../msbuild/how-to-ignore-errors-in-tasks.md)。|  
|`Parameter`|如果任务类包含一个或多个标记有 `[Required]` 特性的属性时，它为必需。<br /><br /> 用户定义的任务参数，其中包含作为其值的参数值。 `Task` 元素中可以有任意数量的参数，其中每个特性均映射到任务类中的 .NET 属性。|  
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[输出](../msbuild/output-element-msbuild.md)|将任务的输出存储于项目文件中。 任务中可能有零个或零个以上 `Output` 元素。|  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Target](../msbuild/target-element-msbuild.md)|[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 任务的容器元素。|  
  
## <a name="remarks"></a>备注  
 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目文件中的 `Task` 元素创建任务实例、在其中设置属性并执行它。 `Output` 元素存储属性或项中用于项目文件中其他位置的输出参数。  
  
 如果任务的父 `Target` 元素中存在任何 [OnError](../msbuild/onerror-element-msbuild.md) 元素，当任务失败且 `ContinueOnError` 具有值 `false` 时仍将对该元素评估。 有关任务的详细信息，请参阅[任务](../msbuild/msbuild-tasks.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例创建 [Csc 任务](../msbuild/csc-task.md)类的实例、设置其中 6 个属性并执行任务。 执行任何后，对象的 `OutputAssembly` 属性的值将放入名为 `FinalAssemblyName` 的项列表中。  
  
```  
<Target Name="Compile" DependsOnTarget="Resources" >  
    <Csc Sources="@(CSFile)"  
          TargetType="library"  
          Resources="@(CompiledResources)"  
          EmitDebugInformation="$(includeDebugInformation)"  
          References="@(Reference)"  
          DebugType="$(debuggingType)" >  
        <Output TaskParameter="OutputAssembly"  
                  ItemName="FinalAssemblyName" />  
    </Csc>  
</Target>  
```  
  
## <a name="see-also"></a>请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)   
 [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
