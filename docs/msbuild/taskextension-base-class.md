---
title: TaskExtension 基类 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, tool task base class
- tool task base class [MSBuild]
ms.assetid: 08bb8059-b7e2-4565-89ba-d9034d4f0e16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b5e39b6a785b6542d95477dec761c1857c4222be
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62938974"
---
# <a name="taskextension-base-class"></a>TaskExtension 基类
很多任务继承自 <xref:Microsoft.Build.Tasks.TaskExtension> 类，该类本身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 此继承链向从它们派生的任务添加了几个参数。 本文档中列出了这些参数。

## <a name="parameters"></a>参数
 下表介绍基类的参数。

|参数|说明|
|---------------|-----------------|
|<xref:Microsoft.Build.Utilities.Task.BuildEngine%2A>|可选 <xref:Microsoft.Build.Framework.IBuildEngine> 参数。<br /><br /> 指定可供任务使用的生成引擎接口。 生成引擎会自动设置此参数，以允许任务回调到其中。|
|<xref:Microsoft.Build.Utilities.Task.BuildEngine2%2A>|可选 <xref:Microsoft.Build.Framework.IBuildEngine2> 参数。<br /><br /> 指定可供任务使用的生成引擎接口。 生成引擎会自动设置此参数，以允许任务回调到其中。<br /><br /> 这是一个便捷属性，使从此类继承的任务作者不必将值从 `IBuildEngine` 强制转换为 `IBuildEngine2`。|
|<xref:Microsoft.Build.Utilities.Task.BuildEngine3%2A>|可选 <xref:Microsoft.Build.Framework.IBuildEngine3> 参数。<br /><br /> 指定主机使用的生成引擎接口。|
|<xref:Microsoft.Build.Utilities.Task.HostObject%2A>|可选 <xref:Microsoft.Build.Framework.ITaskHost> 参数。<br /><br /> 指定主机对象实例（可以为 null）。 如果主机 IDE 具有与此特定任务关联的主机对象，则生成引擎会设置此属性。|
|<xref:Microsoft.Build.Tasks.TaskExtension.Log%2A>|可选 <xref:Microsoft.Build.Utilities.TaskLoggingHelper> 只读参数。<br /><br /> 获取包含任务日志记录方法的 `TaskLoggingHelperExtension` 对象。|

## <a name="see-also"></a>请参阅
- [任务参考](../msbuild/msbuild-task-reference.md)
- [任务](../msbuild/msbuild-tasks.md)