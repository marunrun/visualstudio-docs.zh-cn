---
title: FormatVersion 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 96e692f6-b581-46ca-8cc9-441a1861e371
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ee6e163bd6587d93c970a56ac1c08383084ddc0c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68149617"
---
# <a name="formatversion-task"></a>FormatVersion 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

将修订号追加到版本号。  
  
- 案例 #1：输入：Version=\<undefined>; Revision=\<don't care>; 输出：OutputVersion ="1.0.0.0"  
  
- 案例 #2：输入：Version="1.0.0.*"  Revision="5" 输出：OutputVersion="1.0.0.5"  
  
- 案例 #3：输入：Version="1.0.0.0" Revision=\<don't care>; 输出：OutputVersion ="1.0.0.0"  
  
## <a name="parameters"></a>参数  
 下表描述了 `FormatVersion` 任务的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|`FormatType`|可选 `String` 参数。<br /><br /> 指定格式类型。<br /><br /> -“Version”= 版本。<br />-“Path”=将“.”替换为“_”；|  
|`OutputVersion`|可选 `String` 输出参数。<br /><br /> 指定包含修订号的输出版本。|  
|`Revision`|可选 `Int32` 参数。<br /><br /> 指定要追加到该版本的修订。|  
|`Version`|可选 `String` 参数。<br /><br /> 指定要进行格式化的版本号字符串。|  
  
## <a name="remarks"></a>备注  
 除了具有表中列出的参数外，此任务还将从本身继承自 <xref:Microsoft.Build.Utilities.Task> 类的 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)。  
  
## <a name="see-also"></a>另请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)
