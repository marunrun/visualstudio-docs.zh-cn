---
title: MultiToolTask 任务 | Microsoft Docs
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
ms.openlocfilehash: d9e8b23492f23d39977b4eb26f8ee633b8463f27
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75565209"
---
# <a name="multitooltask-task"></a>MultiToolTask 任务

无说明。

## <a name="parameters"></a>参数

下表描述了 MultiToolTask  任务的参数。

|参数|描述|
|---------------|-----------------|
|**EnvironmentVariablesToSet**|可选的 string[]  参数。|
|**SemaphoreProcCount**|可选的 string  参数。|
|**SchedulerFunction**|可选的 string  参数。|
|**SchedulerVerbose**|可选的 bool  参数。|
|**Sources**|必需的 **ITaskItem[]** 参数。|
|**TaskAssemblyName**|可选的 string  参数。|
|**TaskName**|必需的 **String** 参数。|
|**TrackerLogDirectory**|必需的 **String** 参数。|

## <a name="see-also"></a>请参阅

[任务参考](../msbuild/msbuild-task-reference.md)
