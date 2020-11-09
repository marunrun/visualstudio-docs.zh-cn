---
title: ParallelCustomBuild 任务 | Microsoft Docs
description: 了解 MSBuild 如何使用 ParallelCustomBuild 任务来运行 CustomBuild 任务的并行实例。
ms.custom: SEO-VS-2020
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
- MSBuild (C++), ParallelCustomBuild task
- ParallelCustomBuild task (MSBuild (C++))
author: corob-msft
ms.author: corob
ms.workload:
- multiple
ms.openlocfilehash: f4491d0a5e9c9d3a2554bd32211fd1fa8f7be2d2
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048891"
---
# <a name="parallelcustombuild-task"></a>ParallelCustomBuild 任务

运行 [CustomBuild 任务](../msbuild/custombuild-task.md)的并行实例。

## <a name="parameters"></a>参数

下表介绍了 ParallelCustomBuild 任务的参数。

|参数|说明|
|---------------|-----------------|
|**BreakOnFirstFailure**|可选的 bool  参数。|
|**MaxItemsInBatch**|可选 **int** 参数。|
|**MaxProcesses**|可选 **int** 参数。|
|**源**|必需的 **ITaskItem[]** 参数。|

## <a name="see-also"></a>另请参阅

[任务参考](../msbuild/msbuild-task-reference.md)