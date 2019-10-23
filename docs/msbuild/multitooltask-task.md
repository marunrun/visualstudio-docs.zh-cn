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
author: mikeblome
ms.author: mblome
ms.workload:
- multiple
ms.openlocfilehash: 137fb53a46c3fa31a69602906ef53d2f65e25c4b
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747231"
---
# <a name="multitooltask-task"></a>MultiToolTask 任务

无说明。

## <a name="parameters"></a>参数

下表描述了 MultiToolTask  任务的参数。

|参数|说明|
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