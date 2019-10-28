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
author: mikeblome
ms.author: mblome
ms.workload:
- multiple
ms.openlocfilehash: 678068d1b6acc055fa65e6d0305b07152ed28695
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748104"
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

## <a name="see-also"></a>请参阅

[任务参考](../msbuild/msbuild-task-reference.md)
