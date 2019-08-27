---
title: Parameter 元素 | Microsoft Docs
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
- Parameter element [MSBuild]
- <Parameter> element [MSBuild]
ms.assetid: b273afff-b500-4e97-8cfd-31f39fa64a51
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a815d2ef623a35030469fa631cae65653c2fe2d1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68185228"
---
# <a name="parameter-element"></a>Parameter 元素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含某个任务的特定参数信息，该任务可通过使用 `UsingTask``TaskFactory` 生成。  元素的名称就是该参数的名称。  有关详细信息，请参阅 [UsingTask 元素 (MSBuild)](../msbuild/usingtask-element-msbuild.md)。  
  
 \<Project>  
 \<UsingTask>  
 \<ParameterGroup>  
 \<Parameter>  
  
## <a name="syntax"></a>语法  
  
```  
<ParameterGroup ParameterType="SystemType"  
    Output="true/false"  
    Required="true/false" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|说明|  
|---------------|-----------------|  
|`ParameterType`|可选特性。<br /><br /> 参数的.NET 类型，例如，“System.String”。|  
|`Output`|可选布尔属性。<br /><br /> 如果值为 `true`，该参数是任务的输出参数。 默认情况下，该值为 `false`。|  
|`Required`|可选布尔属性。<br /><br /> 如果值为 `true`，该参数是任务的必需参数。 默认情况下，该值为 `false`。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|说明|  
|-------------|-----------------|  
|[ParameterGroup](../msbuild/parametergroup-element.md)|包含一系列可选参数，这些参数将显示在通过使用 `UsingTask``TaskFactory` 生成的任务上。|  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用 `Parameter` 元素。  
  
```  
<UsingTask TaskName="MyTask" AssemblyName="My.Assembly" TaskFactory="MyTaskFactory">  
       <ParameterGroup>  
              <Parameter1 ParameterType="System.String" Required="False" Output="False"/>  
              <Parameter2 ParameterType="System.Int" Required="True" Output="False"/>  
             ...  
</ParameterGroup>  
       <TaskBody Evaluate="true">  
      ... Task factory-specific data ...  
       </TaskBody>  
</UsingTask>  
```  
  
## <a name="see-also"></a>另请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)   
 [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
