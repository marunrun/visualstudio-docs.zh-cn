---
title: AssignTargetPath 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: 0e830e31-3bcf-4259-b2a8-a5df49b92d51
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f7bf12e9f6c90ce544205370a8ed26440388b0a6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187019"
---
# <a name="assigntargetpath-task"></a>AssignTargetPath 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

此任务接受文件列表，并添加 `<TargetPath>` 属性（如果尚未指定）。  
  
## <a name="task-parameters"></a>任务参数  
 下表描述了 `AssignTargetPath` 任务的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|`RootFolder`|可选的 `string` 输入参数。<br /><br /> 包含文件夹的路径，该文件夹包含目标链接。|  
|`Files`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输入参数。<br /><br /> 包含传入的文件列表。|  
|`AssignedFiles`|Optional<br /><br /> <xref:Microsoft.Build.Framework.ITaskItem> `[]` 输出参数。<br /><br /> 包含生成的文件列表。|  
  
## <a name="remarks"></a>备注  
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)。  
  
## <a name="example"></a>示例  
 下例执行 `AssignTargetPath` 任务以对项目进行配置。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
    <Target Name="MyProject">  
        <AssignTargetPath  
RootFolder="Resources"  
            Files="@(ResourceFiles)"  
            <Output TaskParameter="AssignedFiles"  
                ItemName="OutAssignedFiles"/>  
        </AssignTargetPath>  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>另请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)
