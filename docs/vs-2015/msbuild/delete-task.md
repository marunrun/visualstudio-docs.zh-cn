---
title: Delete 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#Delete
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- Delete task [MSBuild]
- MSBuild, Delete task
ms.assetid: 916bb2e3-3017-4828-ae27-c0b5c99bbb48
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ea1411925c6858bceaea3e2e190ecb1a5f2c7f89
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196543"
---
# <a name="delete-task"></a>Delete 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

删除指定的文件。  
  
## <a name="parameters"></a>参数  
 下表描述了 `Delete` 任务的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|`DeletedFiles`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 指定已成功删除的文件。|  
|`Files`|必选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要删除的文件。|  
|`TreatErrorsAsWarnings`|可选的 `Boolean` 参数<br /><br /> 如果为 `true`，错误将被记录为警告。 默认值是 `false`。|  
  
## <a name="remarks"></a>备注  
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)。  
  
## <a name="example"></a>示例  
 下面的示例删除文件 `MyApp.pdb`。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <PropertyGroup>  
        <AppName>MyApp</AppName>  
    </PropertyGroup>  
  
    <Target Name="DeleteFiles">  
        <Delete Files="$(AppName).pdb" />  
    </Target>  
</Project>  
```  
  
## <a name="see-also"></a>另请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)
