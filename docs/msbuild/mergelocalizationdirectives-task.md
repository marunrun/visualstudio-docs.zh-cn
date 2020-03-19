---
title: MergeLocalizationDirectives 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- localizing XAML [WPF MSBuild], moving comments and attributes to a separate file
- MergeLocalizationDirectives task [WPF MSBuild], parameters
- MergeLocalizationDirectives task [WPF MSBuild]
- moving localization comments and attributes to a separate file [WPF MSBuild]
ms.assetid: 9095b4f1-88da-4194-914b-ee1456826830
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9c7699afeb09604a437aad091f9aaf9ce624d33e
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77633494"
---
# <a name="mergelocalizationdirectives-task"></a>MergeLocalizationDirectives 任务

<xref:Microsoft.Build.Tasks.Windows.MergeLocalizationDirectives> 任务可将本地化属性和一个或多个 XAML 二进制格式文件的注释合并到整个程序集的单一文件中。

## <a name="task-parameters"></a>任务参数

| 参数 | 描述 |
|------------------------------| - |
| `GeneratedLocalizationFiles` | 必需的 **ITaskItem[]** 参数。<br /><br /> 指定单个 XAML 二进制格式文件的本地化指令文件列表。 |
| `OutputFile` | 必需的 **String** 输出参数。<br /><br /> 指定编译的本地化指令程序集的输出路径。 |

## <a name="remarks"></a>备注

可将本地化属性和注释添加到 XAML 内容中。 借助 Windows Presentation Foundation (WPF) 本地化支持，可以去除本地化属性和注释，并将其放在独立于生成的程序集的 .loc  文件中。 可以通过使用 **LocalizationPropertyStorage** 属性执行此操作。 若要深入了解本地化属性和注释，以及 LocalizationPropertyStorage，请参阅[本地化属性和注释](/dotnet/framework/wpf/advanced/localization-attributes-and-comments)  。

## <a name="example"></a>示例

下面的示例将多个 XAML 二进制格式化文件的本地化注释合并到单个 .loc  文件中。

```xml
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <UsingTask
    TaskName="Microsoft.Build.Tasks.Windows.MergeLocalizationDirectives"
    AssemblyFile="C:\Program Files\Reference Assemblies\Microsoft\Framework\v3.0\PresentationBuildTasks.dll" />
  <Target Name="MergeLocalizationDirectivesTask">
    <MergeLocalizationDirectives
      GeneratedLocalizationFiles="obj\debug\page1.loc;obj\debug\page2.loc;obj\debug\page3.loc"
      OutputFile="obj\debug\WPFMSBuildSample.loc" />
  </Target>
</Project>
```

## <a name="see-also"></a>请参阅

- [WPF MSBuild 参考](../msbuild/wpf-msbuild-reference.md)
- [WPF MSBuild 任务参考](../msbuild/wpf-msbuild-task-reference.md)
- [MSBuild 参考](../msbuild/msbuild-reference.md)
- [MSBuild 任务参考](../msbuild/msbuild-task-reference.md)
- [生成 WPF 应用程序 (WPF)](/dotnet/framework/wpf/app-development/building-a-wpf-application-wpf)
