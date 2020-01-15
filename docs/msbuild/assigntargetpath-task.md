---
title: AssignTargetPath 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 0e830e31-3bcf-4259-b2a8-a5df49b92d51
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 41a32b914cab8626df513994a3d68c2aac3d7cb7
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593429"
---
# <a name="assigntargetpath-task"></a>AssignTargetPath 任务
此任务接受文件列表，并添加 `<TargetPath>` 属性（如果尚未指定）。

## <a name="task-parameters"></a>任务参数
下表描述了 `AssignTargetPath` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`RootFolder`|可选的 `string` 输入参数。<br /><br /> 包含文件夹的路径，该文件夹包含目标链接。|
|`Files`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输入参数。<br /><br /> 包含传入的文件列表。|
|`AssignedFiles`|可选<br /><br /> <xref:Microsoft.Build.Framework.ITaskItem> `[]` 输出参数。<br /><br /> 包含生成的文件列表。|

## <a name="remarks"></a>备注
除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="example"></a>示例
下例执行 `AssignTargetPath` 任务以对项目进行配置。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <Target Name="MyProject">
        <AssignTargetPath
RootFolder="Resources"
            Files="@(ResourceFiles)"
            <Output TaskParameter="AssignedFiles"
                ItemName="OutAssignedFiles"/>
        </AssignTargetPath>
    </Target>
</Project>
```

## <a name="see-also"></a>请参阅
- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
