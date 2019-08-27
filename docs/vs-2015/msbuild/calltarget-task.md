---
title: CallTarget 任务 | Microsoft Docs
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
- CallTarget task [MSBuild]
- MSBuild, CallTarget task
ms.assetid: bb1fe2c4-4383-436f-8326-c24cc4a46150
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9093b35cc444fc0b346f81a91d20afe73bd476cd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160422"
---
# <a name="calltarget-task"></a>CallTarget 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

调用项目文件中的指定目标。  
  
## <a name="task-parameters"></a>任务参数  
 下表描述了 `CallTarget` 任务的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|`RunEachTargetSeparately`|可选 `Boolean` 输出参数。<br /><br /> 如果为 `true`，则对每个目标调用一次 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 引擎。 如果为 `false`，则调用一次 [!INCLUDE[vstecmsbuild](../includes/vstecmsbuild-md.md)] 引擎即可生成所有目标。 默认值为 `false`。|  
|`TargetOutputs`|可选的 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 输出参数。<br /><br /> 包括所有生成目标的输出。|  
|`Targets`|可选 `String[]` 参数。<br /><br /> 指定要生成的一个或多个目标。|  
|`UseResultsCache`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，则返回缓存的结果（如存在）。<br /><br /> 注意：运行 MSBuild 任务时，其输出会以生成项列表的形式缓存在作用域 (ProjectFileName, GlobalProperties)[TargetNames] 中  。|  
  
## <a name="remarks"></a>备注  
 如果 `Targets` 中指定的目标失败，`RunEachTargetSeparately` 为 `true`，则该任务会继续生成剩余目标。  
  
 如果要生成默认目标，请使用 [MSBuild 任务](../msbuild/msbuild-task.md)，并将 `Projects` 参数设置为等于 `$(MSBuildProjectFile)`。  
  
 除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)。  
  
## <a name="example"></a>示例  
 以下示例从内部 `CallOtherTargets` 调用 `TargetA`。  
  
```  
<Project DefaultTargets="CallOtherTargets"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  
    <Target Name="CallOtherTargets">  
        <CallTarget Targets="TargetA"/>  
    </Target>  
  
    <Target Name="TargetA">  
        <Message Text="Building TargetA..." />  
    </Target>  
  
</Project>  
```  
  
## <a name="see-also"></a>另请参阅  
 [任务参考](../msbuild/msbuild-task-reference.md)   
 [目标](../msbuild/msbuild-targets.md)
