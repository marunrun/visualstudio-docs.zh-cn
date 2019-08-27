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
- MSBuild (Visual C++), CustomBuild task
- CustomBuild task (MSBuild (Visual C++))
author: mikeblome
ms.author: mblome
ms.workload:
- multiple
ms.openlocfilehash: 04f33f3852f051e1f492cb2b6dca44fcdb260e11
ms.sourcegitcommit: 32144a09ed46e7223ef7dcab647a9f73afa2dd55
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2019
ms.locfileid: "67587006"
---
# <a name="custombuild-task"></a>CustomBuild 任务

包装 Visual C++ 编译器工具 cmd.exe。 此类派生自 [TrackedVCToolTask](../msbuild/trackedvctooltask-base-class.md)，但不使用文件跟踪来发现文件依赖项。 所有依赖项都应显式指定为 AdditionalDependencies，以便使增量生成正常工作。

## <a name="parameters"></a>参数

下表描述了 CustomBuild 任务  的参数。

|参数|说明|
|---------------|-----------------|
|**BuildSuffix**|可选的 string  参数。|
|**Sources**|必需的 **ITaskItem[]** 参数。|
|**TrackerLogDirectory**|可选的 string  参数。|

## <a name="see-also"></a>请参阅

[任务参考](../msbuild/msbuild-task-reference.md)
