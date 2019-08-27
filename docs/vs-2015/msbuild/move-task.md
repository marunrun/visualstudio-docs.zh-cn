---
title: 移动任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, Move task
- Move task [MSBuild]
ms.assetid: d1405347-1309-4f18-b565-905408093d59
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ab75ccebd618946454c3386f564e3f6199409935
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68191575"
---
# <a name="move-task"></a>Move 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

将文件移至新位置。  
  
## <a name="parameters"></a>参数  
 下表描述了 `Move` 任务的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|`DestinationFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 指定要将源文件移动到的文件的列表。 此列表应与 `SourceFiles` 参数中指定的列表具有一对一的映射关系。 也就是说，`SourceFiles` 中指定的第一个文件将移动到 `DestinationFiles` 中指定的第一个位置，依次类推。|  
|`DestinationFolder`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定要将文件移动到的目录。|  
|`MovedFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包含已成功移动的项。|  
|`OverwriteReadOnlyFiles`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则覆盖文件，即使它们标记为只读文件。|  
|`SourceFiles`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要移动的文件。|  
  
## <a name="remarks"></a>备注  
 必须指定 `DestinationFolder` 参数或 `DestinationFiles` 参数，但不能对两者都进行指定。 如果指定了两者，则任务失败并记录一条错误。  
  
 除了具有表中列出的参数外，此任务还将从本身继承自 <xref:Microsoft.Build.Utilities.Task> 类的 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)。  
  
## <a name="see-also"></a>另请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)
