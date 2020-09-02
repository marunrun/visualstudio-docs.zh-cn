---
title: Output 元素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Output
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- <Output> Element [MSBuild]
- Output Element [MSBuild]
ms.assetid: 34bc7cd1-efd3-4b57-b691-4584eeb6a0e9
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 52b8ef11e295d60e71a59820a48bca5e477c639d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68163599"
---
# <a name="output-element-msbuild"></a>Output 元素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

存储项和属性中的任务输出值。  
  
 \<Project>  
 \<Target>  
 \<Task>  
 \<Output>  
  
## <a name="syntax"></a>语法  
  
```  
<Output TaskParameter="Parameter"  
    PropertyName="PropertyName"   
    Condition = "'String A' == 'String B'" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`TaskParameter`|必需的特性。<br /><br /> 任务输出参数的名称。|  
|`PropertyName`|`PropertyName` 或 `ItemName` 特性是必需的。<br /><br /> 接收任务输出参数值的属性。 然后，你的项目可引用具有 `$(` *PropertyName* `)` 语法的属性。 此属性名称可以是新属性名称，也可以是项目中已定义的名称。<br /><br /> 在已使用 `ItemName` 的情况下，不能使用该特性。|  
|`ItemName`|`PropertyName` 或 `ItemName` 特性是必需的。<br /><br /> 接收任务输出参数值的项。 然后，你的项目可引用具有项目的语法的项 `@(` *ItemName* `)` 。 项名称可以是新项名称，也可以是项目中已定义的名称。<br /><br /> 在已使用 `PropertyName` 的情况下，不能使用该特性。|  
|`Condition`|可选特性。<br /><br /> 要计算的条件。 有关详细信息，请参阅[条件](../msbuild/msbuild-conditions.md)。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Task](../msbuild/task-element-msbuild.md)|创建并执行的 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 任务的实例。|  
  
## <a name="example"></a>示例  
 以下代码示例演示在 `Target` 元素中执行的 `Csc` 任务。 传递给任务参数的项和属性在本示例外部声明。 来自输出参数 `OutputAssembly` 的值存储在 `FinalAssemblyName` 项中，来自输出参数 `BuildSucceeded` 的值存储在 `BuildWorked` 属性中。 有关详细信息，请参阅[任务](../msbuild/msbuild-tasks.md)。  
  
```  
<Target Name="Compile" DependsOnTargets="Resources">  
    <Csc  Sources="@(CSFile)"  
            TargetType="library"  
            Resources="@(CompiledResources)"  
            EmitDebugInformation="$(includeDebugInformation)"  
            References="@(Reference)"  
            DebugType="$(debuggingType)"  
            OutputAssembly="$(builtdir)\$(MSBuildProjectName).dll" >  
        <Output TaskParameter="OutputAssembly"  
                  ItemName="FinalAssemblyName" />  
        <Output TaskParameter="BuildSucceeded"  
                  PropertyName="BuildWorked" />  
    </Csc>  
</Target>  
```  
  
## <a name="see-also"></a>另请参阅  
 [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)   
 [任务](../msbuild/msbuild-tasks.md)
