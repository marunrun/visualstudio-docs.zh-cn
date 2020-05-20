---
title: FindUnderPath 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#FindUnderPath
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, FindUnderPath task
- FindUnderPath task [MSBuild]
ms.assetid: 3c6d58b0-36e8-47aa-bfca-b73dd2045d91
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4d97b727dcba8cd16fe97ee33764947797c36db7
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634131"
---
# <a name="findunderpath-task"></a>FindUnderPath 任务

确定指定项集合中的哪些项具有指定文件夹及其子文件夹的路径。

## <a name="parameters"></a>参数

下表描述了 `FindUnderPath` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`Files`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定应将其路径与 `Path` 参数指定的路径进行比较的文件。|
|`InPath`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包括在指定路径下找到的项。|
|`OutOfPath`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包括未在指定路径下找到的项。|
|`Path`|必选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定用作参考的文件夹路径。|
|`UpdateToAbsolutePaths`|可选 `Boolean` 参数。<br /><br /> 如果为 true，则输出项的路径会更新为绝对路径。|

## <a name="remarks"></a>备注

除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例

以下示例使用 `FindUnderPath` 任务确定 `MyFiles` 项中所包含的文件是否具有位于 `SearchPath` 属性指定的路径下的路径。 任务完成后，`FilesNotFoundInPath` 项包含 File1.txt 文件，`FilesFoundInPath` 项包含 File2.txt 文件。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup>
        <MyFiles Include="C:\File1.txt" />
        <MyFiles Include="C:\Projects\MyProject\File2.txt" />
    </ItemGroup>

    <PropertyGroup>
        <SearchPath>C:\Projects\MyProject</SearchPath>
    </PropertyGroup>

    <Target Name="FindFiles">
        <FindUnderPath
            Files="@(MyFiles)"
            Path="$(SearchPath)">
            <Output
                TaskParameter="InPath"
                ItemName="FilesFoundInPath" />
            <Output
                TaskParameter="OutOfPath"
                ItemName="FilesNotFoundInPath" />
        </FindUnderPath>
    </Target>

</Project>
```

## <a name="see-also"></a>另请参阅

- [任务参考](../msbuild/msbuild-task-reference.md)
- [任务](../msbuild/msbuild-tasks.md)
- [MSBuild 概念](../msbuild/msbuild-concepts.md)
