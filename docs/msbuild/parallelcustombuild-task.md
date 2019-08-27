---
title: ParallelCustomBuild 任务 | Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.parallelcustombuild
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (Visual C++), ParallelCustomBuild task
- ParallelCustomBuild task (MSBuild (Visual C++))
author: mikeblome
ms.author: mblome
ms.workload:
- multiple
ms.openlocfilehash: 54623ab1c58d85de55c5b8a24384bf0be46f1a61
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62963749"
---
# <a name="parallelcustombuild-task"></a>ParallelCustomBuild 任务

运行 [CustomBuild 任务](../msbuild/custombuild-task.md)的并行实例。

## <a name="parameters"></a>参数

下表介绍了 ParallelCustomBuild 任务的参数。

|参数|说明|
|---------------|-----------------|
|**BreakOnFirstFailure**|可选的 bool 参数。|
|**MaxItemsInBatch**|可选 **int** 参数。|
|**MaxProcesses**|可选 **int** 参数。|
|**Sources**|必需的 **ITaskItem[]** 参数。|

## <a name="see-also"></a>请参阅

[任务参考](../msbuild/msbuild-task-reference.md)