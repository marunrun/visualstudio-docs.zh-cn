---
title: RequiresFramework35SP1Assembly 任务 | Microsoft Docs
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
- RequiresFramework35SP1Assembly task [MSBuild]
- MSBuild, RequiresFramework35SP1Assembly task
ms.assetid: 755c018a-8a8b-4c94-8aee-3f171fc419e5
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ada207a619021922b999d0e821ecf27ba48dbb38
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68158744"
---
# <a name="requiresframework35sp1assembly-task"></a>RequiresFramework35SP1Assembly 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

确定应用程序是否需要 .NET Framework 3.5 SP1。  
  
## <a name="parameters"></a>参数  
 下表描述了 `RequiresFramework35SP1Assembly` 任务的参数。  
  
|参数|说明|  
|---------------|-----------------|  
|`Assemblies`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定在应用程序中引用的程序集。|  
|`CreateDesktopShortcut`|可选 `Boolean` 参数。<br /><br /> 如果为 `true`，安装期间会在桌面上创建一个快捷方式图标。|  
|`DeploymentManifestEntryPoint`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定应用程序的清单文件名。|  
|`EntryPoint`|可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指定应用程序运行时应执行的程序集。|  
|`ErrorReportUrl`|可选 `String` 参数。<br /><br /> 指定 ClickOnce 安装期间所遇对话框中显示的网站。|  
|`Files`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定在发布应用程序时将部署的文件列表。|  
|`ReferencedAssemblies`|可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定在项目中引用的程序集。|  
|`RequiresMinimumFramework35SP1`|可选 `Boolean` 输出参数。<br /><br /> 如果为 `true`，应用程序需要 .NET Framework 3.5 SP1。|  
|`SigningManifests`|可选 `Boolean` 输出参数。<br /><br /> 如果为 `true`，ClickOnce 清单已签名。|  
|`SuiteName`|可选 `String` 参数。<br /><br /> 指定  “开始”菜单上，应用程序的安装文件夹的名称。|  
|`TargetFrameworkVersion`|可选 `String` 参数。<br /><br /> 指定应用程序面向的 .NET Framework 版本。|  
  
## <a name="remarks"></a>备注  
 除了具有表中列出的参数外，此任务还将从本身继承自 <xref:Microsoft.Build.Utilities.Task> 类的 <xref:Microsoft.Build.Tasks.TaskExtension> 类继承参数。 有关这些其他参数的列表及其说明的信息，请参阅 [TaskExtension Base Class](../msbuild/taskextension-base-class.md)。  
  
## <a name="see-also"></a>另请参阅  
 [任务](../msbuild/msbuild-tasks.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)
