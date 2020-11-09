---
title: MultiToolTask 任务 | Microsoft Docs
description: 访问描述 MSBuild MultiToolTask 任务的必需参数和可选参数的表。
ms.custom: SEO-VS-2020
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.multitooltask
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), MultiToolTask task
- MultiToolTask task (MSBuild (C++))
author: ghogen
ms.author: ghogen
ms.workload:
- multiple
ms.openlocfilehash: 6d76aa3762b254ee35ada1e4e81fe857f509a4e5
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048967"
---
# <a name="multitooltask-task"></a>MultiToolTask 任务

无说明。

## <a name="parameters"></a>参数

下表描述了 MultiToolTask 任务的参数。

|参数|说明|
|---------------|-----------------|
|**EnvironmentVariablesToSet**|可选的 string[] 参数。|
|**SemaphoreProcCount**|可选的 string  参数。|
|**SchedulerFunction**|可选的 string  参数。|
|**SchedulerVerbose**|可选的 bool  参数。|
|**源**|必需的 **ITaskItem[]** 参数。|
|**TaskAssemblyName**|可选的 string  参数。|
|**TaskName**|必需的 **String** 参数。|
|**TrackerLogDirectory**|必需的 **String** 参数。|

## <a name="see-also"></a>另请参阅

[任务参考](../msbuild/msbuild-task-reference.md)
