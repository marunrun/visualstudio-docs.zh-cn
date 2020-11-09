---
title: ResolveNonMSBuildProjectOutput 任务 | Microsoft Docs
description: 了解 MSBuild 如何使用 ResolveNonMSBuildProjectOutput 任务来确定非 MSBuild 项目引用的输出文件。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, ResolveNonMSBuildProjectOutput task
- ResolveNonMSBuildProjectOutput task [MSBuild]
ms.assetid: a0b8fcec-8c8d-4867-85ac-5304c5108e5e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3486788331574aa70874c0deeefa3c553404c166
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048516"
---
# <a name="resolvenonmsbuildprojectoutput-task"></a>ResolveNonMSBuildProjectOutput 任务

确定非 MSBuild 项目引用的输出文件。

## <a name="parameters"></a>参数

 下表描述了 `ResolveNonMSBuildProjectOutput` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`PreresolvedProjectOutputs`|可选 `String` 参数。<br /><br /> 指定包含解析的项目输出的 XML 字符串。|
|`ProjectReferences`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定项目引用。|
|`ResolvedOutputPaths`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含已解析引用路径的列表（并保留原始项目引用特性）。|
|`UnresolvedProjectReferences`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含项目引用项的列表，其中这些项无法使用输出的预解析列表进行解析。<br /><br /> 因为 Visual Studio 只预解析非 MSBuild 项目，这意味着此列表中的项目引用都采用 MSBuild 格式。|

## <a name="remarks"></a>备注

 除了具有表中列出的参数外，此任务还将从本身继承自 <xref:Microsoft.Build.Utilities.Task> 类的 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)