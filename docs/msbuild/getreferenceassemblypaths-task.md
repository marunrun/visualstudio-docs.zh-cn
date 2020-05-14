---
title: GetReferenceAssemblyPaths 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 178ef49c-5dee-405b-a14b-a37f41dc0609
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d2ca532e37fa2f70800416539a7de2ff5e9978e2
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633975"
---
# <a name="getreferenceassemblypaths-task"></a>GetReferenceAssemblyPaths 任务

返回各种框架的引用程序集路径。

## <a name="parameters"></a>参数

 下表描述了 `GetReferenceAssemblyPaths` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`ReferenceAssemblyPaths`|可选 `String[]` 输出参数。<br /><br /> 基于 `TargetFrameworkMoniker` 参数返回路径。 如果 `TargetFrameworkMoniker` 为 null 或为空，则此路径将为 `String.Empty`。|
|`FullFrameworkReferenceAssemblyPaths`|可选 `String[]` 输出参数。<br /><br /> 基于 `TargetFrameworkMoniker` 参数返回路径，无需考虑名字对象的配置文件部分。 如果 `TargetFrameworkMoniker` 为 null 或为空，则此路径将为 `String.Empty`。|
|`TargetFrameworkMoniker`|可选 `String` 参数。<br /><br /> 指定与引用程序集路径关联的目标框架名字对象。|
|`RootPath`|可选 `String` 参数。<br /><br /> 指定用于生成引用程序集路径的根路径。|
|`BypassFrameworkInstallChecks`|可选 <xref:System.Boolean> 参数。<br /><br /> 如果为 `true`，则绕过基本检查。默认情况下，`GetReferenceAssemblyPaths` 执行这些基本检查是为了确保已根据目标框架安装了某些运行时框架。|
|`TargetFrameworkMonikerDisplayName`|可选 `String` 输出参数。<br /><br /> 指定目标框架名字对象的显示名称。|

## <a name="remarks"></a>备注

 除了具有表中列出的参数外，此任务还将从本身继承自 <xref:Microsoft.Build.Tasks.TaskExtension> 类的 <xref:Microsoft.Build.Utilities.Task> 类继承参数。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)