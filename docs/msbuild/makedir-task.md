---
title: MakeDir 任务 | Microsoft Docs
description: 了解 MSBuild 如何使用 MakeDir 任务来创建目录和（必要时）任何父目录。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#MakeDir
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MakeDir task [MSBuild]
- MSBuild, MakeDir task
ms.assetid: bc951577-1bfb-4100-b1f1-bc8278c45bf7
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 91be7dc2baf7df36d98cd725e8141cfa9cab773f
ms.sourcegitcommit: f1d47655974a2f08e69704a9a0c46cb007e51589
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92904306"
---
# <a name="makedir-task"></a>MakeDir 任务

创建目录，并在必要时创建任何父目录。

## <a name="parameters"></a>参数

下表描述了 `MakeDir` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`Directories`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 要创建的目录集。|
|`DirectoriesCreated`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 由此任务创建的目录。 如果无法创建某些目录，则其中可能不包含已传递到 `Directories` 参数的所有项。|

## <a name="remarks"></a>备注

除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

以下代码示例使用 `MakeDir` 任务创建由 `OutputDirectory` 属性指定的目录。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <PropertyGroup>
        <OutputDirectory>\Output\</OutputDirectory>
    </PropertyGroup>

    <Target Name="CreateDirectories">
        <MakeDir
            Directories="$(OutputDirectory)"/>
    </Target>

</Project>
```

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
