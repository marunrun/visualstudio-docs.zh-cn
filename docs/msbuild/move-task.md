---
title: 移动任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, Move task
- Move task [MSBuild]
ms.assetid: d1405347-1309-4f18-b565-905408093d59
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 05b9f83fa7c80769ea3c584e2885c8fb1db24176
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77633455"
---
# <a name="move-task"></a>Move 任务

将文件移至新位置。

## <a name="parameters"></a>参数

 下表描述了 `Move` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`DestinationFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 指定要将源文件移动到的文件的列表。 此列表应与 `SourceFiles` 参数中指定的列表具有一对一的映射关系。 也就是说，`SourceFiles` 中指定的第一个文件将移动到 `DestinationFiles` 中指定的第一个位置，依次类推。|
|`DestinationFolder`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定要将文件移动到的目录。|
|`MovedFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含已成功移动的项。|
|`OverwriteReadOnlyFiles`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则覆盖文件，即使它们标记为只读文件。|
|`SourceFiles`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要移动的文件。|

## <a name="remarks"></a>备注

 必须指定 `DestinationFolder` 参数或 `DestinationFiles` 参数，但不能对两者都进行指定。 如果指定了两者，则任务失败并记录一条错误。

 `Move` 任务根据需要为所需的目标文件创建文件夹。

 除了具有表中列出的参数外，此任务还将从本身继承自 <xref:Microsoft.Build.Utilities.Task> 类的 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
