---
title: ResourcesGenerator 任务 | Microsoft Docs
ms.date: 11/04/2016
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8ef54bdc3b3c692869b4883cf4f92293551a1958
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62996773"
---
# <a name="resourcesgenerator-task"></a>ResourcesGenerator 任务
<xref:Microsoft.Build.Tasks.Windows.ResourcesGenerator> 任务将一个或多个资源（二进制格式的 .jpg、.ico、.bmp、[!INCLUDE[TLA2#tla_xaml](../msbuild/includes/tla2sharptla_xaml_md.md)] 以及其他扩展名类型）嵌入 .resources 文件中。

## <a name="task-parameters"></a>任务参数

|参数|说明|
|---------------|-----------------|
|`OutputPath`|必需的 **String** 参数。<br /><br /> 指定输出目录的路径。 如果路径不是绝对路径，则将它视为相对于根项目目录的路径。|
|`OutputResourcesFile`|必需的 **ITaskItem[]** 输出参数。<br /><br /> 指定生成的 .resources 文件的路径和名称。 如果该路径不是绝对路径，则生成根项目目录的相对 .resources 文件。|
|`ResourcesFiles`|必需的 **ITaskItem[]** 参数。<br /><br /> 指定一个或多个资源，以嵌入生成的 .resources 文件中。|

## <a name="example"></a>示例
 以下示例使用单个 .bmp 资源生成 .resources 文件。 向项目根目录的相对目录生成 .bmp 资源。

```xml
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

## <a name="see-also"></a>请参阅
- [WPF MSBuild 参考](../msbuild/wpf-msbuild-reference.md)
- [任务参考](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
- [生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)