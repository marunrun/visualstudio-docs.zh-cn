---
title: UidManager 任务 | Microsoft Docs
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
- UidManager task [WPF MSBuild]
- UidManager task [WPF MSBuild], parameters
- managing UIDs when localizing XAML elements [WPF MSBuild]
- localizing XAML elements [WPF MSBuild], managing UIDs
- checking UIDs when localizing XAML elements [WPF MSBuild]
ms.assetid: 4fc7b5a5-11b0-46ca-9656-8c2a0b08d1fe
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5fd8175911def7fb1b63dc63d967c404d649e9e4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65703692"
---
# <a name="uidmanager-task"></a>UidManager 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:Microsoft.Build.Tasks.Windows.UidManager> 任务将检查、更新或删除唯一标识符 (UID)，以对源 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 文件中包含的所有 [!INCLUDE[TLA#tla_xaml](../includes/tlasharptla-xaml-md.md)] 元素进行本地化。  
  
## <a name="task-parameters"></a>任务参数  
  
|参数|描述|  
|---------------|-----------------|  
|`IntermediateDirectory`|可选 **String** 参数。<br /><br /> 指定用于备份由 **MarkupFiles** 参数指定的源 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 文件的目录。|  
|`MarkupFiles`|必需的 **ITaskItem[]** 参数。<br /><br /> 指定要包含的源 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)]文件，以用于 UID 检查、更新或删除。|  
|`Task`|必需的 **String** 参数。<br /><br /> 指定想要执行的 UID 管理任务。 有效选项为“检查”、“更新”或“删除”。|  
  
## <a name="example"></a>示例  
 下例使用 <xref:Microsoft.Build.Tasks.Windows.UidManager> 任务来检查指定的源 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 文件是否包含具有适当 UID 的 [!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 元素。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.UidManager"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="UidManagerTask">  
    <UidManager  
      Task="Check"  
      MarkupFiles="Page1.xaml;Page2.xaml"  
      IntermediateDirectory="c:\UidManagerIntermediateDirectory" />  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>请参阅  
 [WPF MSBuild 引用](../msbuild/wpf-msbuild-reference.md)   
 [任务参考](../msbuild/wpf-msbuild-task-reference.md)   
 [MSBuild 参考](../msbuild/msbuild-reference.md)   
 [任务参考](../msbuild/msbuild-task-reference.md)   
 [Building a WPF Application (WPF)](https://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c) （生成 WPF 应用程序 (WPF)）  
 [如何：本地化应用程序](https://msdn.microsoft.com/library/5001227e-9326-48a4-9dcd-ba1b89ee6653)
