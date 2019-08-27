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
- MSBuild (Visual C++), MultiToolTask task
- MultiToolTask task (MSBuild (Visual C++))
author: mikeblome
ms.author: mblome
ms.workload:
- multiple
ms.openlocfilehash: a16a61c06bf80bef3fbb78f155cd8b41905a8d72
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963905"
---
# <a name="multitooltask-task"></a>MultiToolTask 任务

无说明。

## <a name="parameters"></a>参数

下表描述了 MultiToolTask 任务的参数。

|参数|说明|
|---------------|-----------------|
|**EnvironmentVariablesToSet**|可选的 string[] 参数。|
|**SemaphoreProcCount**|可选的 string 参数。|
|**SchedulerFunction**|可选的 string 参数。|
|**SchedulerVerbose**|可选的 bool 参数。|
|**Sources**|必需的 **ITaskItem[]** 参数。|
|**TaskAssemblyName**|可选的 string 参数。|
|**TaskName**|必需的 **String** 参数。|
|**TrackerLogDirectory**|必需的 **String** 参数。|

## <a name="see-also"></a>请参阅

[任务参考](../msbuild/msbuild-task-reference.md)