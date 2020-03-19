---
title: Project 元素 (MSBuild) | Microsoft Docs
ms.date: 03/13/2017
ms.topic: reference
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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: df9eff3e941cc21aaa71c2779a72084e12e8e590
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77632974"
---
# <a name="project-element-msbuild"></a>Project 元素 (MSBuild)

MSBuild 项目文件必需的根元素。

## <a name="syntax"></a>语法

```xml
<Project InitialTargets="TargetA;TargetB"
         DefaultTargets="TargetC;TargetD"
         TreatAsLocalProperty="PropertyA;PropertyB"
         ToolsVersion=<version number>
         Sdk="name[/version]"
         xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Sdk... />
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

| 特性 | 描述 |
|------------------------| - |
| `DefaultTargets` | 可选特性。<br /><br /> 如果未指定目标，则默认目标将作为生成的入口点。 使用分号 (;) 分隔多个目标。<br /><br /> 如果未在 `DefaultTargets` 属性或 MSBuild 命令行中指定默认目标，那么引擎会在评估 [Import](../msbuild/import-element-msbuild.md) 元素后在项目文件中执行第一个目标。 |
| `InitialTargets` | 可选特性。<br /><br /> 会在 `DefaultTargets` 属性中或命令行上指定的目标前运行初始目标。 使用分号 (`;`) 分隔多个目标。 如果多个导入文件定义 `InitialTargets`，则将按照导入的顺序运行所有提到的目标。 |
| `Sdk` | 可选特性。 <br /><br /> 用于创建添加到 .proj 文件的隐式 Import 语句的 SDK 名称和可选版本。 如果不指定任何版本，则 MSBuild 将尝试解析默认版本。  例如，`<Project Sdk="Microsoft.NET.Sdk" />` 或 `<Project Sdk="My.Custom.Sdk/1.0.0" />`。 |
| `ToolsVersion` | 可选特性。<br /><br /> 用于确定 $(MSBuildBinPath) 和 $(MSBuildToolsPath) 的值的工具集 MSBuild 的版本。 |
| `TreatAsLocalProperty` | 可选特性。<br /><br /> 不会被视为全局的属性名称。 此属性可防止特定命令行属性替代项目或目标文件和所有后续导入中设置的属性值。 使用分号 (;) 分隔多个属性。<br /><br /> 通常，全局属性会替代项目或文件中设置的属性值。 如果该属性在 `TreatAsLocalProperty` 值中列出，那么全局属性值不会替代在该文件或任何后续导入中设置的属性值。 有关详细信息，请参阅[如何：使用不同选项生成相同的源文件](../msbuild/how-to-build-the-same-source-files-with-different-options.md)。 **注意：** 可使用“-property”（或“-p”）开关，在命令提示符处设置全局属性   。 还可使用 MSBuild 任务的 `Properties` 属性为多项目生成中的子项目设置或修改全局属性。 有关详细信息，请参阅 [MSBuild 任务](../msbuild/msbuild-task.md)。 |
| `xmlns` | 可选特性。<br /><br /> 指定后，`xmlns` 属性必须具有 `http://schemas.microsoft.com/developer/msbuild/2003` 值。 |

### <a name="child-elements"></a>子元素

| 元素 | 描述 |
| - | - |
| [Choose](../msbuild/choose-element-msbuild.md) | 可选元素。<br /><br /> 评估子元素，选择一组 `ItemGroup` 元素和/或 `PropertyGroup` 元素进行评估。 |
| [Import](../msbuild/import-element-msbuild.md) | 可选元素。<br /><br /> 启用项目文件，导入另一项目文件。 项目中可能有零个或零个以上的 `Import` 元素。 |
| [ImportGroup](../msbuild/importgroup-element.md) | 可选元素。<br /><br /> 包含在可选条件下进行分组的 `Import` 元素的集合。 |
| [ItemGroup](../msbuild/itemgroup-element-msbuild.md) | 可选元素。<br /><br /> 各个项的分组元素。 使用 [Item](../msbuild/item-element-msbuild.md) 元素指定项。 项目中可能有零个或零个以上的 `ItemGroup` 元素。 |
| [ItemDefinitionGroup](../msbuild/itemdefinitiongroup-element-msbuild.md) | 可选元素。<br /><br /> 可定义一组项定义，这些项定义默认为应用到项目中的所有项的元数据值。 ItemDefinitionGroup 取代使用 `CreateItem` 任务和 `CreateProperty` 任务。 |
| [ProjectExtensions](../msbuild/projectextensions-element-msbuild.md) | 可选元素。<br /><br /> 提供在 MSBuild 项目文件中保留非 MSBuild 信息的方法。 项目中可能有零个或一个 `ProjectExtensions` 元素。 |
| [PropertyGroup](../msbuild/propertygroup-element-msbuild.md) | 可选元素。<br /><br /> 各个属性的分组元素。 使用 [Property](../msbuild/property-element-msbuild.md) 元素指定属性。 项目中可能有零个或零个以上的 `PropertyGroup` 元素。 |
| [SDK](../msbuild/sdk-element-msbuild.md) | 可选元素。<br /><br /> 引用 MSBuild 项目 SDK。  此元素可以用作 SDK 属性的替代属性。 |
| [Target](../msbuild/target-element-msbuild.md) | 可选元素。<br /><br /> 包含一组要连续执行的 MSBuild 任务。 使用 [Task](../msbuild/task-element-msbuild.md) 元素指定任务。 项目中可能有零个或零个以上的 `Target` 元素。 |
| [UsingTask](../msbuild/usingtask-element-msbuild.md) | 可选元素。<br /><br /> 提供在 MSBuild 中注册任务的方法。 项目中可能有零个或零个以上的 `UsingTask` 元素。 |

### <a name="parent-elements"></a>父元素

 无。

## <a name="see-also"></a>请参阅

- [如何：指定首先生成的目标](../msbuild/how-to-specify-which-target-to-build-first.md)
- [命令行参考](../msbuild/msbuild-command-line-reference.md)
- [项目文件架构参考](../msbuild/msbuild-project-file-schema-reference.md)
- [MSBuild](../msbuild/msbuild.md)
