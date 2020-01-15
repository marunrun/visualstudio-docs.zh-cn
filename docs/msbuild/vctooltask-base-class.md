---
title: VCToolTask 类 | Microsoft Docs
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
ms.openlocfilehash: df75bb998d2b8c6486e20c4c3ca0d80347c8f88a
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591666"
---
# <a name="vctooltask-base-class"></a>VCToolTask 基类

许多任务最终继承自 <xref:Microsoft.Build.Utilities.Task> 类和 [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) 类。 此类向派生自该类的任务添加几个参数。 本文档中列出了这些参数。

## <a name="parameters"></a>参数

下表介绍了 VCToolTask  基类的参数。

|参数|描述|
|---------------|-----------------|
|**ActiveToolSwitchesValues**|可选的 Dictionary\<string, ToolSwitch>  参数。|
|**AdditionalOptions**|可选的 string  参数。|
|**EffectiveWorkingDirectory**|可选的 string  参数。|
|**EnableErrorListRegex**|可选的 bool  参数。<br/><br/>默认值为 `true`。|
|**ErrorListRegex**|可选的 **ITaskItem[]** 参数。|
|**ErrorListListExclusion**|可选的 **ITaskItem[]** 参数。|
|**GenerateCommandLine**|可选的 string  参数。<br/><br/>使用 CommandLineFormat  format  [default = CommandLineFormat.ForBuildLog] 和 EscapeFormat  escapeFormat  [default = EscapeFormat.Default] 值。|
|**GenerateCommandLineExceptSwitches**|可选的 string  参数。<br/><br/>使用 string[]  switchesToRemove  、CommandLineFormat  format  [default = CommandLineFormat.ForBuildLog] 和 EscapeFormat  escapeFormat  [default = EscapeFormat.Default] 值。|

## <a name="see-also"></a>请参阅

[任务参考](../msbuild/msbuild-task-reference.md)<br/>
[任务](../msbuild/msbuild-tasks.md)
