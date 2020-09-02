---
title: ResourcesGenerator 任务 | Microsoft Docs
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
- embedding resources into a .resources file [WPF MSBuild]
- ResourcesGenerator task [WPF MSBuild]
- ResourcesGenerator task [WPF MSBuild], parameters
ms.assetid: e782bbac-9ee6-472b-8171-3ee008c77b4e
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: fa8b438727160bb5a752643f7ef9791ca5e09245
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682142"
---
# <a name="resourcesgenerator-task"></a>ResourcesGenerator 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

<xref:Microsoft.Build.Tasks.Windows.ResourcesGenerator> 任务将一个或多个资源（二进制格式的 .jpg、.ico、.bmp、[!INCLUDE[TLA2#tla_xaml](../includes/tla2sharptla-xaml-md.md)] 以及其他扩展名类型）嵌入 .resources 文件中。  
  
## <a name="task-parameters"></a>任务参数  
  
|参数|描述|  
|---------------|-----------------|  
|`OutputPath`|必需的 **String** 参数。<br /><br /> 指定输出目录的路径。 如果该路径不是绝对路径，则将其视作根项目目录的相对路径。|  
|`OutputResourcesFile`|必需的 **ITaskItem[]** 输出参数。<br /><br /> 指定生成的 .resources 文件的路径和名称。 如果该路径不是绝对路径，则生成根项目目录的相对 .resources 文件。|  
|`ResourcesFiles`|必需的 **ITaskItem[]** 参数。<br /><br /> 指定一个或多个资源，以嵌入生成的 .resources 文件中。|  
  
## <a name="example"></a>示例  
 以下示例使用单个 .bmp 资源生成 .resources 文件。 向项目根目录的相对目录生成 .bmp 资源。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <UsingTask   
    TaskName="Microsoft.Build.Tasks.Windows.ResourcesGenerator"   
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />  
  <Target Name="ResourcesGeneratorTask">  
    <ResourcesGenerator  
      ResourceFiles="Resource1.bmp"  
      OutputPath="myresources"  
      OutputResourcesFile="myresources\my.resources" />  
  </Target>  
</Project>  
```  
  
## <a name="see-also"></a>另请参阅  
 [WPF MSBuild 参考](../msbuild/wpf-msbuild-reference.md)   
 [任务引用](../msbuild/wpf-msbuild-task-reference.md)   
 [MSBuild 引用](../msbuild/msbuild-reference.md)   
 [任务引用](../msbuild/msbuild-task-reference.md)   
 [Building a WPF Application (WPF)](https://msdn.microsoft.com/library/a58696fd-bdad-4b55-9759-136dfdf8b91c)（生成 WPF 应用程序 (WPF)）
