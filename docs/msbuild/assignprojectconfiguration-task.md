---
title: AssignProjectConfiguration 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 09633a0b-8f6f-4aba-8058-7cb4d13ce2c0
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 95f61858bfcdf0f54c4f786e1b1064707b57c68c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593442"
---
# <a name="assignprojectconfiguration-task"></a>AssignProjectConfiguration 任务
此任务接受列表配置字符串，并将其分配给指定的项目。

## <a name="task-parameters"></a>任务参数
 下表描述了 `AssignProjectConfiguration` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`SolutionConfigurationContents`|可选 `string` 输出参数。<br /><br /> 包含 XML 字符串，该字符串包含每个项目的项目配置。 这些配置分配给已命名的项目。|
|`DefaultToVcxPlatformMapping`|可选 `string` 输出参数。<br /><br /> 包含以分号分隔的映射列表，这些映射是从大多数类型使用的平台名称到 .vcxproj 文件使用的平台名称的映射  。<br /><br /> 例如：<br /><br /> `"AnyCPU=Win32;X86=Win32;X64=X64"`|
|`VcxToDefaultPlatformMapping`|可选<br /><br /> `string` 输出参数。<br /><br /> 包含以分号分隔的映射列表，这些映射是从 .vcxproj 平台名称到由大多数类型所使用的平台名称的映射  。<br /><br /> 例如：<br /><br /> `"Win32=AnyCPU;X64=X64"`|
|`CurrentProjectConfiguration`|可选 `string` 输出参数。<br /><br /> 包含当前项目的配置。|
|`CurrentProjectPlatform`|可选 `string` 输出参数。<br /><br /> 包含当前项目的平台。|
|`OnlyReferenceAndBuildProjectsEnabledInSolutionConfiguration`|可选 `bool` 输出参数。<br /><br /> 包含指示应生成引用（即使在项目配置中禁用引用）的标志。|
|`ShouldUnsetParentConfigurationAndPlatform`|可选 `bool` 输出参数。<br /><br /> 包含指示是否应取消设置父级配置和平台的标志。|
|`OutputType`|可选 `string` 输出参数。<br /><br /> 包含项目的输出类型。|
|`ResolveConfigurationPlatformUsingMappings`|可选 `bool` 输出参数。<br /><br /> 包含指示生成是否应使用默认映射来解析项目引用中传递的配置和平台的标志。|
|`AssignedProjects`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含解析引用路径的列表。|
|`UnassignedProjects`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含项目引用项的列表，其中这些项无法使用输出的预解析列表进行解析。|

## <a name="remarks"></a>备注
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>请参阅
- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
