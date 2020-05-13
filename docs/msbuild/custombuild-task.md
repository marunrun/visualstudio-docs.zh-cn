---
title: CustomBuild 任务 | Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.custombuild
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), CustomBuild task
- CustomBuild task (MSBuild (C++))
author: ghogen
ms.author: ghogen
ms.workload:
- multiple
ms.openlocfilehash: d95b6e7d4197487adc13050572ac31310701c759
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75595340"
---
# <a name="custombuild-task"></a>CustomBuild 任务

包装 Microsof C++ 编译器工具 (cmd.exe)。 此类派生自 [TrackedVCToolTask](../msbuild/trackedvctooltask-base-class.md)，但不使用文件跟踪来发现文件依赖项。 所有依赖项都应显式指定为 AdditionalDependencies，以便使增量生成正常工作。

## <a name="parameters"></a>参数

下表描述了 CustomBuild 任务  的参数。

|参数|说明|
|---------------|-----------------|
|**BuildSuffix**|可选的 string  参数。|
|**Sources**|必需的 **ITaskItem[]** 参数。|
|**TrackerLogDirectory**|可选的 string  参数。|

## <a name="see-also"></a>另请参阅

[任务参考](../msbuild/msbuild-task-reference.md)
