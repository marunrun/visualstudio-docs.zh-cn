---
title: XmlPeek 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- XmlPeek task [MSBuild]
- MSBuild, XmlPeek task
ms.assetid: 19196031-a3bc-41b5-9c4a-f2572630e179
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 59bc42bd438d80bbaf0ff45cd1c95447961cd437
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/26/2020
ms.locfileid: "77630621"
---
# <a name="xmlpeek-task"></a>XmlPeek 任务

从 XML 文件返回 XPath 查询指定的值。

## <a name="parameters"></a>参数

 下表描述了 `XmlPeek` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`Namespaces`|可选 `String` 参数。<br /><br /> 指定 XPath 查询前缀的命名空间。|
|`Query`|可选 `String` 参数。<br /><br /> 指定 XPath 查询。|
|`Result`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含由此任务返回的结果。|
|`XmlContent`|可选 `String` 参数。<br /><br /> 指定 XML 输入为字符串。|
|`XmlInputPath`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定 XML 输入为文件路径。|

## <a name="remarks"></a>备注

 除了具有表中列出的参数外，此任务还将从本身继承自 <xref:Microsoft.Build.Utilities.Task> 类的 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension 基类](../msbuild/taskextension-base-class.md)。

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
