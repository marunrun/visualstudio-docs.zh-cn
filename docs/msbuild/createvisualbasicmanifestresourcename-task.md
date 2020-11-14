---
title: CreateVisualBasicManifestResourceName 任务 | Microsoft Docs
description: 使用 MSBuild CreateVisualBasicManifestResourceName 任务可根据给定的 .resx 文件名或其他资源创建 Visual Basic 样式的清单名称。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, CreateVisualBasicManifestResourceName task
- CreateVisualBasicManifestResourceName task [MSBuild]
ms.assetid: 251c47b9-de32-414b-a138-bf45290af12e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ba80c4d52491a70a7bb8e294c9dd6ca2c9664ec3
ms.sourcegitcommit: bd9417123c6ef67aa2215307ba5eeec511e43e02
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92796727"
---
# <a name="createvisualbasicmanifestresourcename-task"></a>CreateVisualBasicManifestResourceName 任务

根据给定的 .resx 文件名或其他资源创建 Visual Basic 样式的清单名称。

## <a name="parameters"></a>参数

 下表描述 [CreateVisualBasicManifestResourceName 任务](../msbuild/createvisualbasicmanifestresourcename-task.md)的参数。

| 参数 | 说明 |
| - | - |
| `ManifestResourceNames` | <xref:Microsoft.Build.Framework.ITaskItem> `[]` 输出只读参数。<br /><br /> 生成的清单名称。 |
| `ResourceFiles` | 必选 `String` 参数。<br /><br /> 从中创建 Visual Basic 清单名称的资源文件的名称。 |
| `RootNamespace` | 可选 `String` 参数。<br /><br /> 资源文件的根命名空间，通常取自于项目文件。 可为 `null`。 |
| `PrependCultureAsDirectory` | 可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则将区域性名称作为目录名称添加到清单资源名称前。 默认值为 `true`。 |
| `ResourceFilesWithManifestResourceNames` | 可选的 `String` 只读输出参数。<br /><br /> 返回现在包括清单资源名称的资源文件的名称。 |

## <a name="remarks"></a>注解

 [CreateVisualBasicManifestResourceName 任务](../msbuild/createvisualbasicmanifestresourcename-task.md)决定了要分配到给定 .resx 或其他资源文件的相应清单资源名称。 该任务向资源文件提供一个逻辑名称，然后将其作为元数据附加到输出参数。

 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
