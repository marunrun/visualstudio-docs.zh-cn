---
title: FileClassifier 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- classifying a resource set to embed in an assembly [WPF MSBuild]
- non-localizable resources [WPF MSBuild], classifying to embed in an assembly
- FileClassifier task [WPF MSBuild]
ms.assetid: 14e03310-fcc0-4bb2-a84d-cda12be66367
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 46ed1b1f94cd2ef23ff0704912cb2a2194ba7dab
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634183"
---
# <a name="fileclassifier-task"></a>FileClassifier 任务

<xref:Microsoft.Build.Tasks.Windows.FileClassifier> 任务将一组源资源分类为将嵌入到程序集的源资源。 如果资源不可本地化，则将其嵌入主应用程序程序集；否则，将其嵌入附属程序集。

## <a name="task-parameters"></a>任务参数

|参数|说明|
|---------------|-----------------|
|`CLREmbeddedResource`|未使用。|
|`CLRResourceFiles`|未使用。|
|`CLRSatelliteEmbeddedResource`|未使用。|
|`Culture`|可选 **String** 参数。<br /><br /> 指定生成的区域性。 如果生成不可本地化，则此值可能为 **Null**。 如果为 **Null**，默认值是 **CultureInfo.InvariantCulture** 返回的小写值。|
|`MainEmbeddedFiles`|可选的 **ITaskItem[]** 输出参数。<br /><br /> 指定嵌入到主程序集中的非本地化资源。|
|`OutputType`|必需的 **String** 参数。<br /><br /> 指定要将指定源文件嵌入的文件类型。 有效值为 **exe**、**winexe** 或 **library**。|
|`SatelliteEmbeddedFiles`|可选的 **ITaskItem[]** 输出参数。<br /><br /> 指定嵌入区域性附属程序集中的可本地化文件，该区域性由 **Culture** 参数指定。|
|`SourceFiles`|必需的 **ITaskItem[]** 参数。<br /><br /> 指定要分类的文件的列表。|

## <a name="remarks"></a>备注

如果未设置 **Culture** 参数，则所有通过 **SourceFiles** 参数指定的资源都不可本地化；反之都可本地化（除非它们与设置为 **false** 的 **Localizable** 属性相关联）。

## <a name="example"></a>示例

下面示例将单个源文件分类为资源，并将其嵌入法语-加拿大 (fr-CA) 区域性的附属程序集。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.FileClassifier"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <ItemGroup>
    <Resource Include="Resource1.bmp" />
  </ItemGroup>
  <Target Name="FileClassifierTask">
    <FileClassifier
      SourceFiles="Resource1.bmp"
      Culture="fr-CA"
      OutputType="exe" />
  </Target>
</Project>
```

## <a name="see-also"></a>另请参阅

- [WPF MSBuild 参考](../msbuild/wpf-msbuild-reference.md)
- [任务参考](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
- [生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
