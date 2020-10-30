---
title: CombinePath 任务 | Microsoft Docs
description: 了解如何使用 MSBuild CombinePath 任务将指定路径合并到单个路径中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, CombinePath task
- CombinePath task [MSBuild]
ms.assetid: c20edbf4-3d4f-4f66-b1d5-753a0d858ed8
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dc33c3a413d788bd9a5a30a7db69c4c7766a3392
ms.sourcegitcommit: bd9417123c6ef67aa2215307ba5eeec511e43e02
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92796610"
---
# <a name="combinepath-task"></a>CombinePath 任务

将指定路径合并到单个路径。
## <a name="task-parameters"></a>任务参数

 下表描述了 [CombinePath 任务](../msbuild/combinepath-task.md)的参数。


|参数|描述|
|---------------|-----------------|
|`BasePath`|必选 `String` 参数。<br /><br /> 与其他路径组合的基路径。 可以是相对路径、绝对路径或空白。|
|`Paths`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 要与 BasePath 组合成组合路径的各个路径的列表。 路径可以是相对路径，也可以是绝对路径。|
|`CombinedPaths`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 由此任务创建的组合路径。|

## <a name="remarks"></a>备注

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

 下面的示例演示如何使用 `CombinePath` 创建输出文件夹结构，通过结合连接到 `$(ReleaseDirectory)` 的根路径 `$(PublishRoot)` 和子文件夹列表 `$(LangDirectories)` 来构造属性 `$(OutputDirectory)`。

 ```xml
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp3.1</TargetFramework>
    <PublishRoot>C:\Site1\Release</PublishRoot>
  </PropertyGroup>

  <ItemGroup>
    <LangDirectories Include="en-us\;fr-fr\"/>
  </ItemGroup>

  <Target Name="CreateOutputDirectories" AfterTargets="Build">
    <CombinePath BasePath="$(PublishRoot)" Paths="@(LangDirectories)" >
      <Output TaskParameter="CombinedPaths" ItemName="OutputDirectories"/>
    </CombinePath>
    <MakeDir Directories="@(OutputDirectories)" />
  </Target>
```

`CombinePath` 允许作为列表的唯一属性是 `Paths`，在此情况下，输出也是一个列表。 因此，如果 `$(PublishRoot)` 是 C:\Site1\\，`$(ReleaseDirectory)` 是 Release\\，`@(LangDirectories)` 是 en-us\;fr-fr\\，则此示例将创建文件夹：

- C:\Site1\Release\en-us\
- C:\Site1\Release\fr-fr\

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
