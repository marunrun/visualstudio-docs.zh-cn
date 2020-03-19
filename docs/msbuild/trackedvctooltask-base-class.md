---
title: TrackedVCToolTask 类 |Microsoft Docs
ms.date: 03/10/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
author: ghogen
ms.author: ghogen
ms.workload:
- multiple
ms.openlocfilehash: 8a4272f7800e0532c0674fe7117e839cb16557d5
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75594924"
---
# <a name="trackedvctooltask-base-class"></a>TrackedVCToolTask 基类

许多任务最终继承自 <xref:Microsoft.Build.Utilities.Task> 类和 [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) 类。 此类会向派生自 [VCToolTask](../msbuild/vctooltask-base-class.md) 的任务添加几个参数。 本文档中列出了这些参数。

## <a name="parameters"></a>参数

下表介绍了 TrackedVCToolTask  基类的参数。

|参数|说明|
|---------------|-----------------|
|**DeleteOutputOnExecute**|可选的 bool  参数。|
|**EnableExecuteTool**|可选的 bool  参数。|
|**ExcludedInputPaths**|可选的 **ITaskItem[]** 参数。|
|**MinimalRebuildFromTracking**|可选的 bool  参数。|
|**PathOverride**|可选的 string  参数。|
|**PostBuildTrackingCleanup**|可选的 bool  参数。|
|**RootSource**|可选的 string  参数。|
|**SkippedExecution**|可选的 bool  输出参数。|
|**SourcesCompiled**|可选的 **ITaskItem[]** 输出参数。|
|**TLogCommandFile**|可选的 ITaskItem  参数。|
|**TLogReadFiles**|可选的 **ITaskItem[]** 参数。|
|**TLogWriteFiles**|可选的 **ITaskItem[]** 参数。|
|**ToolArchitecture**|可选的 string  参数。|
|**TrackCommandLines**|可选的 bool  参数。|
|**TrackFileAccess**|可选的 bool  参数。|
|**TrackedInputFilesToIgnore**|可选的 **ITaskItem[]** 参数。|
|**TrackedOutputFilesToIgnore**|可选的 **ITaskItem[]** 参数。|
|**TrackerFrameworkPath**|可选的 string  参数。|
|**TrackerSdkPath**|可选的 string  参数。|

## <a name="see-also"></a>另请参阅

[任务参考](../msbuild/msbuild-task-reference.md)<br/>
[任务](../msbuild/msbuild-tasks.md)
