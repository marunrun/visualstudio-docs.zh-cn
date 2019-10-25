---
title: GetOutOfDateItems 任务 |Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
f1_keywords:
- vc.task.getoutofdateitems
dev_langs:
- VB
- CSharp
- C++
- jsharp
- C++
helpviewer_keywords:
- MSBuild (C++), GetOutOfDateItems task
- GetOutOfDateItems task (MSBuild (C++))
author: mikeblome
ms.author: mblome
ms.workload:
- multiple
ms.openlocfilehash: d3dc343c595606faf5bd31d7f087f7ba8d95f69e
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72747308"
---
# <a name="getoutofdateitems-task"></a>GetOutOfDateItems 任务

帮助程序任务，可读取旧 tlog、写入新 tlog 并返回不是最新的项集合。

## <a name="parameters"></a>参数

下表介绍了 GetOutOfDateItems 任务的参数  。

|参数|说明|
|---------------|-----------------|
|**CheckForInterdependencies**|可选的 bool  参数。|
|**CommandMetadataName**|可选的 string  参数。|
|**DependenciesMetadataName**|可选的 string  参数。|
|**HasInterdependencies**|可选的 bool  输出参数。|
|**OutOfDateSources**|可选的 **ITaskItem[]** 输出参数。|
|**OutputsMetadataName**|必需的 **String** 参数。|
|**Sources**|可选的 **ITaskItem[]** 参数。|
|**TLogDirectory**|必需的 **String** 参数。|
|**TLogNamePrefix**|必需的 **String** 参数。|

## <a name="see-also"></a>请参阅

[任务参考](../msbuild/msbuild-task-reference.md)