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
- MSBuild (Visual C++), GetOutOfDateItems task
- GetOutOfDateItems task (MSBuild (Visual C++))
author: mikeblome
ms.author: mblome
ms.workload:
- multiple
ms.openlocfilehash: e3393dd7e81fa98c49dd09a32457171286f88f18
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977485"
---
# <a name="getoutofdateitems-task"></a>GetOutOfDateItems 任务

帮助程序任务，可读取旧 tlog、写入新 tlog 并返回不是最新的项集合。

## <a name="parameters"></a>参数

下表介绍了 GetOutOfDateItems 任务的参数。

|参数|说明|
|---------------|-----------------|
|**CheckForInterdependencies**|可选的 bool 参数。|
|**CommandMetadataName**|可选的 string 参数。|
|**DependenciesMetadataName**|可选的 string 参数。|
|**HasInterdependencies**|可选的 bool 输出参数。|
|**OutOfDateSources**|可选的 **ITaskItem[]** 输出参数。|
|**OutputsMetadataName**|必需的 **String** 参数。|
|**Sources**|可选的 **ITaskItem[]** 参数。|
|**TLogDirectory**|必需的 **String** 参数。|
|**TLogNamePrefix**|必需的 **String** 参数。|

## <a name="see-also"></a>请参阅

[任务参考](../msbuild/msbuild-task-reference.md)