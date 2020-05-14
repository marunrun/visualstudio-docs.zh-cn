---
title: UpdateManifest 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, UpdateManifest task
- UpdateManifest task [MSBuild]
ms.assetid: 1291fd33-b89e-4e15-8fb1-69f9625cf2d2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 25e410ba3122e0065f92186195ee5a82d6a55c2f
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77631337"
---
# <a name="updatemanifest-task"></a>UpdateManifest 任务

更新清单中所选的属性并重新签名。

## <a name="parameters"></a>参数

 下表描述了 `UpdateManifest` 任务的参数。

|参数|说明|
|---------------|-----------------|
|`ApplicationManifest`|必选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定应用程序清单。|
|`ApplicationPath`|必选 `String` 参数。<br /><br /> 指定应用程序清单的路径。|
|`InputManifest`|必选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定要更新的清单。|
|`OutputManifest`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 输出参数。<br /><br /> 指定包含更新的属性的清单。|

## <a name="remarks"></a>备注

 除了具有表中列出的参数外，此任务还将从 <xref:Microsoft.Build.Utilities.Task> 类继承参数。 有关这些其他参数的列表及其说明，请参阅[任务基类](../msbuild/task-base-class.md)。

## <a name="see-also"></a>另请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)