---
title: Project 元素 (MSBuild) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Project
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- ToolsVersion attribute [MSBuild]
- <Project> element [MSBuild]
- Project element [MSBuild]
ms.assetid: d1cda56a-dbef-4109-9201-39e962e3f653
caps.latest.revision: 34
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 132d1c3fbf23433ea89e7dba39bc226bc253b015
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68205650"
---
# <a name="project-element-msbuild"></a>Project 元素 (MSBuild)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目文件必需的根元素。  
  
## <a name="syntax"></a>语法  
  
```  
<Project InitialTargets="TargetA;TargetB"  
         DefaultTargets="TargetC;TargetD"  
         TreatAsLocalProperty="PropertyA;PropertyB"  
         ToolsVersion=<version number>  
         xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Choose>... </Choose>  
    <PropertyGroup>... </PropertyGroup>  
    <ItemGroup>... </ItemGroup>  
    <Target>... </Target>  
    <UsingTask.../>  
    <ProjectExtensions>... </ProjectExtensions>  
    <Import... />  
</Project>  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|       特性        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    `DefaultTargets`    |                                                                                                                                                                                                                                                                                                 可选特性。<br /><br /> 如果未指定目标，则默认目标将作为生成的入口点。 使用分号 (;) 分隔多个目标。<br /><br /> 如果未在 `DefaultTargets` 属性或 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 命令行中指定默认目标，那么引擎会在评估 [Import](../msbuild/import-element-msbuild.md) 元素后在项目文件中执行第一个目标。                                                                                                                                                                                                                                                                                                  |
|    `InitialTargets`    |                                                                                                                                                                                                                                                                                                                                                                                                                                             可选特性。<br /><br /> 会在 `DefaultTargets` 属性中或命令行上指定的目标前运行初始目标。 使用分号 (;) 分隔多个目标。                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|     `ToolsVersion`     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                             可选特性。<br /><br /> 用于确定 $(MSBuildBinPath) 和 $(MSBuildToolsPath) 的值的工具集 MSBuild 的版本。                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| `TreatAsLocalProperty` | 可选特性。<br /><br /> 不会被视为全局的属性名称。 此属性可防止特定命令行属性替代项目或目标文件和所有后续导入中设置的属性值。 使用分号 (;) 分隔多个属性。<br /><br /> 通常，全局属性会替代项目或文件中设置的属性值。 如果该属性在 `TreatAsLocalProperty` 值中列出，那么全局属性值不会替代在该文件或任何后续导入中设置的属性值。 有关详细信息，请参阅[如何：生成相同的源文件使用不同选项](../msbuild/how-to-build-the-same-source-files-with-different-options.md)。 **注意：** 通过在命令提示符处设置全局属性 **/property** (或 **/p**) 切换。 还可使用 MSBuild 任务的 `Properties` 属性为多项目生成中的子项目设置或修改全局属性。 有关详细信息，请参阅 [MSBuild 任务](../msbuild/msbuild-task.md)。 |
|        `Xmlns`         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 必需的特性。<br /><br /> `xmlns`属性必须包含的值"<http://schemas.microsoft.com/developer/msbuild/2003>"。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
  
### <a name="child-elements"></a>子元素  
  
|元素|描述|  
|-------------|-----------------|  
|[Choose](../msbuild/choose-element-msbuild.md)|可选元素。<br /><br /> 评估子元素，选择一组 `ItemGroup` 元素和/或 `PropertyGroup` 元素进行评估。|  
|[Import](../msbuild/import-element-msbuild.md)|可选元素。<br /><br /> 启用项目文件，导入另一项目文件。 项目中可能有零个或零个以上的 `Import` 元素。|  
|[ItemGroup](../msbuild/itemgroup-element-msbuild.md)|可选元素。<br /><br /> 各个项的分组元素。 使用 [Item](../msbuild/item-element-msbuild.md) 元素指定项。 项目中可能有零个或零个以上的 `ItemGroup` 元素。|  
|[ProjectExtensions](../msbuild/projectextensions-element-msbuild.md)|可选元素。<br /><br /> 提供在 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 项目文件中保留非 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 信息的方法。 项目中可能有零个或一个 `ProjectExtensions` 元素。|  
|[PropertyGroup](../msbuild/propertygroup-element-msbuild.md)|可选元素。<br /><br /> 各个属性的分组元素。 使用 [Property](../msbuild/property-element-msbuild.md) 元素指定属性。 项目中可能有零个或零个以上的 `PropertyGroup` 元素。|  
|[Target](../msbuild/target-element-msbuild.md)|可选元素。<br /><br /> 包含一组要连续执行的 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 任务。 使用 [Task](../msbuild/task-element-msbuild.md) 元素指定任务。 项目中可能有零个或零个以上的 `Target` 元素。|  
|[UsingTask](../msbuild/usingtask-element-msbuild.md)|可选元素。<br /><br /> 提供在 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 中注册任务的方法。 项目中可能有零个或零个以上的 `UsingTask` 元素。|  
  
### <a name="parent-elements"></a>父元素  
 无。  
  
## <a name="see-also"></a>请参阅  
 [如何：指定首先生成的目标](../msbuild/how-to-specify-which-target-to-build-first.md)   
 [命令行参考](../msbuild/msbuild-command-line-reference.md)   
 [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)   
 [MSBuild](msbuild.md)
