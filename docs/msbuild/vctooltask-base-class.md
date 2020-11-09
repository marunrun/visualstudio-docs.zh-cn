---
title: VCToolTask 类 | Microsoft Docs
description: 了解 VCToolTask 基类向继承自它的任务添加的多个参数。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: b2e45d7c672ebc2177c2bb197399133e7b077a5c
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93046732"
---
# <a name="vctooltask-base-class"></a>VCToolTask 基类

许多任务最终继承自 <xref:Microsoft.Build.Utilities.Task> 类和 [ToolTask](/dotnet/api/microsoft.build.utilities.tooltask) 类。 此类向派生自该类的任务添加几个参数。 本文档中列出了这些参数。

## <a name="parameters"></a>参数

下表介绍了 VCToolTask  基类的参数。

|参数|说明|
|---------------|-----------------|
|**ActiveToolSwitchesValues**|可选 Dictionary\<string, ToolSwitch> 参数。|
|**AdditionalOptions**|可选的 string  参数。|
|**EffectiveWorkingDirectory**|可选的 string  参数。|
|**EnableErrorListRegex**|可选的 bool  参数。<br/><br/>默认值为 `true`。|
|**ErrorListRegex**|可选的 **ITaskItem[]** 参数。|
|**ErrorListListExclusion**|可选的 **ITaskItem[]** 参数。|
|**GenerateCommandLine**|可选的 string  参数。<br/><br/>使用 CommandLineFormat  format  [default = CommandLineFormat.ForBuildLog] 和 EscapeFormat  escapeFormat  [default = EscapeFormat.Default] 值。|
|**GenerateCommandLineExceptSwitches**|可选的 string  参数。<br/><br/>使用 string[]  switchesToRemove  、CommandLineFormat  format  [default = CommandLineFormat.ForBuildLog] 和 EscapeFormat  escapeFormat  [default = EscapeFormat.Default] 值。|

## <a name="see-also"></a>另请参阅

[任务参考](../msbuild/msbuild-task-reference.md)<br/>
[任务](../msbuild/msbuild-tasks.md)
