---
title: CustomBuild 任务 | Microsoft Docs
description: 本文介绍 MSBuild CustomBuild 任务，该任务由 MSBuild 用于支持自定义 C++ 生成过程。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 640c1e6ae286b45f8700709829140093452a9491
ms.sourcegitcommit: bd9417123c6ef67aa2215307ba5eeec511e43e02
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2020
ms.locfileid: "92796545"
---
# <a name="custombuild-task"></a>CustomBuild 任务

包装 Microsof C++ 编译器工具 (cmd.exe)。 此类派生自 [TrackedVCToolTask](../msbuild/trackedvctooltask-base-class.md)，但不使用文件跟踪来发现文件依赖项。 所有依赖项都应显式指定为 AdditionalDependencies，以便使增量生成正常工作。

## <a name="parameters"></a>参数

下表描述了 CustomBuild 任务  的参数。

|参数|说明|
|---------------|-----------------|
|**BuildSuffix**|可选的 string  参数。|
|**源**|必需的 **ITaskItem[]** 参数。|
|**TrackerLogDirectory**|可选的 string  参数。|

## <a name="see-also"></a>另请参阅

[任务参考](../msbuild/msbuild-task-reference.md)
